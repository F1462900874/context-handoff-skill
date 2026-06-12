# Context Handoff Skill

A reusable Codex skill for generating continuation-ready task handoffs.

It helps compress the current task into:

- a Markdown handoff file in the workspace
- a concise summary that can be pasted into a new thread

The skill is designed to preserve momentum across threads, windows, and later sessions while clearly separating confirmed facts from assumptions.

## What It Does

When invoked, `context-handoff` guides Codex to:

- inspect the current thread and workspace context first
- summarize the work into a fixed handoff structure
- write a Markdown handoff file into the current workspace
- return a short new-thread prompt for immediate continuation

Default behavior:

- output language: Chinese
- default filename: `handoff.md`
- if `handoff.md` already exists and overwrite is not explicitly requested, use `handoff-YYYYMMDD-HHMM.md`

## Repository Layout

```text
context-handoff-skill/
├─ .gitignore
├─ LICENSE
├─ README.md
└─ context-handoff/
   ├─ SKILL.md
   ├─ agents/
   │  └─ openai.yaml
   └─ references/
      └─ SKILL-cn.md
```

## Install

Copy the `context-handoff/` folder into your Codex skills directory:

- Windows: `C:\Users\<you>\.codex\skills\`
- macOS/Linux: `~/.codex/skills/`
- Or: `$CODEX_HOME/skills/`

After installation, restart Codex if needed so the skill is rediscovered.

## Verified GitHub Install

This repository has been verified with the Codex GitHub skill installer.

At the time of verification, the repository default branch is `master`, so the install command should include `--ref master`.

Example:

```bash
python install-skill-from-github.py --repo F1462900874/context-handoff-skill --path context-handoff --ref master --method download
```

If you use the installer skill or script directly, prefer `--method download` for public installs.

Restart Codex to pick up new skills.

## How to Use

Recommended explicit invocation:

```text
用 $context-handoff 生成交接文档
```

More explicit examples:

```text
用 $context-handoff 把当前任务整理成可在新线程继续的 handoff，写到工作区文件里
```

```text
用 $context-handoff 生成交接文档，文件名用 handoff-api.md
```

English examples:

```text
Use $context-handoff to generate a concise handoff for this task.
```

```text
Use $context-handoff to write a workspace handoff file and a new-thread summary.
```

## Output Shape

The skill instructs Codex to produce a handoff with these sections:

- `Task`
- `Current Goal`
- `Confirmed Facts`
- `Key References`
- `Assumptions / Inferences`
- `Tried Already`
- `Open Questions`
- `Next Best Step`
- `Suggested New-Thread Prompt`

## Language Strategy

`SKILL.md` remains the required entry file.

Language-specific guidance lives in companion files such as:

- `references/SKILL-cn.md`
- future: `references/SKILL-ja.md`

This keeps the skill compatible with Codex while allowing multilingual expansion.

## Contributing

Suggested ways to improve this skill:

- refine the handoff template for different task types
- add `SKILL-ja.md` or other locale-specific guidance
- improve examples in `SKILL.md`
- add more install and usage notes based on real-world workflows

If you change behavior, keep these invariants:

- facts and inferences must stay clearly separated
- the output must remain continuation-oriented
- the skill should still produce both a file-oriented handoff and a chat-ready continuation prompt

## License

This repository currently uses the MIT License.
