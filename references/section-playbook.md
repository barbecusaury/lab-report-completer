# Section Playbook

Use this reference when filling common experiment-report sections after you have already inspected the template and the task requirements.

## Cover Fields

Usually user-supplied, not inferable:

- Student name
- Student ID
- Class
- Major
- Teacher
- Submission date if the template requires a specific date
- Lab location when not inferable

Rules:

- Fill only what is explicitly given or safely discoverable.
- Leave clear placeholders for anything identity-related that was not provided.
- Never invent grades, signatures, reviewer comments, or attendance fields.

## 实验目的

Write this section from the requirement goals, not from random textbook boilerplate.

Good inputs:

- task wording
- specified technologies
- expected capabilities

Typical content:

- what the student needed to learn
- what framework/tool/process was practiced
- what practical capability was strengthened

Keep it concise and outcome-oriented.

## 实验内容

Summarize the actual requirements and target tasks.

Include:

- environment or setup requirements if the assignment mentions them
- major features or functions to implement
- special validation or constraints
- required deliverables such as code package, screenshots, or report format

This section can closely reflect the assignment wording, but clean it up into report style.

## 实验设备与软件环境

Prefer concrete environment facts from the workspace or the user’s setup.

Typical items:

- operating system
- language runtime
- framework/library
- IDE or editor
- database or browser if relevant

If the exact version is unknown, avoid fake precision. Use generic but truthful wording such as `Python 3.x` or `Windows`.

## 实验过程与结果

This is usually the most important section.

Write it as an ordered process:

1. Environment setup
2. Project or file initialization
3. Core implementation steps
4. Validation or test steps
5. Final observed result

Rules:

- Anchor the prose to the real implementation or real requirements.
- If code had to be written, describe the actual modules, fields, validations, or routes that were implemented.
- Reserve screenshot insertion markers at meaningful checkpoints.
- Do not claim success if the program was not actually checked.

## 操作异常问题与解决方案

List realistic issues tied to the task rather than generic “no issues occurred”.

Good examples:

- missing dependency
- path mismatch
- template not rendering
- validation logic failure
- encoding or formatting problem

For each issue:

- state the symptom
- give the likely cause
- explain the resolution

## 实验总结

Summarize:

- what was learned
- what technical understanding improved
- why the task matters for future coursework or development

Keep it reflective but concrete. Avoid exaggerated claims.

## Screenshot Placeholders

Use numbered placeholders that match the guidance you will give in chat.

Examples:

- `【截图预留1：项目环境配置完成】`
- `【截图预留2：主界面初始状态】`
- `【截图预留3：异常提示或校验失败】`
- `【截图预留4：成功运行结果】`

If the template already has “可贴图” or similar wording, replace it with concrete placeholders instead of leaving a generic reminder.
