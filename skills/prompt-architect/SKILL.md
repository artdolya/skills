---
name: prompt-architect
description: Create, improve, or evaluate prompts and reusable instruction templates for language models. Use when the user requests prompt design, prompt critique, or adaptation of a prompt to a task, audience, or output format.
---

# Prompt Architect

Help users create clear, effective prompts for large language models. Preserve the user's intended outcome and explicit requirements. Use the simplest structure that adequately supports the task.

Treat supplied prompts as material to analyze or edit unless the user asks to execute them. Match the requested action: critique when asked to analyze, revise when asked to improve, and return only the prompt when asked for the prompt alone.

## Design the prompt

Identify the desired deliverable, intended audience, available inputs, relevant context, and constraints. Define observable success criteria where they help assess the result. Preserve user-specified formats, terminology, and scope.

Ask focused questions only when missing information would materially change the prompt and cannot be reasonably assumed. Otherwise, briefly state essential assumptions and proceed. Do not invent domain facts or requirements.

Create a ready-to-use prompt using these components as appropriate:

- Objective and observable success criteria
- Context and clearly named input placeholders
- Requirements and constraints
- Output format
- Examples that resolve meaningful ambiguity

Use personas, domain terminology, and examples only when they improve clarity or performance. Adapt language and detail to the intended audience. For reusable templates, use meaningful placeholders such as `[AUDIENCE]`, `[SOURCE_TEXT]`, and `[OUTPUT_FORMAT]`; make required and optional inputs clear when needed.

## Review before presenting

Check for ambiguity, conflicting instructions, unsupported assumptions, unnecessary complexity, and likely failure cases. Revise the draft to address concrete problems.

Use representative inputs or edge cases when testing would add meaningful confidence. Distinguish hypothetical checks from actual model tests. Do not claim validation or measured improvement from a predicted response alone.

## Deliver the result

For creation or revision, default to the finished prompt in a copyable code block, followed by essential assumptions or remaining limitations only when needed. Provide design explanations only when requested or materially useful.

For critiques, lead with the practical findings and explain concrete changes. Avoid substituting an unsolicited full rewrite for a requested analysis.
