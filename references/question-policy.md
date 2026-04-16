# Question Policy

This skill should ask questions only after inspection and only when the answer cannot be derived locally.

## Order

### 1. Inspect First

Before asking:

- inspect `.docx` templates
- inspect repository files
- inspect compressed package contents when available
- infer likely stack and report structure

Do not ask the user for information that is already present in the workspace.

### 2. Ask Output-Blocking Questions

Ask these first only if they block a credible draft:

- required cover-page identity fields
- missing output format when no default can be applied safely
- technology stack when code must be written and cannot be inferred

### 3. Draft Before Evidence Questions

If screenshots, runtime evidence, or personal metadata are missing but the report can still be drafted:

- draft the report first
- leave placeholders in the document
- then ask or instruct the user what to provide

This keeps the workflow moving and avoids unnecessary early interruption.

## Tech Stack Rule

If implementation is required:

- infer the stack from local files whenever possible
- ask the user only when the stack is not discoverable and the implementation would otherwise be speculative

## Identity Rule

Identity or submission fields should not be guessed. If they are required and absent:

- leave placeholders, or
- ask the user if the document is ready for finalization

## Evidence Rule

Never fabricate screenshots, grades, signatures, or runtime results.

When evidence is missing:

- keep the report structurally complete
- label the missing evidence explicitly
- provide a concrete checklist for what the user should capture or supply
