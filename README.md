# Confusion Detector

Makes your AI assistant notice when you are confused, stuck, or overwhelmed, work out what exactly is unclear, and help with the lightest guidance that works: an explanation, an example, or a single next step. It then checks whether the help landed and adapts if it did not.

It is just as careful about the opposite mistake. Short, casual, misspelled, or basic messages are **not** treated as confusion.

Works with any assistant that accepts custom instructions, `AGENTS.md`-style files, or Agent Skills: Claude, ChatGPT, Gemini, Codex, Cursor, GitHub Copilot, Windsurf, Cline, and more. See [Setup by tool](#setup-by-tool).

## Two ways to use it

| Mode | How it activates | Best for |
|---|---|---|
| **Always-On** (recommended) | Instructions are read in every conversation | Consistent behavior; works in nearly every tool |
| **Skill** | The assistant decides from the skill's description whether to load it | Keeping everyday context light; full playbooks and examples |

Auto-triggering a skill is a judgment call by the assistant, so it is never guaranteed. If you want this behavior every time, use Always-On. You can also use both.

Two ready-to-paste texts live in [`always-on/`](always-on):

- [`short.md`](always-on/short.md): about 1,000 characters. For chat apps and fields with a size limit.
- [`full.md`](always-on/full.md): detection rules, approach table, adaptation steps, boundaries. For files read by coding agents.

## Setup by tool

Menu names and file locations change between versions. If something does not match, check the tool's own documentation for "custom instructions", "rules", or "skills".

### Chat apps: paste `always-on/short.md`

| Tool | Where to paste |
|---|---|
| **Claude** (claude.ai, Desktop, mobile) | Settings → Profile → personal preferences; or a Project's instructions |
| **ChatGPT** | Settings → Personalization → Custom instructions; or a Project's instructions |
| **Gemini** (app and web) | Settings → Instructions for Gemini; see Google's help page "Personalize Gemini's responses with your instructions". A Gem's instructions also work for a single use case |
| **Perplexity, Grok, Mistral Le Chat, Microsoft Copilot, others** | Look for custom instructions, AI profile, personalization, or a space/project instructions field |
| **Any API or playground** | Add it to the system prompt |

### Coding agents: add `always-on/full.md` to the instructions file

| Tool | File or location |
|---|---|
| **Claude Code** | `CLAUDE.md` (project) or `~/.claude/CLAUDE.md` (all projects) |
| **OpenAI Codex** | `AGENTS.md` (project) or `~/.codex/AGENTS.md` (global) |
| **Gemini CLI** | `GEMINI.md` (project) or `~/.gemini/GEMINI.md` (global) |
| **Gemini in Android Studio** | `AGENTS.md` |
| **Cursor** | `AGENTS.md`, or a rule in `.cursor/rules/`, or User Rules in Settings |
| **GitHub Copilot** | `.github/copilot-instructions.md` (or `AGENTS.md` where supported) |
| **Windsurf** | `.windsurf/rules/` or global rules in Settings; `AGENTS.md` is also read |
| **Cline** | `.clinerules` |
| **Roo Code** | `.roo/rules/` |
| **Continue** | `.continue/rules/` |
| **OpenCode** | `AGENTS.md` |
| **Zed** | `.rules` or `AGENTS.md` |
| **Aider** | Save as `CONVENTIONS.md` and run `aider --read CONVENTIONS.md` |
| **Anything else** | Most tools read `AGENTS.md`; try that, then check the docs |

Example for several tools at once:

```bash
cat always-on/full.md >> AGENTS.md          # Codex, Cursor, OpenCode, Zed, ...
cat always-on/full.md >> CLAUDE.md          # Claude Code
cat always-on/full.md >> GEMINI.md          # Gemini CLI
mkdir -p .github && cat always-on/full.md >> .github/copilot-instructions.md   # Copilot
```

Use `>>` (append), not `>`, so you do not overwrite instructions you already have.

## Skill mode

The folder is a standard Agent Skill: a `SKILL.md` with YAML frontmatter, plus `references/`. Typical triggers: "I don't get it", "I'm lost", "I don't know where to start", a pasted error with "why?", asking again after an explanation, "bingung", "gatau mulai dari mana".

### Claude.ai / Claude Desktop
1. Download `confusion-detector.skill` from the [Releases](../../releases) page (or build it, see below).
2. Open **Settings → Capabilities → Skills** and upload the file.
3. Make sure Skills is enabled.

### Any agent that supports Agent Skills
Install with the community Skills CLI (not tested with this repository yet):

```bash
npx skills add AvarynND/confusion-detector
```

Or clone the folder into the tool's skills directory:

```bash
git clone https://github.com/AvarynND/confusion-detector.git <skills-dir>/confusion-detector
```

Commonly used skills directories (project-level; many tools also have a global one under `~`):

| Tool | `<skills-dir>` |
|---|---|
| Claude Code | `.claude/skills` |
| OpenAI Codex | `.codex/skills` or `.agents/skills` |
| Gemini CLI | `.gemini/skills` |
| Cursor | `.cursor/skills` |
| GitHub Copilot | `.github/skills` |
| Cline | `.cline/skills` |
| Continue | `.continue/skills` |
| OpenCode | `.opencode/skills` |

The Gemini app also has a Customize area with a Skills tab; check Google's help page for how to add your own.

## What it does

| It does | It does not |
|---|---|
| Spots explicit and implicit signs of confusion | Label users as confused or slow |
| Finds the specific gap (term, step, reason, goal) | Ask "what are you confused about?" |
| Picks explanation, example, or step-by-step | Dump a full tutorial or plan |
| Checks understanding with small tasks | Quiz people or ask only "does that make sense?" |
| Changes approach when the first try fails | Repeat the same explanation louder |
| Replies in the user's language and register | Assume confusion from typos, slang, or short messages |

## Try it

```
I've read the docs three times and I still don't get what "idempotent" means.
gw disuruh bikin proposal skripsi tapi gatau harus mulai dari mana
I got two job offers and I've been going back and forth for a week. Which one??
```

And one that should **not** trigger the confusion workflow:

```
whats the diff between let and const in js
```

## Compatibility and testing status

| Environment | Status |
|---|---|
| Claude skill format | Validated against the skill validator |
| Always-On text in chat apps and agents | Plain text, should work anywhere custom instructions exist |
| Other agents' skill loaders | Same open format; not tested yet |
| Chat apps without file or skill support | Use `short.md` only. The `references/` files are not read there |

The skill uses only portable frontmatter fields (`name`, `description`, `license`, `metadata`). Test reports for other tools are welcome as issues.

## Repository layout

```
confusion-detector/
├── SKILL.md                 # Skill instructions (loaded when triggered)
├── always-on/
│   ├── short.md             # Paste into custom instructions
│   └── full.md              # Append to AGENTS.md, CLAUDE.md, GEMINI.md, ...
├── references/
│   ├── signals.md           # Evidence, ten confusion types, false positives
│   ├── approaches.md        # Playbooks, adaptation ladder, comprehension checks
│   └── examples.md          # Eight worked scenarios
├── evals/                   # Test cases (prompt, expected outcome, graders)
├── README.md
├── CHANGELOG.md
├── LICENSE                  # Apache-2.0
└── .gitignore
```

## Testing

The folders in `evals/` follow the layout used by `claude plugin eval` (Claude Code 2.1.269 or later):

```bash
cd confusion-detector
claude plugin eval . --allow-tools Write,Edit,Bash
```

Each case has a `prompt.md`, a `case.yaml` with the expected outcome, and one grader file per assertion. These make real model calls and may be billed.

To test Always-On mode in any tool, paste `always-on/short.md` into a fresh chat and run the same prompts by hand.

## Building the `.skill` file

A `.skill` file is a zip of the skill folder. From the folder that contains `confusion-detector/`:

```bash
zip -r confusion-detector.skill confusion-detector -x "confusion-detector/evals/*" "confusion-detector/.git/*"
```

## Contributing

Issues and pull requests are welcome. Good contributions:

- A realistic prompt where the behavior fired when it should not have, or failed to fire when it should have (add it as a case under `evals/`).
- Setup notes or corrections for a specific tool.
- Examples in other languages.
- Tightening wording that makes responses longer than they need to be.

Keep `SKILL.md` under 500 lines and put detail in `references/`. When you change the behavior, update `always-on/short.md` and `always-on/full.md` so the three stay in sync.

## License

Apache-2.0. See [LICENSE](LICENSE).

## Author

Avaryn ND (Not Dev), [github.com/AvarynND](https://github.com/AvarynND)
