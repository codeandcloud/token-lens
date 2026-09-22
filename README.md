# TokenLens

**TokenLens** is a Windows desktop application for tracking, consolidating, and analyzing usage across AI coding assistants.

The goal is to provide a single local dashboard for understanding how tools such as **OpenAI Codex**, **Claude Code**, **Google Gemini**, and **GitHub Copilot** are being used during software development.

> Repository: `agent-token-analytics`
> Application: **TokenLens**

## Why TokenLens?

Developers increasingly work with multiple AI coding assistants, but usage information is usually scattered across different tools, CLIs, dashboards, logs, and providers.

TokenLens aims to bring that information together in one place.

It is intended to help answer questions such as:

* How many tokens am I using?
* Which AI coding assistant am I using the most?
* Which models consume the most tokens?
* How much of the usage is input vs. output?
* How much cached-token usage is occurring?
* How does usage change over time?
* How much does each provider or model cost?
* Which development sessions consume the most AI resources?

## Supported Providers

The initial goal is to support:

* OpenAI Codex
* Anthropic Claude Code
* Google Gemini
* GitHub Copilot

Provider support will depend on what usage information each tool exposes through local logs, APIs, CLI output, telemetry, or other accessible sources.

## Planned Metrics

Where supported by the provider, TokenLens will capture information such as:

* Provider
* Model
* Agent or tool
* Session
* Input tokens
* Output tokens
* Cached input tokens
* Total tokens
* Estimated cost
* Request count
* Timestamp
* Usage duration

Not every provider exposes every metric, so TokenLens will normalize the available data while preserving provider-specific information where useful.

## Planned Features

### Unified Dashboard

View usage from all supported AI coding assistants in one place.

### Usage Analytics

Analyze token consumption by:

* Provider
* Model
* Day
* Week
* Month
* Session

### Cost Estimation

Estimate usage cost using provider and model pricing where applicable.

### Session Analysis

Identify individual development sessions and understand how AI usage is distributed across them.

### Historical Trends

Visualize token consumption and AI coding-assistant usage over time.

### Provider Adapters

Use a provider-based architecture so additional AI tools can be integrated without changing the core application.

### Local-First

TokenLens is intended to keep collected usage information locally wherever possible.

## High-Level Architecture

The application is planned around a provider-adapter model.

```text
Codex ───────────┐
Claude Code ─────┤
Gemini ──────────┼──> Provider Adapters
GitHub Copilot ──┘          │
                            ▼
                    Normalized Usage Data
                            │
                            ▼
                       Local Storage
                            │
                            ▼
                     Analytics Engine
                            │
                            ▼
                    TokenLens Dashboard
```

Each provider adapter is responsible for discovering and translating provider-specific usage information into a common TokenLens model.

## Proposed Solution Structure

```text
TokenLens.sln

src/
├── TokenLens.App
├── TokenLens.Core
└── TokenLens.Infrastructure

tests/
└── TokenLens.Tests
```

### TokenLens.App

Windows desktop UI and application composition.

### TokenLens.Core

Core domain models, interfaces, analytics logic, and provider abstractions.

### TokenLens.Infrastructure

Provider integrations, local data collection, persistence, external APIs, and operating-system integration.

### TokenLens.Tests

Unit and integration tests.

## Example Usage Model

A normalized usage record may eventually resemble:

```text
Provider        OpenAI
Agent           Codex
Model           gpt-5.x
Session         abc123
Input Tokens    12,450
Output Tokens   3,280
Cached Tokens   8,100
Total Tokens    15,730
Estimated Cost  ...
Timestamp       ...
```

The exact model will evolve as the capabilities of each provider are investigated.

## Technology

TokenLens is being designed as a Windows application using the **.NET ecosystem**.

The exact UI framework, storage engine, and integration mechanisms will be documented as the project architecture is finalized.

## Project Status

🚧 **Early development / research phase**

Current work includes:

* Investigating token and usage data exposed by each AI coding assistant
* Defining the normalized usage model
* Designing the provider-adapter architecture
* Determining the Windows application architecture
* Evaluating local persistence and analytics requirements

## Principles

TokenLens will aim to follow a few core principles:

**Local-first**
Usage data should remain on the developer's machine unless an external API is explicitly required.

**Provider-neutral**
The core analytics model should not depend on a single AI provider.

**Extensible**
Adding another AI coding assistant should primarily involve implementing a new provider adapter.

**Transparent**
Token counts, estimates, and unavailable metrics should be clearly distinguished.

**Developer-focused**
The application should provide useful information without adding significant overhead to the development workflow.

## Roadmap

Initial milestones:

1. Define the TokenLens domain model
2. Investigate Codex usage sources
3. Investigate Claude Code usage sources
4. Investigate Gemini usage sources
5. Investigate GitHub Copilot usage sources
6. Build provider adapter interfaces
7. Implement local persistence
8. Build the Windows dashboard
9. Add usage charts and filtering
10. Add cost estimation
11. Add export and reporting capabilities

## Contributing

TokenLens is currently in its early stages.

Contribution guidelines will be added as the architecture and initial implementation stabilize.

## License

License information will be added to the repository.

---

**TokenLens** — one view of your AI coding-assistant usage.

