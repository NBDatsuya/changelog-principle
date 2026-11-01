---
name: changelog-principle
description: Principles for writing and editing a CHANGELOG (Keep a Changelog style). Use when asked to update, fill in, or fix a changelog, or when an agent is about to turn commit messages or a work log into entries. Produces net-result entries written from the reader's side, not rewritten commits.
---

# Changelog principle

A changelog is a curated list of notable changes for humans. It is not `git log`, and it is not a diary of how the code got there.

## The one rule

Each entry answers: **what will a user or developer notice that differs from the last release?** If the answer is "nothing", write no entry.

## Source of truth

Build entries from the **net diff against the last released state** and the intent behind it. Do not start from commit subjects, and do not paraphrase them. Commits record steps; a changelog records outcomes. Use `git log` at most to find which files changed.

## Procedure

1. List candidate changes from the net diff, not per commit and not per file.
2. Collapse to the net result. If something went A -> B -> C before release, record C only. A feature added and then reworked before release is one entry in its final form.
3. Filter with the table below.
4. Fold polish into its feature. Tweaks to a feature that is itself unreleased (spacing, colors, copy, animation timing, bugs found while building it) go inside that feature's entry or nowhere. They never become new `Changed` or `Fixed` lines.
5. Check existing entries first. If a later change reworks, renames, or corrects something already listed under `Unreleased`, edit that entry. Do not append a duplicate.
6. Write each entry, then run the verification gate.

## What gets an entry

| Drop (no entry) | Keep (entry) |
| --- | --- |
| Refactors, helper extraction, renames, file moves | A behavior a user or developer can observe |
| Type fixes, lint fixes, formatting, comment edits | A new or removed command, flag, page, script, or setting |
| Build and dev-server internals | A changed default or limit |
| Docs, decision logs, state-tracking file updates | Deprecations, removals, breaking changes (always list) |
| Polish of an unreleased feature (fold it in) | A bug fix on something already released that a user could hit |
| A bug introduced and fixed inside the same unreleased period | A one-clause known limitation |
| Intermediate states and abandoned approaches | Net-new content or capability |

When unsure whether a change is observable, skip it and name the candidate to the user in one line. Do not pad the file to be safe.

## Entry shape

- One or two plain sentences. Lead with the effect, not the mechanism.
- Allowed: user-facing command names, flags, routes, and setting names, in backticks.
- Not allowed: a `type(scope):` prefix, a bold lead, file or path lists, internal function or constant names, mechanism or trade-off detail. Mechanism belongs in the commit body or a decision log.
- No unmeasured numbers. No vague praise ("improved", "smoother", "enhanced") without saying what changed.
- Match the tense and voice of the surrounding entries.
- One entry may span several commits. One commit may need no entry.
- Group under Keep a Changelog categories (`Added`, `Changed`, `Deprecated`, `Removed`, `Fixed`, `Security`), omit empty ones, and keep newest first.

```text
Bad:  - refactor(viewer): extract tabs into composable and tweak spacing.
Bad:  - Improved the profile viewer UX with better hover handling and updated tab styles.
Good: - The profile view switches between avatars when hovered.
```

## Failure modes

| Symptom | Cause | Fix |
| --- | --- | --- |
| Entry reads like a commit subject | Wrote per commit | Re-derive from the net diff and state the visible effect |
| Several lines for one feature | Logged each tweak as it landed | Merge into one entry for the final form |
| `Changed` or `Fixed` lines for an unreleased feature | Treated unreleased polish as a change | Fold into the feature's `Added` entry |
| Entry names a function, file, or hook | Mechanism leaked in | Move it to the commit body and describe the effect |
| Refactor or type fix appears | Completeness instinct | Delete it; listing everything makes the changelog less trustworthy |
| "Various improvements" | No concrete change identified | Name the observable change or delete the entry |

## Verification gate

1. Every entry traces to an observable difference in the net diff, and no sentence describes something the code does not do.
2. No entry duplicates or contradicts an existing one; reworked items were edited in place.
3. No entry would survive if the intermediate commits were squashed.
4. Nothing from the Drop column is present.
5. Prose is plain: no filler, no invented certainty, nothing upgraded from "may" to "does".
