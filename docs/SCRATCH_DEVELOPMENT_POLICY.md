# CalcMind AI — Scratch Development Policy

## Purpose

CalcMind AI is intended to be a genuinely lightweight conversational calculator whose complete core intelligence is created within this repository.

The project is not a wrapper around an existing chatbot, pretrained model, cloud service or third-party calculation engine.

## Core Requirement

All core product logic must be designed, implemented, tested and documented by CalcMind AI contributors.

This rule applies to the calculator and to the AI.

## Components That Must Be Built From Scratch

The following components must be implemented inside this repository:

1. Basic arithmetic engine
2. Numeric validation and result formatting
3. Text normalization
4. Tokenization required by the calculator domain
5. Number extraction
6. Operation extraction
7. Intent detection
8. Natural-language calculation parsing
9. Conversation routing
10. Greeting and calculator-dialogue handling
11. Missing-information detection
12. Clarification-response logic
13. Conversation context
14. Previous-result references
15. Calculation history
16. Response generation
17. Error handling
18. Command-line interaction
19. Desktop application behavior
20. Tests and performance benchmarks

## Prohibited Approaches

Contributors must not use the following to implement the core intelligence:

- Cloud AI APIs
- Remote inference services
- Hosted chatbot services
- Pretrained language models
- Downloaded local LLMs
- Transformer models
- External chatbot engines
- Third-party intent-detection engines
- Third-party NLP pipelines
- External vector databases
- Online conversation-memory services
- Libraries that silently perform the main calculation or language-understanding work
- Wrappers that merely forward user messages to another AI system

Examples of prohibited dependency categories include hosted LLM SDKs, pretrained transformer pipelines and general-purpose chatbot frameworks.

## Permitted Design Techniques

CalcMind AI may use techniques implemented directly by project contributors, including:

- Rule-based tokenization
- Pattern matching
- Keyword and phrase dictionaries
- Handwritten grammar rules
- Intent scoring
- Finite-state conversation flows
- Deterministic context tracking
- Domain-specific response templates
- Project-owned arithmetic algorithms
- Local file-based history

These techniques must remain understandable, testable and documented.

## Dependency Policy

The runtime should remain minimal.

- Prefer the programming language standard library.
- Core intelligence must not depend on third-party AI or NLP packages.
- A dependency must not replace a component that the project is expected to build.
- Development or testing tools may be considered separately, but they must not provide the product's calculator or conversational intelligence.
- Any proposed runtime dependency requires explicit maintainer approval and documentation explaining why it does not violate this policy.

## Offline Requirement

After installation, CalcMind AI must perform its supported calculations and conversations without an internet connection.

The application must not:

- Send user messages to an external server
- Download a model during runtime
- Require an API key
- Require a cloud account
- Depend on remote storage for conversation history

## CPU and Resource Requirement

The system must be suitable for ordinary CPU-based computers.

Contributors should prefer:

- Small data structures
- Deterministic algorithms
- Fast startup
- Low memory usage
- No GPU requirement
- No background model downloads
- No heavyweight inference runtime

## Explainability Requirement

For every supported request, developers should be able to trace:

1. How the text was normalized
2. Which intent was detected
3. Which numbers and operations were extracted
4. Which calculator function was called
5. How conversation context affected the request
6. How the final response was produced

The system should never behave like an unexplained black box.

## Contribution Review Checklist

A contribution should be rejected or revised when it:

- Introduces an external AI model
- Calls a cloud AI API
- Uses a third-party NLP engine for core parsing
- Replaces project-owned logic with a wrapper
- Adds unnecessary heavyweight dependencies
- Requires internet access for normal operation
- Makes the AI behavior difficult to explain or test
- Expands the project into a scientific calculator

A contribution is aligned with the project when it:

- Implements focused functionality directly
- Keeps the code understandable
- Includes tests
- Preserves offline execution
- Preserves CPU-friendly operation
- Improves the scratch-built conversational calculator architecture

## Final Standard

CalcMind AI must remain a simple conversational calculator built from the ground up.

Its value comes from owning and understanding the complete system: input processing, conversation logic, calculation, memory and response generation.