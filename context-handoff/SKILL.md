---
name: context-handoff
description: Generate a continuation-ready handoff for the current task and thread. Use when the user wants to continue work in another thread, window, or later session, or asks for a handoff, context transfer, continuation summary, 交接文档, 上下文续接, 新线程继续任务, or a concise restart prompt. Produce both a Markdown handoff file in the current workspace and a compact chat summary that can be pasted into a new thread.
---

# Context Handoff

Generate a high-density handoff that preserves task continuity without copying the whole conversation.

If the working language is Chinese, also read [references/SKILL-cn.md](references/SKILL-cn.md) before producing the handoff. Keep `SKILL.md` as the required entry file for the skill. Use locale-suffixed companion files such as `SKILL-cn.md` or `SKILL-ja.md` for language-specific guidance.

Invocation examples:

- `Use $context-handoff to generate a concise handoff for this task.`
- `Use $context-handoff to write a workspace handoff file and a new-thread summary.`

## Workflow

1. Gather context from the current thread and workspace before asking questions.
2. Distinguish confirmed facts from assumptions or inferences.
3. Compress the work into a fixed structure focused on continuation.
4. Write a Markdown handoff file in the current workspace.
5. Return a compact chat-ready summary with a suggested new-thread prompt.

## Defaults

- Default output language: Chinese.
- Keep code identifiers, APIs, commands, and file names in their original language.
- Default filename: `handoff.md`.
- If `handoff.md` already exists and the user did not explicitly ask to overwrite it, create `handoff-YYYYMMDD-HHMM.md`.
- Default location: current workspace root.
- If the user gives a destination path or filename, use it.

## Required Output Structure

Use this exact section order in the Markdown handoff:

```md
# Task

## Current Goal

## Confirmed Facts

## Key References

## Assumptions / Inferences

## Tried Already

## Open Questions

## Next Best Step

## Suggested New-Thread Prompt
```

## Content Rules

- Never present speculation as fact.
- Never dump full chat history or long transcript excerpts.
- Preserve commands already run, findings already proven, and dead ends already explored.
- Prefer reusable handoff wording over conversational filler.
- Include at least one ready-to-send prompt for a new thread.
- Keep the summary dense, specific, and continuation-oriented.

## Section Guidance

### Current Goal

State the active objective in one to three sentences. Mention the desired endpoint, not the whole history.

### Confirmed Facts

List only validated conclusions. If a point is not proven, move it to `Assumptions / Inferences`.

### Key References

Tailor this section by task type:

- Code tasks: include exact file links, relevant symbols, commands, and test/build status.
- Research tasks: include evidence sources, findings, hypotheses, and the best next analysis path.
- Mixed tasks: include both.

Prefer clickable local file links with line numbers when available.

### Assumptions / Inferences

List inferred or likely conclusions separately from facts. Use wording such as `推断` or `尚未证实`.

### Tried Already

Capture:

- searches already performed
- commands already run
- branches already ruled out
- failed or unproductive approaches worth not repeating

### Open Questions

Include only unresolved items that materially affect the next step.

### Next Best Step

Give the single best continuation path first. If there are multiple valid branches, rank them.

### Suggested New-Thread Prompt

Write a concise prompt that a user can paste into a fresh thread. It should name the task, point to the handoff file, and tell the next agent what to continue.

Example:

```md
继续处理当前任务。先阅读 [handoff.md](/abs/path/handoff.md) 和相关代码引用，然后从“Next Best Step”开始继续，不要重复已经验证过的搜索和结论。
```

## File-Writing Behavior

When creating the handoff file:

- write Markdown only
- prefer the workspace root unless instructed otherwise
- include exact file paths and line references for important findings
- if there is too little context, still produce a lightweight handoff and say what is missing rather than inventing details

## Response Behavior

After writing the file:

- tell the user which file was created
- provide a short chat summary
- include the paste-ready new-thread prompt inline

If file writing is not possible in the current environment, still produce the full handoff content in chat and clearly state that the file could not be written.
