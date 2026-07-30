# CalcMind AI — Project Milestones

CalcMind AI is a lightweight, offline, CPU-friendly conversational calculator for simple everyday calculations. It is not a scientific calculator.

## Mandatory Development Requirement

Every core component in this roadmap must be built from scratch inside the CalcMind AI repository.

This includes:

- Calculator engine
- Conversational AI engine
- Natural-language parser
- Intent detection
- Number and operation extraction
- Conversation context
- Memory and history
- Response generation
- Validation and error handling
- Command-line and desktop application logic

The project must not use cloud AI APIs, pretrained language models, downloaded AI models, external LLMs, transformer models, chatbot frameworks or third-party NLP engines for its core intelligence.

The AI must remain lightweight, explainable, offline and suitable for ordinary CPUs.

See [Scratch Development Policy](docs/SCRATCH_DEVELOPMENT_POLICY.md).

---

## M1 — Project Foundation

Establish the initial project structure, standards and scratch-development workflow.

### Tasks

- Create the source, test, documentation and example directories
- Define module boundaries and naming conventions
- Define the scratch-development rules
- Add dependency restrictions
- Add basic configuration files
- Add error-handling conventions
- Set up unit testing
- Add contribution guidelines
- Document prohibited external AI dependencies

### Deliverable

A clean and maintainable project foundation that enforces from-scratch implementation.

---

## M2 — Basic Calculation Engine

Build the core calculator engine from scratch for simple arithmetic.

### Tasks

- Implement addition
- Implement subtraction
- Implement multiplication
- Implement division
- Add decimal number support
- Add negative number support
- Handle division by zero
- Implement safe numeric validation
- Implement clear result formatting
- Avoid external calculation engines

### Deliverable

A reliable, independently implemented offline engine for basic calculations.

---

## M3 — Conversational AI Engine From Scratch

Build the lightweight offline AI system that allows users to communicate naturally with the calculator.

### Tasks

- Design the conversational architecture from scratch
- Implement message preprocessing from scratch
- Implement lightweight tokenization from scratch
- Implement greeting and conversation-intent recognition
- Implement calculator-related dialogue rules
- Generate clear and friendly responses
- Ask for missing values when a request is incomplete
- Handle unclear or unsupported requests politely
- Keep responses focused on simple calculations
- Keep the system deterministic and explainable
- Operate without cloud APIs
- Operate without pretrained or downloaded AI models
- Avoid external LLM, transformer, chatbot and NLP frameworks

### Example

```text
User: Hello
AI: Hello! What would you like me to calculate?

User: I bought 4 items for 250 rupees each.
AI: The total cost is 1,000 rupees.
```

### Deliverable

A scratch-built conversational AI layer that communicates naturally without depending on an external AI model.

---

## M4 — Natural Language Calculation Parser From Scratch

Convert normal user messages into structured calculator operations using project-owned parsing logic.

### Tasks

- Implement text normalization
- Detect numbers in sentences
- Detect calculation intent
- Recognize addition, subtraction, multiplication and division phrases
- Understand phrases such as add, remove, total, double, half and divide
- Map language patterns to structured calculator commands
- Detect incomplete or invalid requests
- Connect parsed commands to the calculation engine
- Add confidence scoring for supported intents
- Add tests for ambiguous messages
- Avoid third-party NLP parsers and pretrained models

### Examples

```text
Add 25 and 40
Subtract 15 from 100
Multiply 12 by 8
Divide 500 by 5
```

### Deliverable

A lightweight natural-language parser designed and implemented completely within CalcMind AI.

---

## M5 — Everyday Calculation Features

Add common daily-use calculations while keeping the project simple.

### Tasks

- Percentage calculations
- Discount calculations
- Profit and loss calculations
- Average calculation
- Bill splitting
- Price increase and decrease
- Basic money calculations
- Simple tax calculations
- Natural-language patterns for each supported feature

### Deliverable

A practical calculator for common everyday needs.

---

## M6 — Conversation Memory and History

Build local conversation context and history from scratch so the AI can understand connected follow-up calculations.

### Tasks

- Design a lightweight conversation-state structure
- Remember the previous result
- Remember recent supported intents and values
- Understand references such as it, that and the result
- Support multi-step calculations
- Store recent calculation history locally
- Provide a history command
- Clear the current conversation
- Clear saved calculation history
- Keep all conversation data offline
- Do not use external vector databases or memory services

### Example

```text
User: What is 20 percent of 5,000?
AI: 20 percent of 5,000 is 1,000.

User: Add it to 5,000.
AI: The final result is 6,000.
```

### Deliverable

A scratch-built memory system that supports connected, multi-step calculator conversations.

---

## M7 — Command-Line Chat Application

Create the first complete user interface for CalcMind AI.

### Tasks

- Interactive terminal conversation
- Friendly startup message
- Calculation input prompt
- History command
- Reset command
- Clear-screen command
- Exit command
- Helpful error messages
- Fully offline execution
- Connect all scratch-built AI and calculator components

### Deliverable

A complete and usable command-line conversational calculator.

---

## M8 — Lightweight Desktop Interface

Build a simple graphical interface for general users.

### Tasks

- Chat-style message area
- User input field
- Result display
- Calculation history panel
- Send, clear and reset controls
- Copy-result option
- Keyboard shortcuts
- Light and dark themes
- Responsive desktop window
- Keep the interface lightweight and CPU-friendly

### Deliverable

A lightweight desktop conversational calculator application.

---

## M9 — Testing and CPU Optimization

Improve reliability, safety, speed and resource usage.

### Tasks

- Unit tests for calculator operations
- Natural-language parser tests
- Conversation-flow tests
- Memory and history tests
- Invalid-input tests
- Large-number tests
- Scratch-policy compliance tests
- Verify that no external AI service is required
- Verify that no pretrained model is bundled or downloaded
- Performance benchmarks
- CPU usage optimization
- Memory usage optimization
- Cross-platform testing

### Deliverable

A stable, fast and CPU-friendly calculator AI whose complete intelligence runs locally.

---

## M10 — Documentation and Version 1.0

Prepare CalcMind AI for its first public release.

### Tasks

- Complete user documentation
- Add developer documentation
- Add installation instructions
- Add usage examples
- Document the scratch-built architecture
- Explain how the conversational AI works
- Document every permitted and prohibited dependency
- Add troubleshooting guidance
- Prepare release notes
- Package the application
- Publish Version 1.0

### Deliverable

A documented and release-ready first version of CalcMind AI.

---

## Final Project Scope

CalcMind AI focuses only on simple and everyday calculations. It will not include scientific calculator features such as trigonometry, logarithms, matrices, calculus or complex algebra.

The project is intended to demonstrate how a small conversational AI system can be engineered from scratch for one focused domain without relying on cloud services, pretrained AI models or heavyweight external frameworks.