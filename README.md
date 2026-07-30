# CalcMind AI

CalcMind AI is a lightweight, offline, CPU-friendly conversational calculator designed for simple everyday calculations.

It is **not a scientific calculator**. It focuses on basic arithmetic and practical daily-use calculations while allowing the user to communicate through normal English messages.

## Core Principle: Built Completely From Scratch

Every core part of CalcMind AI must be designed and implemented inside this repository.

This requirement includes the conversational AI itself.

### Mandatory Rules

- Build the calculator engine from scratch.
- Build the conversational AI engine from scratch.
- Build the natural-language parser from scratch.
- Build intent detection and number extraction from scratch.
- Build conversation context and memory from scratch.
- Build response-generation logic from scratch.
- Build validation, history, and error handling from scratch.
- Keep all processing offline and CPU-friendly.
- Do not use cloud AI services or remote inference APIs.
- Do not use pretrained language models or downloaded AI models.
- Do not use external LLMs, transformer models, or chatbot engines.
- Do not use third-party NLP systems to provide the core intelligence.
- Do not hide external AI functionality behind wrappers or SDKs.

The AI should be a small, deterministic and explainable system created specifically for calculator conversations. It may use project-owned rules, tokenization, pattern matching, intent scoring, context tracking and response templates, but those systems must be implemented by contributors within CalcMind AI.

See [Scratch Development Policy](docs/SCRATCH_DEVELOPMENT_POLICY.md) for the complete rules.

## Example

**User:**  
What is 18% of 4,500?

**AI:**  
18% of 4,500 is 810.

## Core Features

- Addition
- Subtraction
- Multiplication
- Division
- Percentage calculations
- Discount calculations
- Profit and loss calculations
- Bill splitting
- Average calculations
- Basic money calculations
- Natural-language calculation requests
- Friendly conversational responses
- Calculation history
- Conversation context
- Reuse of previous results

## Conversation Example

```text
User: Hello
AI: Hello! What would you like me to calculate?

User: Calculate 20% of 5,000.
AI: 20% of 5,000 is 1,000.

User: Add it to 5,000.
AI: The final result is 6,000.
```

## Basic Architecture

```text
User Message
      ↓
Scratch-Built Conversation Engine
      ↓
Scratch-Built Language Parser
      ↓
Intent and Number Extraction
      ↓
Basic Calculator Engine
      ↓
Conversation Context and Memory
      ↓
Scratch-Built Response Generator
```

All components run locally without internet access, cloud APIs or pretrained AI models.

## Project Milestones

1. M1 — Project Foundation
2. M2 — Basic Calculation Engine
3. M3 — Conversational AI Engine From Scratch
4. M4 — Natural Language Calculation Parser From Scratch
5. M5 — Everyday Calculation Features
6. M6 — Conversation Memory and History
7. M7 — Command-Line Chat Application
8. M8 — Lightweight Desktop Interface
9. M9 — Testing and CPU Optimization
10. M10 — Documentation and Version 1.0

See [MILESTONES.md](MILESTONES.md) for the complete roadmap.

## Project Scope

CalcMind AI will not include advanced scientific features such as:

- Trigonometry
- Logarithms
- Matrices
- Complex algebra
- Calculus
- Advanced equations

The goal is to build a simple, fast, private and user-friendly conversational calculator AI that is fully understandable, locally executable and developed from scratch.