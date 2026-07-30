# CalcMind AI — System Architecture

Status: Draft for review
Related issue: M1.1 — Define Project Architecture and Module Boundaries
Scope: Architecture and module interfaces only. No feature implementation is included here.

## 1. Purpose and Goals

CalcMind AI is a conversational calculator. It accepts natural-language messages, determines whether the user wants to perform a calculation or is simply chatting, extracts the arithmetic intent, executes it, remembers the result for follow-up requests, and replies in a friendly, human-readable way.

The architecture is built around five hard constraints from the issue:

- Calculation, conversation, and interface logic must never mix.
- Every core intelligence component (parsing, dialogue handling, response phrasing) is built from scratch — no cloud AI APIs, pretrained models, LLMs, transformers, chatbot frameworks, or third-party NLP engines.
- The system must run fully offline, on CPU, with no external dependencies for its core logic.
- CLI and desktop front ends are thin shells over one shared core.
- Every module must be independently unit-testable with no circular dependencies.

## 2. Module List and Responsibilities

| # | Module | Responsibility | Must NOT do |
|---|--------|-----------------|--------------|
| 1 | Input Processor | Receive raw user text; trim whitespace, normalize casing/punctuation where safe, strip control characters; pass normalized text onward. | Interpret meaning, detect intent, touch calculation or dialogue state. |
| 2 | Conversation Engine | Classify each normalized message as calculation-related or general conversation; drive dialogue flow (greetings, clarifications, follow-ups); ask for missing information. | Parse numbers/operations itself, perform arithmetic, format final user-facing text. |
| 3 | Natural-Language Parser | Detect calculation intent inside a message; extract numbers and operation phrases; produce a structured calculation request. | Execute the calculation, generate responses, manage conversation state. |
| 4 | Calculator Engine | Execute supported arithmetic operations on a structured request; return a structured result or structured error. | Know about conversation, phrasing, or the interface layer. |
| 5 | Conversation Context | Hold the last result and recent supported values in memory for the active session; resolve references like "it" or "that". | Perform calculations, generate text, persist permanently to disk (that is History Manager's job). |
| 6 | Response Generator | Convert a structured result or structured error into a friendly natural-language reply. | Perform or re-derive any calculation, mutate context or history. |
| 7 | History Manager | Persist completed calculations locally; provide read access to recent records. | Perform calculations, format responses, know about the UI. |
| 8 | Application Interfaces (CLI / Desktop) | Collect raw input from the user and display the final response, driving calls into the core system. | Contain calculation, parsing, dialogue, or response-generation logic. |

Each module has exactly one responsibility, matching the "single clearly defined responsibility" acceptance criterion.

## 3. End-to-End Processing Flow

```
User Message
     ↓
Input Processor            (raw text → cleaned text)
     ↓
Conversation Engine        (cleaned text → routed intent + dialogue state)
     ↓
Natural-Language Parser    (message text → StructuredCalculationRequest | ParseError)
     ↓
Calculator Engine          (StructuredCalculationRequest → CalculationResult | CalculationError)
     ↓
Conversation Context + History Manager   (store result, update "last value")
     ↓
Response Generator         (CalculationResult/Error → user-facing string)
     ↓
User Response
```

Notes on branching not shown in the linear diagram:
- If the Conversation Engine classifies a message as general conversation (not calculation-related), it routes directly to the Response Generator with a conversational payload, bypassing the Parser and Calculator Engine.
- If the Parser cannot extract a full calculation (e.g., missing operand), it returns a structured `ParseError`. The Conversation Engine uses this to ask a clarifying question instead of calling the Calculator Engine.
- If the Calculator Engine encounters an invalid operation (e.g., divide by zero), it returns a structured `CalculationError`, which flows to the Response Generator the same way a success result would.

## 4. Data Contracts Between Modules

All communication between modules uses plain structured data objects (dictionaries/records), never module-to-module method calls into internals, and never free-form strings once past the Parser.

### 4.1 Input Processor → Conversation Engine
```
NormalizedMessage {
  raw_text: str
  clean_text: str
  timestamp: str
}
```

### 4.2 Conversation Engine → Natural-Language Parser
```
ParseRequest {
  clean_text: str
  context_snapshot: ContextSnapshot   # last result, recent values, for reference resolution
}
```

### 4.3 Natural-Language Parser → Conversation Engine
```
StructuredCalculationRequest {
  operation: str            # e.g. "add", "subtract", "multiply", "divide"
  operands: list[float]
  reference_used: bool      # true if "it"/"that" was resolved via context
}

ParseError {
  reason: str                # e.g. "no_operation_found", "missing_operand"
  original_text: str
}
```

### 4.4 Conversation Engine → Calculator Engine
```
CalculationRequest {
  operation: str
  operands: list[float]
}
```

### 4.5 Calculator Engine → Conversation Engine / Context / History
```
CalculationResult {
  operation: str
  operands: list[float]
  value: float
  timestamp: str
}

CalculationError {
  operation: str
  operands: list[float]
  reason: str                # e.g. "division_by_zero", "unsupported_operation"
}
```

### 4.6 Conversation Engine → Response Generator
```
ResponsePayload {
  kind: str                  # "calculation_result" | "calculation_error" | "conversation" | "clarification_request"
  result: CalculationResult | None
  error: CalculationError | ParseError | None
  conversational_text: str | None
}
```

### 4.7 Application Interfaces ↔ Core
```
CoreRequest { raw_text: str, session_id: str }
CoreResponse { display_text: str, session_id: str }
```
This is the only contract the CLI and desktop apps are allowed to depend on — a single request/response pair into the core system.

## 5. Module Dependency Rules

Allowed dependency direction (arrow means "depends on"):

```
Application Interfaces → Core Facade
Core Facade → Conversation Engine
Conversation Engine → Natural-Language Parser, Conversation Context, Response Generator
Natural-Language Parser → Conversation Context (read-only, for reference resolution)
Calculator Engine → (nothing else in the system)
Response Generator → (nothing else in the system)
History Manager ← Conversation Engine (writes), Application Interfaces (optional read for "show history")
```

Explicit rules:

- The **Calculator Engine** has zero dependencies on any other module. It is a pure function layer: structured request in, structured result out.
- The **Response Generator** has zero dependencies on any other module besides the data contracts it receives. It never calls back into the Calculator Engine, Parser, or Context.
- The **Natural-Language Parser** may read from Conversation Context (to resolve "it"/"that") but never writes to it, and never calls the Calculator Engine or Response Generator directly.
- The **Conversation Engine** is the only module allowed to orchestrate calls across Parser, Calculator Engine, Context, History, and Response Generator. It acts as the coordinator so no two leaf modules need to know about each other.
- **Application Interfaces** depend only on a thin Core Facade (a single entry function such as `handle_message(CoreRequest) -> CoreResponse`). They never import the Parser, Calculator Engine, or Response Generator directly.
- No module listed above may import the Application Interfaces layer. This guarantees the core works headless and prevents circular dependencies, since dependencies only ever point "inward" toward Calculator Engine/Response Generator and never back out toward the interfaces.

This produces a strict layering:

```
Interfaces  →  Core Facade  →  Conversation Engine  →  { Parser, Context, History, Response Generator }  →  Calculator Engine
```

No arrow ever points right-to-left, so circular dependencies are structurally prevented.

## 6. Initial Interface Definitions (Pseudocode)

```python
# input_processor.py
def process_input(raw_text: str) -> NormalizedMessage:
    ...

# nl_parser.py
def parse(request: ParseRequest) -> StructuredCalculationRequest | ParseError:
    ...

# calculator_engine.py
def calculate(request: CalculationRequest) -> CalculationResult | CalculationError:
    ...

# conversation_context.py
class ConversationContext:
    def get_snapshot(self) -> ContextSnapshot: ...
    def update(self, result: CalculationResult) -> None: ...

# response_generator.py
def generate_response(payload: ResponsePayload) -> str:
    ...

# history_manager.py
class HistoryManager:
    def record(self, result: CalculationResult) -> None: ...
    def recent(self, limit: int = 10) -> list[CalculationResult]: ...

# conversation_engine.py
class ConversationEngine:
    def handle(self, message: NormalizedMessage) -> ResponsePayload: ...

# core_facade.py
def handle_message(request: CoreRequest) -> CoreResponse:
    ...
```

Each function/class above is independently testable: the Calculator Engine can be tested with plain dictionaries/records and no mocks; the Response Generator can be tested by feeding it hand-built `ResponsePayload` objects; the Parser can be tested with fixed `ParseRequest` inputs without any live conversation running.

## 7. Architecture Decision Record — From-Scratch Conversational Approach

**Decision:** All natural-language understanding (intent detection, number/operation extraction) and all response phrasing will be implemented using hand-written rules, pattern matching, and lightweight local logic — not any pretrained model, transformer, LLM, cloud AI API, or third-party NLP/chatbot framework.

**Rationale:**
- The project must run fully offline and be CPU-friendly; pretrained language models and cloud APIs are incompatible with that constraint by nature.
- Keeping the Parser and Response Generator rule-based makes their behavior fully predictable and testable — a requirement for independent unit testing of every module.
- A from-scratch approach keeps the Calculator Engine and Parser free of any hidden dependency on a heavyweight runtime or network access, satisfying the "core processing must work without internet access" requirement.

**Consequences:**
- The Parser's vocabulary of recognized operation phrases (e.g., "add", "plus", "sum of") must be maintained and extended manually as new phrasing needs surface.
- Ambiguous or highly varied phrasing will sometimes fall through to a `ParseError`, which the Conversation Engine turns into a clarification request rather than a guess — an intentional tradeoff for predictability over coverage.
- The Response Generator's friendliness comes from templated/rule-based phrasing rather than generative text, which keeps output deterministic and easy to test.

## 8. Summary Against Acceptance Criteria

- All core modules are documented with a single responsibility each (Section 2).
- Input and output data for each module are defined as structured contracts (Section 4).
- The end-to-end processing flow, including branch cases, is documented (Section 3).
- Calculator logic is fully separated from conversational logic; the Calculator Engine has no dependency on the Conversation Engine or Response Generator (Section 5).
- Core modules do not depend on CLI or desktop interfaces; dependencies point strictly inward (Section 5).
- Circular dependencies are structurally prevented by the one-directional layering (Section 5).
- The architecture supports independent unit testing per module (Section 6).
- Scratch-development restrictions and the reasoning behind them are captured in the ADR (Section 7).
