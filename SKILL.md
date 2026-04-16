---
name: complete-lab-report
description: Use when the task is to complete or deliver a university lab report or experiment report from plain-text requirements, a Word/docx template, an existing codebase, or a compressed submission package. Trigger on requests such as “完成实验报告”, “根据模板补全文档”, “保留原格式填写”, “预留截图位置”, “没有代码也要完成实验”, or “complete a lab report from requirements and template”.
---

# Complete Lab Report

## Overview

Complete university experiment reports from requirements, templates, and optional project files. Inspect existing artifacts first, preserve template structure when possible, and leave explicit placeholders for any content that cannot be verified.

## Trigger Cues

Use this skill when the user wants a near-submit-ready experiment report and the task involves one or more of the following:

- A `.docx` template that must be filled without breaking layout.
- Plain-text experiment requirements that need to become a formal report.
- Missing or incomplete code that must be supplemented before the report can be written.
- Screenshot placeholders or screenshot guidance for runtime evidence.
- Packaged coursework such as source archives, report templates, and prior examples.

Typical phrases:

- “根据这个 docx 要求完成实验报告”
- “不要破坏原格式，直接补全文档”
- “没有代码也帮我完成实验并写报告”
- “把截图位置先留出来，并告诉我要截什么”
- “complete the lab report from the template”

## Inputs And Outputs

Supported inputs:

- Plain text task requirements
- Existing `.docx` report templates
- Existing repository contents
- Compressed source packages
- Prior report examples or supporting notes

Default output priority:

1. Completed `.docx`
2. `pdf` when explicitly requested or when downstream conversion is required
3. `md` or plain text when no `docx` workflow exists or the user explicitly asks for it

If the user provides a template, preserve its structure and formatting unless the task explicitly allows redesign.

## Workflow

### 1. Inspect Before Asking

- Inspect the workspace and provided artifacts before asking questions.
- If a `.docx` exists, extract its paragraphs, tables, headings, and fillable sections first.
- If source code exists, inspect the repo and infer the technology stack before asking about it.
- If the task includes compressed files, inspect their contents before deciding what is missing.

Use:

- `scripts/extract_docx_structure.py` to inspect paragraph and table structure
- `scripts/inspect_docx_targets.py` to identify likely fillable sections and placeholders

### 2. Separate Facts From Preferences

Classify unknowns into two groups:

- Discoverable facts: report sections, technology stack, existing code layout, template instructions
- User-supplied facts: student identity fields, class info, teacher, exact submission metadata, screenshots, runtime evidence, grades, signatures

Do not ask about anything that can be discovered locally.

### 3. Ask In Stages

Ask only after inspection, and ask in the smallest useful batch.

Order of questions:

1. Output-blocking identity fields if they are required on the cover page
2. Technology stack only when code must be written and the stack cannot be inferred locally
3. Evidence-dependent items such as screenshots or runtime results after the draft is materially complete

Do not front-load every question. If a placeholder is acceptable, write the draft first and ask only for the missing evidence.

### 3.1 Reusing Known Identity Fields

If a persistent memory file such as `~/.codex/memories/PROFILE.md` already contains stable lab-report identity fields, prefer reusing them instead of asking from scratch every time.

Use this rule:

1. On the first use, if the required identity fields are missing from memory, ask for the minimum blocking set such as student name, student number, class, and major.
2. On later uses, if those fields already exist in memory, show them back to the user briefly and ask whether this report should use the previously stored values.
3. Only overwrite stored identity facts when the user explicitly corrects or updates them.
4. Keep grades, signatures, screenshots, and submission-specific metadata out of long-term memory unless the user explicitly asks to store them.

See `references/question-policy.md`.

### 4. Generate The Needed Artifacts

When writing the report:

- Reuse the user’s existing structure and headings when possible.
- Fill the standard sections using concrete, implementation-backed prose rather than generic filler.
- If code is required, either:
  - infer the stack from the repo and implement the minimum working solution, or
  - ask the user for the stack first when it is not discoverable.
- Keep unverifiable facts as placeholders with explicit labels.
- If screenshots are required, reserve insertion points inside the report and provide screenshot capture guidance in chat.

For common section guidance, see `references/section-playbook.md`.

### 5. Truthfulness And Placeholder Policy

Never fabricate:

- Screenshots
- Runtime outputs that were not observed
- Student identity fields
- Teacher signatures, grades, review comments
- Claims that the program ran successfully if it was not checked

Instead:

- leave a visible placeholder in the document
- explain what evidence is still needed
- provide a screenshot checklist when relevant

Recommended placeholder patterns:

- `【待补：学生姓名】`
- `【截图预留1：依赖安装成功界面】`
- `【待确认：运行结果】`

### 6. Verify Before Finalizing

Before claiming the report is complete:

- inspect the final document structure again
- check whether template instructions or red guidance text remain
- check whether target sections are still blank
- confirm placeholders are only present where verification is impossible or the user has not supplied the data

Use `scripts/check_report_completeness.py` for the basic checks.

## Code Generation Rules

- If code is needed and the stack is discoverable from files such as `requirements.txt`, `package.json`, `pom.xml`, `pyproject.toml`, or existing source layout, infer the stack and proceed.
- If code is needed and the stack is not discoverable, stop and ask for the stack before generating implementation-specific code.
- Prefer the minimum runnable implementation that satisfies the written requirements.
- Write the report from what the implementation actually does, not from a generic imagined solution.

## Screenshot Guidance Rules

When screenshots are needed:

- reserve concrete insertion points in the report
- number them in the order the user should capture them
- describe exactly what each screenshot should show
- include both terminal and UI screenshots when the task includes setup plus runtime behavior

Example sequence:

1. Virtual environment creation and dependency installation
2. Initial page or program startup screen
3. Validation failure or exception-handling state
4. Successful final result

## Real Workflow Examples

Example 1:

- Read the `.docx` template
- Identify cover fields, standard report sections, and blank tables
- Fill the report content without breaking layout
- Preserve screenshot placeholders inside the report
- Output screenshot instructions in chat

Example 2:

- Read plain-text experiment requirements
- Inspect the repo for code and infer the stack
- If no stack is inferable and code is required, ask the user which stack to use
- Implement the smallest working solution
- Write the experiment process, issues, and summary around the real implementation

## Verification Checklist

- Template structure inspected before editing
- Required sections filled or intentionally marked pending
- No fabricated evidence
- No leftover template instructions unless intentionally preserved
- Output format matches user request or default policy
- Screenshot checklist provided when screenshots are required

## Resources

- `references/section-playbook.md`: common experiment-report section patterns and boundaries
- `references/question-policy.md`: staged questioning rules
- `references/test-scenarios.md`: baseline prompts and forward-test expectations
- `scripts/extract_docx_structure.py`: structured `.docx` inspection
- `scripts/inspect_docx_targets.py`: heading/table/fill-target discovery
- `scripts/check_report_completeness.py`: basic report completeness checks
