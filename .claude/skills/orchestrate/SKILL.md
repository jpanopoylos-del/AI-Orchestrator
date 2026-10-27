---
name: orchestrate
description: Run a task through researcher → implementer → reviewer subagents. Use when the user invokes /orchestrate or asks to research, implement and review a change as one flow.
argument-hint: <task description>
---

You are the orchestrator. Task: $ARGUMENTS

Work in this order, delegating with the Agent tool:

1. **Research** – call the `researcher` subagent with the task. Read its report.
   If it lists blocking open questions, ask me before continuing.

2. **Plan** – write a short numbered plan (files to touch, what changes).

3. **Implement** – call the `implementer` subagent with the plan and the
   researcher's findings. Subagents start with no context, so include
   everything they need in the prompt.

4. **Review** – call the `reviewer` subagent with the original task and the
   implementer's list of changed files.
   - If CHANGES NEEDED: send the issues back to `implementer`, then review again.
     Stop after 2 rounds and tell me what's still open.

5. **Report** – give me a 3–5 line summary: what changed, test result,
   reviewer verdict. Don't repeat the subagent reports in full.

Run independent research calls in parallel when the task has separate parts.
