# changelog-principle

An agent skill that keeps CHANGELOG entries about outcomes instead of commit history.

It tells the agent to build entries from the net diff against the last release, drop refactors, lint fixes and intermediate states, fold polish of unreleased features into their original entry, and edit reworked entries in place.

## Install

```bash
npx skills add NBDatsuya/changelog-principle -g -y
```

Or copy `SKILL.md` into your agent's skills folder as `changelog-principle/SKILL.md`.

## Credits

Draws on the net-diff and observable-change ideas in [samber/developer-relations-skills `changelog-writing`](https://github.com/samber/developer-relations-skills) and the format of [Keep a Changelog 1.1.0](https://keepachangelog.com/en/1.1.0/).
