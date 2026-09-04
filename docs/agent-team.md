# Agent team

The Mona's Project Pulse dashboard will be built by a coordinated team of custom agents, orchestrated through GitHub Copilot CLI in a Codespace:

| Agent | Target model | Responsibility | Definition |
| --- | --- | --- | --- |
| **Orchestrator** | Claude Opus 4.7 (copilot) | Coordinates Planner, Coder, and Designer; breaks work into phases, manages dependencies and file ownership, and verifies the integrated result. | `.github/agents/orchestrator.agent.md` |
| **Planner** | Claude Opus 4.7 (copilot) | Researches the repository and relevant documentation, then creates implementation plans covering steps, dependencies, edge cases, and validation. | `.github/agents/planner.agent.md` |
| **Coder** | GPT-5.5 (copilot) | Implements the dashboard code within the assigned scope, follows repository patterns, and validates deterministic, runnable behavior. | `.github/agents/coder.agent.md` |
| **Designer** | Gemini 3.1 Pro (copilot) | Defines and implements UI/UX direction, accessibility, information hierarchy, responsive behavior, and polished Project Pulse styling. | `.github/agents/designer.agent.md` |

The Orchestrator will typically have the Planner establish the approach first, then coordinate the Designer and Coder in parallel where their file scopes are independent, integrating their work before reporting the final outcome.
