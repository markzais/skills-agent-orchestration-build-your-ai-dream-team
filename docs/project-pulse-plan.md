# Project Pulse implementation plan

## Goal

Build Mona's Project Pulse as a lightweight, polished static dashboard for
contributors. The first view should make active projects easy to scan by
showing each project's name, owner, status, recent activity, priority or risk,
and a short contributor-friendly summary. The dashboard must run from
`app/index.html` rather than showing a server directory listing.

## Team responsibilities

### Orchestrator

- Turn this plan into ordered work phases and keep file ownership explicit.
- Delegate experience and accessibility decisions to Designer.
- Delegate implementation and runnable-app configuration to Coder.
- Resolve integration issues between the design guidance, data shape, markup,
  styles, and launch configuration.
- Review the complete result and report validation and remaining limitations.

### Planner

- Research the repository brief, existing conventions, agent definitions, and
  validation checks before implementation.
- Define dependencies, edge cases, file ownership, and validation expectations.
- Keep the plan aligned with the requested static HTML, CSS, and JSON
  deliverables.

### Designer

- Define the information hierarchy and responsive layout for a contributor
  friendly dashboard.
- Specify accessible semantic markup, readable contrast, keyboard-friendly
  interactions, status and priority treatments, and responsive behavior.
- Implement or guide the visual styling in `app/styles.css`, including a
  polished dashboard layout, visible project cards, status badges, readable
  spacing, rounded corners, shadows, and clear typography.
- Keep deterministic hooks such as `.dashboard` and `.project-card` available
  for integration and validation.

### Coder

- Create `app/index.html` with the exact title **Project Pulse**, a semantic
  dashboard structure, a reference to `styles.css`, and a reference to
  `project-data.json`.
- Load the top-level `projects` array and render visible cards using the
  `project-card` class. Each card must show `name`, `owner`, `status`,
  `recentActivity`, and `priority`.
- Create valid `app/project-data.json` with contributor-friendly project
  records.
- Create strict JSON at `.vscode/launch.json` with the **Run Project Pulse
  Dashboard** configuration, serving from the `app` directory with
  `python3 -m http.server 5500` and opening
  `http://localhost:%s/index.html`.
- Keep the implementation deterministic, understandable, and easy to preview
  from a Codespace.

## File assignments

| File | Owner | Responsibility | Dependencies |
| --- | --- | --- | --- |
| `app/styles.css` | Designer | Responsive visual system, dashboard layout, project cards, badges, spacing, contrast, and polished styling. | Design decisions; stable class hooks from the HTML contract. |
| `app/project-data.json` | Coder | Valid top-level `projects` array with the required project fields and representative dashboard content. | Data shape agreed before HTML rendering is finalized. |
| `app/index.html` | Coder, with Designer review | Semantic shell, title, data loading, project-card rendering, status/activity/priority presentation, and accessibility attributes. | Data schema and Designer's information hierarchy; must reference `styles.css` and `project-data.json`. |
| `.vscode/launch.json` | Coder | Strict JSON launch configuration named **Run Project Pulse Dashboard** that serves `app/` and opens `index.html`. | Final app path and port decision; independent of visual styling. |

## Ordered implementation phases

1. **Confirm the contract.** Orchestrator and Planner confirm the required
   fields, selectors, launch command, target URL, accessibility expectations,
   and file ownership from the brief and this plan.
2. **Set the experience direction.** Designer defines the information
   hierarchy, responsive layout, visual tokens, status/priority treatments,
   and accessibility guidance. Designer owns `app/styles.css`.
3. **Create the data and runtime configuration.** Coder creates
   `app/project-data.json` and `.vscode/launch.json`, preserving the required
   schema and preview behavior.
4. **Build the page integration.** Coder creates `app/index.html` using the
   agreed data contract and Designer's class and interaction guidance. The
   page renders cards from the project data and shows all required fields.
5. **Integrate and review.** Orchestrator checks that the HTML hooks match the
   CSS, data loads correctly, the launch target opens `index.html`, and the
   visual result meets the Project Pulse brief.
6. **Validate and hand off.** Orchestrator runs the checks below, records
   limitations or follow-up work, and produces the final handoff.

## Dependencies

- The `projects` schema must be agreed before `app/index.html` depends on it.
- Designer's class and layout contract must be available before the final HTML
  and CSS integration review.
- `app/index.html` depends on both `app/styles.css` and
  `app/project-data.json`; it must not assume a directory listing or hard-code
  data that belongs in JSON.
- `.vscode/launch.json` depends on the final `app/` path and must target
  `index.html`, but it does not depend on the CSS implementation.
- The final review depends on all four assigned files being present and on the
  data, markup, styles, and launch settings being consistent.

## Parallel work decisions

After the contract is confirmed, Designer can work on the styling and
accessibility direction in `app/styles.css` while Coder works on
`app/project-data.json` and `.vscode/launch.json`; these scopes do not overlap.
The Orchestrator should keep those tasks parallel to reduce waiting.

Creating the final `app/index.html` and integrating the card hooks should
follow the data contract and Designer's layout decisions, so that work is
sequential with respect to those inputs. The final integration review and
runtime validation must also happen after all assigned files exist. Any fixes
to shared markup/CSS contracts should be handled sequentially by the
Orchestrator to avoid conflicting edits.

## Validation expectations

- Confirm `docs/project-pulse-plan.md` and every assigned file exist.
- Parse `app/project-data.json` and `.vscode/launch.json` as strict JSON.
- Verify the data has a top-level `projects` array and every project includes
  `name`, `owner`, `status`, `recentActivity`, and `priority`.
- Inspect `app/index.html` for the exact **Project Pulse** title, a
  `styles.css` reference, a `project-data.json` reference, visible
  `project-card` elements, and rendering of status, recent activity, and
  priority.
- Inspect `app/styles.css` for `.dashboard`, `.project-card`,
  `border-radius`, `box-shadow`, readable contrast, and responsive layout
  rules.
- Inspect `.vscode/launch.json` for **Run Project Pulse Dashboard**, the
  `app` working directory, `python3 -m http.server 5500`, and a
  `serverReadyAction` URL ending in `/index.html`.
- Run the repository validation script and address failures that relate to the
  learner deliverables.
- Start the launch configuration in the Codespace and confirm the browser
  opens the Project Pulse UI at `index.html`, not the server directory.
- Check narrow-screen behavior, keyboard/focus visibility, semantic headings,
  and status/priority readability during the browser review.

## Edge cases and risks

- Malformed or missing JSON must produce a visible, actionable error rather
  than a blank dashboard.
- Missing project fields should not silently create misleading cards; the
  implementation should either validate the data or present a clear fallback.
- Status and priority values should remain visually distinguishable without
  relying on color alone.
- The launch URL must include `index.html`; opening only the server root risks
  displaying a directory listing.
- The layout must remain readable when project names or activity summaries are
  longer than the sample content and when the viewport is narrow.

## Open questions

- Whether future versions need filtering, sorting, or live data is outside the
  current static-dashboard scope. Do not add those features unless the
  Orchestrator receives a new requirement.
- The initial project records and exact visual palette may be chosen by Coder
  and Designer as long as they satisfy the brief and accessibility checks.
