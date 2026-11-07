---
description: "Survey the project and the latest feature, then report codebase condition, feature readiness and recent changes. Read-only. Optional argument sets a focus area."
---

## User Input

```text
$ARGUMENTS
```

The user input (if any) is a **focus hint**: a feature, module, directory or concern to examine more closely. If empty, give an even overview.

## Rules

- **Strictly read-only.** Do not create, edit or delete any file, and do not run builds that modify tracked files. Shell is allowed only for read-only git commands and listing.
- Do not ask questions; report what you find, and state assumptions explicitly.
- Prefer dedicated read/search tools over shell equivalents.

## Steps

1. **Map the project**
   - List the top-level structure and identify the main source directories, entry points, build/run tooling (README, Makefile, package manifests, etc.) and the tech stack.
   - Read README and any project-level docs/constitution (`.specify/memory/constitution.md`) for intent and constraints.
   - Skim the source files enough to understand architecture and module boundaries. If a focus hint was given, read the relevant files in depth, not just skim.

2. **Locate the latest feature**
   - If `specs/` does not exist or is empty: note that the project has no spec-driven features yet, skip to step 4 (still report codebase condition and recent changes).
   - Determine the "last feature" in this order:
     1. `feature_directory` in `.specify/feature.json` (if present and the directory exists),
     2. the highest-numbered directory in `specs/` (e.g. `002-modules`),
     3. the current git branch name if it matches a spec directory.
   - If these disagree, say so and treat the highest-numbered directory as the latest.

3. **Read the feature artifacts** (whichever exist): `spec.md`, `plan.md`, `tasks.md`, `data-model.md`, `research.md`, `quickstart.md`, `contracts/`, `checklists/`.
   - From `tasks.md`: count total vs completed (`[X]`/`[x]`) vs open tasks; list open tasks by phase.
   - From `checklists/`: count complete vs incomplete items.
   - From `spec.md`: list user stories / functional requirements and any `[NEEDS CLARIFICATION]` markers.
   - **Verify against the code, don't trust checkboxes**: for each major requirement/task, spot-check that the referenced files/symbols exist and do what the task says. Flag tasks marked done but not actually implemented, and implemented work that is not reflected in tasks.

4. **Recent changes**
   - `git log --oneline -n 15`, `git status --short`, and `git diff --stat` against the previous commit(s) as relevant. Summarize what changed recently and which feature each change belongs to. Mention uncommitted work separately.

5. **Report** to the user in this structure (concise, in the user's language):

   ```markdown
   ## Codebase condition
   Stack, architecture, structure, build/run status as far as it can be determined, notable risks, tech debt, inconsistencies.

   ## Latest feature: <directory name>
   Purpose in one or two sentences.
   - Artifacts present / missing
   - Tasks: X/Y done (Z open), checklists: A/B
   - **Readiness**: Not started | In progress | Implemented, needs verification | Ready  — with justification
   - Gaps: spec requirements without implementation, open clarifications, done-but-missing tasks

   ## Recent changes
   Bullet summary of the latest commits and any uncommitted work.

   ## Focus: <hint>   (only if a hint was given)
   Detailed findings for the requested area.

   ## Suggested next step
   One recommendation, e.g. continuing with `__SPECKIT_COMMAND_IMPLEMENT__`, or starting a new feature with `__SPECKIT_COMMAND_SPECIFY__ ...`.
   ```
