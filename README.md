# lab-report-completer

你是否也被重复、机械、耗时的实验报告折磨过？那就让 AI 去当牛马吧。

`lab-report-completer` is a reusable skill for turning templates, requirements, slides, and project files into near-submission-ready computer lab reports.

## Overview

This repository packages a skill focused on computer-related lab reports. It is designed for workflows where the user provides one or more of the following:

- a `.docx` report template
- experiment requirements in plain text
- slides, PDFs, or supporting notes
- an existing codebase or compressed project package
- runtime evidence that still needs screenshot placeholders

The skill is especially useful for courses such as:

- Web development
- Python programming
- Java programming
- Database experiments
- Software engineering practice

It can still be adapted to similar report-writing workflows in other technical courses.

## What It Does

- Inspects templates before asking questions
- Reuses the original document structure instead of rewriting it blindly
- Distinguishes discoverable facts from user-only facts
- Fills report sections with implementation-backed content instead of generic filler
- Leaves explicit placeholders for screenshots, signatures, grades, and unverifiable results
- Supports adapting to the user's actual school template, identity fields, and experiment process

## Key Principles

- Do not fabricate screenshots
- Do not fabricate runtime outputs that were not observed
- Do not fabricate student identity fields, signatures, or grading information
- Ask only for the minimum blocking information after inspecting available artifacts
- Prefer reusing stable identity fields that are already known, but confirm them before using them in a new report
- Update previously known identity facts only when the user explicitly corrects them

## Identity Reuse Rule

The public version of this skill uses a general rule for stable identity fields:

1. If reliable identity information is already known from prior context, reuse it only after asking the user to confirm it for the current report.
2. If the required identity fields are not known, ask only for the minimum blocking set, such as name, student number, class, and major.
3. Only overwrite stored or previously known identity facts when the user explicitly updates them.

This keeps the workflow efficient without hardcoding the rule to a specific local memory implementation.

## Repository Layout

```text
.
├── SKILL.md
├── README.md
├── agents/
├── references/
└── scripts/
```

- `SKILL.md`: the main skill definition
- `agents/`: agent-specific metadata
- `references/`: supporting guidance for report structure and questioning policy
- `scripts/`: utility scripts for inspecting and checking `.docx` reports

## Typical Use Cases

- Complete a lab report from a Word template without breaking formatting
- Generate a report from requirements plus an existing codebase
- Leave screenshot placeholders and tell the user what to capture
- Fill computer experiment reports with more truthful, evidence-based content
- Adapt the draft to a user's real course setup instead of producing generic boilerplate

## Notes

- The current focus is computer-related lab reports, but the workflow is intentionally general enough to be adapted.
- The skill works best when paired with real artifacts such as templates, code, slides, or execution evidence.
- The repository contains the skill and helpers, not a standalone end-user desktop application.

## Suggested Repository Metadata

Suggested GitHub description:

`Let AI handle repetitive computer lab reports from templates, requirements, slides, and code while preserving structure and truthfulness.`

Suggested topics:

`ai`, `skill`, `lab-report`, `docx`, `education`, `automation`, `computer-science`, `report-writing`
