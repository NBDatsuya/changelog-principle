# changelog-principle

<p align="center">
  <strong>Solve changelog generation at the outcome level. Compliant with Keep a Changelog: a changelog is not and cannot be a stream of git commits.</strong>
</p>

<p align="center">
  <a href="LICENSE"><img src="https://img.shields.io/badge/License-CC_BY_4.0-blue.svg" alt="License: CC BY 4.0"></a>
  <a href="https://keepachangelog.com/en/1.1.0/"><img src="https://img.shields.io/badge/Standard-Keep%20a%20Changelog-orange.svg" alt="Keep a Changelog"></a>
</p>

<p align="center">
  <strong>English</strong> | <a href="readme/README.zh-CN.md">简体中文</a> | <a href="readme/README.ru.md">Русский</a> | <a href="readme/README.sh.md">Srpskohrvatski</a>
</p>

---

## What this skill solves

When coding agents (Claude Code, Cursor, Windsurf, Antigravity, and others) update a `CHANGELOG.md`, they typically read `git log` and paraphrase commit subjects.

This turns release notes into an internal developer log:
- Cluttered commits: `fix typo`, `wip`, `format with prettier`, `fix tests`.
- Intermediate states: A feature added in commit A, altered in commit B, and refactored in commit C is logged as three confusing entries.
- Invisible churn: Refactors, extracted helpers, and file moves that end users never observe.
- Premature change logs: Polish applied to an unreleased feature is misclassified as `Fixed` or `Changed` entries for something users have not yet seen.

---

## Core principles

> We reaffirm: a changelog is a curated list of notable changes for users and developers, not a stream of git commits. In the AI coding era, keeping this distinction clean matters more than ever.

### Observable difference from the user perspective is the only basis for an entry

Each entry answers one question: "What will a user or developer notice that differs from the last official release?" If the answer is "nothing", write no entry.

### Difference from git log

Build entries strictly from the net diff against the last released version (such as `git diff <last-tag>..HEAD`) and the intent behind it. Use `git log` only to verify which files changed, never as the source text for changelog entries.

---

## Before & after

| Approach | Typical agent output |
| :--- | :--- |
| Typical agent (from git log) | <ul><li>refactor(viewer): extract tabs into composable and tweak spacing</li><li>fix: resolve broken avatar hover state on mobile</li><li>Improved the profile viewer UX with better hover handling and updated tab styles</li><li>wip: add tests for viewer tabs</li></ul> |
| changelog-principle (from net diff) | <ul><li>The profile view switches between avatars when hovered.</li></ul> |

---

## Inclusion criteria

| Drop | Keep |
| :--- | :--- |
| Refactors, helper extraction, renames, file moves | Observable behavior changes for users or developers |
| Type fixes, lint fixes, formatting, comments | New or removed commands, flags, pages, scripts, or settings |
| Build scripts and dev server internals | Changed defaults or limits |
| Decision logs, docs, internal tracking files | Deprecations, removals, and breaking changes (always list) |
| Polish of an unreleased feature (fold into the original entry) | Bug fixes on already released features that users could hit |
| Bugs introduced and fixed within the same release cycle | Net-new content or capabilities |

---

## Installation & setup

### Via Skills CLI
```bash
npx skills add NBDatsuya/changelog-principle -g -y
```

### Manual installation
Copy [`SKILL.md`](SKILL.md) into your agent's skills or instructions folder:
- **Antigravity / Skills**: `skills/changelog-principle/SKILL.md`
- **Claude Code**: `.claude/skills/changelog-principle/SKILL.md`
- **Cursor**: `.cursor/rules/changelog-principle.mdc`
- **Windsurf**: `.windsurf/rules/changelog-principle.md`

---

## Pre-save checklist

Before saving changelog entries, verify:
1. Every entry corresponds to an observable difference in the net diff, explicitly naming the concrete change.
2. No sentence describes phantom or unverified features; every statement reflects an actual observable capability.
3. If a feature was reworked, its entry is edited in place on the original record to prevent duplicate entries.
4. If intermediate commits were squashed, all transitional or intermediate entries that no longer match the final behavior have been pruned.
5. Phrasing is plain and direct, free of redundant descriptions or empty praise ("improved", "smoother").

---

## Credits & notes

- Core design ideas draw from net-diff concepts in [samber/developer-relations-skills](https://github.com/samber/developer-relations-skills) (`changelog-writing` skill).
- Format strictly adheres to [Keep a Changelog 1.1.0](https://keepachangelog.com/en/1.1.0/).
- This specification was drafted and verified using [blader/humanizer](https://github.com/blader/humanizer), [op7418/Humanizer-zh](https://github.com/op7418/Humanizer-zh), and [LifelongLazyLearner/qu-ai-wei](https://github.com/LifelongLazyLearner/qu-ai-wei) to ensure precise comprehension by humans and AI models without producing junk output.
- Licensed under [Creative Commons Attribution 4.0 International](LICENSE) (`CC BY 4.0`).
