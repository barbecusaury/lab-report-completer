# Test Scenarios

Use these scenarios to validate whether `complete-lab-report` actually changes agent behavior in the intended way.

## Baseline Prompts Without The Skill

Run these prompts without explicitly invoking the skill and record what the agent gets wrong.

### Scenario 1: Existing DOCX Template

Prompt:

`根据这个 docx 要求完成实验报告，不破坏原格式，截图位置先留着。`

Look for failures:

- edits before inspecting template structure
- ignores tables or cover-page fields
- rewrites formatting blindly
- leaves generic filler instead of concrete report prose
- forgets screenshot placeholders or guidance

### Scenario 2: Plain Text Requirements, No Code

Prompt:

`这里只有实验要求文字，没有代码，你帮我完成实验并写报告。`

Look for failures:

- writes a report without checking whether code is required
- invents a stack instead of asking or inspecting
- produces only explanation text rather than a delivery-oriented workflow
- fabricates runtime evidence

### Scenario 3: Template With Instructions

Prompt:

`模板里有红字说明和空白表格，帮我补全并告诉我要截哪些图。`

Look for failures:

- leaves template instructions in the final result
- does not distinguish user-supplied fields from discoverable content
- fails to convert generic “可贴图” wording into concrete screenshot placeholders

## Expected Behavior With The Skill

### Scenario 1: Existing DOCX Template

Expected behavior:

- inspect `.docx` structure first
- identify fillable cells, headings, and blank sections
- preserve layout and original section structure
- leave placeholders only for unverifiable content
- produce screenshot guidance in chat

### Scenario 2: Plain Text Requirements, No Code

Expected behavior:

- extract actual requirements first
- inspect workspace for existing code or stack clues
- ask for the stack only if implementation is required and cannot be inferred
- generate minimal implementation only when justified
- write report content from the real implementation or verified plan

### Scenario 3: Template With Instructions

Expected behavior:

- remove or replace template instructions during completion
- keep structure while replacing instructional text with report content
- reserve numbered screenshot placeholders
- tell the user exactly what to capture

## Acceptance Checklist

- The agent inspects before asking.
- The agent does not fabricate screenshots, grades, signatures, or unverified results.
- The agent preserves template structure when a template exists.
- The agent asks only for identity fields, stack, or evidence that cannot be inferred.
- The agent prioritizes `docx` unless the user explicitly requests another format.
- The agent can describe a complete delivery flow instead of only giving advice.

## Notes

If a validation run fails, update one of these:

- `SKILL.md` when the workflow or trigger guidance is unclear
- `references/question-policy.md` when the agent asks too much or too early
- `references/section-playbook.md` when section-writing guidance is too generic
- helper scripts when inspection or completeness checks are missing obvious targets
