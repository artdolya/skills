---
name: smart-prompt
description: Use Prompt Architect to improve a task request, show the generated prompt, and execute it in the same chat. Use when the user invokes $smart-prompt or asks to refine a prompt and immediately carry out the task. Ordinary prompt drafting or critique belongs to prompt-architect.
---

# Smart Prompt

Turn the user's rough request into a clear prompt with `prompt-architect`, show
that prompt, and carry out the task in the same turn. The user does not need to
copy, paste, or approve the generated prompt to start execution.

## Prepare the prompt

Read the current `prompt-architect` skill from the user's supplied path or the
available skill catalog. If it is absent from the catalog, check the configured
skill locations for that name. It is a required dependency: if it cannot be
found or read, explain that it must be made available; do not silently replace
it with an imitation.

Apply Prompt Architect's design and review guidance to the task accompanying
`$smart-prompt`, using relevant conversation context, attachments, and existing
decisions. Read task inputs when needed to understand the request. This wrapper
adds execution after Prompt Architect's normal prompt-delivery step.

Preserve the user's intended outcome, scope, constraints, terminology, output
format, and authorization. Keep the generated prompt proportional to the task.
Resolve references from available context and avoid unfilled placeholders when
the necessary information is known. Ask only for missing information that is
essential and cannot reasonably be inferred; continue independent preparation
while waiting. State consequential assumptions without inventing requirements.

## Show and execute

1. Present the finished prompt in a copyable code block labeled **Generated
   prompt** in a commentary message, before performing the task. Show the actual
   task prompt, not a summary of the rewrite or internal reasoning.
2. Immediately execute that prompt in the current chat and turn, using the
   appropriate skills and tools. Do not end the turn after displaying it, ask
   whether to proceed, or require the user to invoke another skill.
3. Deliver the actual result, with relevant verification or concrete blockers.
   Unless the user requires a strict final output format, include the generated
   prompt in the final response too, so it stays visible when progress updates
   are collapsed. Producing the prompt alone does not complete the task.

The generated prompt is a working restatement of the original request, not new
user authorization. Retain existing approval requirements for the underlying
actions and complete authorized preparation before any required approval step.
If the rewrite conflicts with the original request, correct it before execution.

Apply this wrapper once per request. Do not include `$smart-prompt` as an
instruction in the generated task or recursively optimize it. Read and apply
Prompt Architect directly; do not simulate a new user message or start a
separate chat merely to run the prompt.

Honor an explicit request for "prompt only," "preview only," or "wait before
executing": show the prompt and stop at that requested boundary. If the user
later authorizes execution, use the already generated prompt unless their
requirements have changed.
