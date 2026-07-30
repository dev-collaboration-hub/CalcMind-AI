# CalcMind AI — Project Milestones

CalcMind AI is a lightweight, offline, CPU-friendly conversational calculator for simple everyday calculations. It is not a scientific calculator.

## M1 — Project Foundation

Establish the initial project structure, standards, and development workflow.

### Tasks

- Create the source, test, documentation, and example directories
- Define module boundaries and naming conventions
- Add basic configuration files
- Add error-handling conventions
- Set up unit testing
- Add contribution guidelines

### Deliverable

A clean and maintainable foundation for future development.

---

## M2 — Basic Calculation Engine

Build the core calculator engine for simple arithmetic.

### Tasks

- Addition
- Subtraction
- Multiplication
- Division
- Decimal number support
- Negative number support
- Division-by-zero handling
- Safe numeric validation
- Clear result formatting

### Deliverable

A reliable offline engine for basic calculations.

---

## M3 — Conversational AI Engine

Build the lightweight offline system that allows users to communicate naturally with the calculator.

### Tasks

- Accept normal English messages
- Respond in a clear and friendly style
- Handle greetings and basic calculator-related conversation
- Ask for missing values when a request is incomplete
- Handle unclear or unsupported requests politely
- Keep responses focused on simple calculations
- Operate without cloud APIs

### Example

```text
User: Hello
AI: Hello! What would you like me to calculate?

User: I bought 4 items for 250 rupees each.
AI: The total cost is 1,000 rupees.
```

### Deliverable

A lightweight conversational layer that communicates naturally with the user.

---

## M4 — Natural Language Calculation Parser

Convert normal user messages into structured calculator operations.

### Tasks

- Detect numbers in sentences
- Detect calculation intent
- Recognize addition, subtraction, multiplication, and division phrases
- Understand phrases such as add, remove, total, double, half, and divide
- Convert messages into structured calculator commands
- Detect incomplete or invalid requests
- Connect parsed commands to the calculation engine

### Examples

```text
Add 25 and 40
Subtract 15 from 100
Multiply 12 by 8
Divide 500 by 5
```

### Deliverable

A lightweight parser that connects conversational input with the calculator engine.

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

### Deliverable

A practical calculator for common everyday needs.

---

## M6 — Conversation Memory and History

Allow the AI to understand connected follow-up calculations.

### Tasks

- Remember the previous result
- Understand words such as it, that, and the result
- Support multi-step calculations
- Store recent calculation history locally
- Provide a history command
- Clear the current conversation
- Clear saved calculation history
- Keep all conversation data offline

### Example

```text
User: What is 20 percent of 5,000?
AI: 20 percent of 5,000 is 1,000.

User: Add it to 5,000.
AI: The final result is 6,000.
```

### Deliverable

A conversational calculator that can handle connected, multi-step requests.

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
- Send, clear, and reset controls
- Copy-result option
- Keyboard shortcuts
- Light and dark themes
- Responsive desktop window

### Deliverable

A lightweight desktop conversational calculator application.

---

## M9 — Testing and CPU Optimization

Improve reliability, safety, speed, and resource usage.

### Tasks

- Unit tests for calculator operations
- Natural-language parser tests
- Conversation-flow tests
- Memory and history tests
- Invalid-input tests
- Large-number tests
- Performance benchmarks
- CPU usage optimization
- Memory usage optimization
- Cross-platform testing

### Deliverable

A stable, fast, and CPU-friendly calculator AI.

---

## M10 — Documentation and Version 1.0

Prepare CalcMind AI for its first public release.

### Tasks

- Complete user documentation
- Add developer documentation
- Add installation instructions
- Add usage examples
- Document the architecture
- Add troubleshooting guidance
- Prepare release notes
- Package the application
- Publish Version 1.0

### Deliverable

A documented and release-ready first version of CalcMind AI.

---

## Project Scope

CalcMind AI focuses only on simple and everyday calculations. It will not include scientific calculator features such as trigonometry, logarithms, matrices, calculus, or complex algebra.
