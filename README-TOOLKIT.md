# Skill Authoring Toolkit

A working reference for writing high-quality **Agent Skills** (`SKILL.md` files) — the portable format used by Claude Code, GitHub Copilot CLI, Microsoft Scout, Gemini CLI, and others.

This is a fork of [`anthropics/skills`](https://github.com/anthropics/skills) (Apache 2.0), plus the official authoring documentation from [agentskills.io](https://agentskills.io) saved locally for offline reference.

## Start here

| If you want to... | Go to |
|---|---|
| Build or improve a skill interactively | [`skills/skill-creator/`](skills/skill-creator/) — install it, then ask your agent to use it |
| Learn the craft principles | [`reference/agentskills.io/best-practices.md`](reference/agentskills.io/best-practices.md) |
| Make a skill trigger reliably | [`reference/agentskills.io/optimizing-descriptions.md`](reference/agentskills.io/optimizing-descriptions.md) |
| Test whether a skill actually helps | [`reference/agentskills.io/evaluating-skills.md`](reference/agentskills.io/evaluating-skills.md) |
| Know the format rules | [`reference/agentskills.io/specification.md`](reference/agentskills.io/specification.md) |

## Skills by category

### Meta — building skills themselves
- **`skill-creator`** — the meta-skill: interview → draft → eval → iterate. Includes eval scripts, a benchmark aggregator, a description optimizer, and an HTML eval viewer.
- **`mcp-builder`** — build MCP servers.

### Document generation
- **`docx`**, **`pptx`**, **`pdf`**, **`xlsx`** — production-grade Office/PDF manipulation. Excellent examples of prescriptive, script-backed skills.

### Design & front-end
- **`canvas-design`**, **`frontend-design`**, **`web-artifacts-builder`**, **`theme-factory`**, **`algorithmic-art`**, **`brand-guidelines`**

### Writing & collaboration
- **`doc-coauthoring`**, **`internal-comms`**

### Engineering
- **`webapp-testing`**, **`claude-api`**

### Fun
- **`slack-gif-creator`**

## Install a skill

Copy the skill folder into your agent's skills directory:

```powershell
# Microsoft Scout
Copy-Item skills\skill-creator "$env:USERPROFILE\.scout\m-skills\skill-creator" -Recurse

# GitHub Copilot CLI
Copy-Item skills\skill-creator "$env:USERPROFILE\.copilot\skills\skill-creator" -Recurse
```

```bash
# Claude Code
cp -r skills/skill-creator ~/.claude/skills/
```

Then invoke it as `/skill-creator`.

## The craft, condensed

Distilled from the reference docs — the rules that matter most in practice:

1. **The `description` field is the whole ballgame.** It's the only thing loaded at startup, so it carries the entire triggering decision. Write it as an instruction ("Use this skill when…"), describe *user intent* rather than internal mechanics, and be deliberately **pushy** — agents tend to *under*-trigger skills. Hard limit 1,024 characters.

2. **Add what the agent lacks; cut what it knows.** Don't explain what a PDF is. Do say which library to use and what to fall back to. Test every sentence against: *"Would the agent get this wrong without this?"* If no, delete it.

3. **Progressive disclosure.** Keep `SKILL.md` under ~500 lines / 5,000 tokens. Move depth into `references/` — and say exactly *when* to load each file ("Read `references/api-errors.md` if the API returns a non-200"), not a vague "see references/".

4. **Gotchas are the highest-value section.** Environment-specific facts that defy reasonable assumptions. Every time you correct the agent in conversation, add that correction here.

5. **Match prescriptiveness to fragility.** Rigid, exact commands for destructive or order-dependent operations; explain the *why* and leave room to judge everywhere else.

6. **Defaults, not menus.** One recommended tool with a brief escape hatch beats four equal options.

7. **Procedures over answers.** Teach how to approach a *class* of problems, not the answer to today's instance.

8. **Templates beat prose** for output format — agents pattern-match against concrete structures far better than descriptions.

## Licence

Upstream content: Apache 2.0 (see `LICENSE`). Some bundled example skills are source-available rather than fully OSS — check individual folders.
`reference/agentskills.io/` is documentation from agentskills.io, CC-BY-4.0, saved here for offline use.
