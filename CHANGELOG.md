# Changelog

All notable changes to this project are documented here.
Format based on [Keep a Changelog](https://keepachangelog.com/), versioning follows [SemVer](https://semver.org/).

## [1.1.0] - 2026-11-27

### Added
- Always-On mode: `always-on/short.md` (paste into custom instructions) and `always-on/full.md` (append to `CLAUDE.md` or `AGENTS.md`), for people who want the behavior in every conversation instead of relying on auto-triggering.
- README setup guide for many tools: chat apps (Claude, ChatGPT, Gemini, others) and coding agents (Claude Code, Codex, Gemini CLI, Cursor, Copilot, Windsurf, Cline, Roo Code, Continue, OpenCode, Zed, Aider), plus skills directories per tool.
- README sections for skill vs. always-on comparison and compatibility status.

### Changed
- README now leads with Always-On as the recommended mode.

## [1.0.0] - 2026-11-26

### Added
- Real `description` with trigger phrases (English and Indonesian) and explicit "do not use" cases.
- Quick decision flow and a response shape in `SKILL.md`.
- `references/signals.md`: explicit and implicit signals, ten confusion types, confusion vs. look-alikes.
- `references/approaches.md`: playbooks for explanation, example, step-by-step, decision paralysis, overwhelm; adaptation ladder; comprehension-check patterns.
- `references/examples.md`: eight worked scenarios, including false-positive and non-English cases.
- `evals/`: eight test cases with graders.
- Language rule: reply in the user's language and register.
- Wellbeing boundary: set the workflow aside when difficulty is tied to real distress.

### Changed
- Frontmatter rewritten to valid, un-indented YAML; `tags` moved under `metadata`.
- "Do what the user asks" exception added: if the user wants it done, do it.

### Removed
- Placeholder description ("No description yet.").
