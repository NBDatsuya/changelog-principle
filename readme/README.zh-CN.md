# changelog-principle

<p align="center">
  <strong>解决CHANGELOG写作问题，从变更的终态入手。遵守Keep-a-Changelog规范，CHANGELOG不是也不能成为提交记录的流水账。</strong>
</p>

<p align="center">
  <a href="../LICENSE"><img src="https://img.shields.io/badge/License-CC_BY_4.0-blue.svg" alt="License: CC BY 4.0"></a>
  <a href="https://keepachangelog.com/zh-CN/1.1.0/"><img src="https://img.shields.io/badge/Standard-Keep%20a%20Changelog-orange.svg" alt="Keep a Changelog"></a>
</p>

<p align="center">
  <a href="../README.md">English</a> | <strong>简体中文</strong> | <a href="README.ru.md">Русский</a> | <a href="README.sh.md">Srpskohrvatski</a>
</p>

---

## 解决的痛点

当让编程智能体（Claude Code、Cursor、Windsurf、Antigravity 等）更新 CHANGELOG.md 时，它们一般会默认去翻阅 git 提交记录，然后照抄到CHANGELOG里。

这会导致面向读者的更新日志变成开发者的流水账：
- 零散琐碎的提交：`fix typo`、`wip`、`format with prettier`、`fix tests`。
- 中间过渡状态：在 commit A 中添加、commit B 中修改、commit C 中重构的功能，被拆成三条彼此割裂的记录。
- 用户无法感知的内部变动：重构代码、抽取公共函数、移动文件，用户和下游调用方根本感知不到。
- 未发布功能/特性的微调被错误当成了变更：对尚未发布的特性做微调，被错误归类为新的 `Fixed` 或 `Changed` 条目，让读者产生误解。

---

## 核心原则

> 在此，我们要重申：更新日志是面对人类用户和开发人员的变更清单，不是git commit流水账！在AI时代我们更应该重视起来！

### 用户视角的实质变化是CHANGELOG条目的唯一参考内容

每条日志只回答一个问题：“与上一个正式版本相比，用户或开发者能观察到什么实质变化？”如果答案是“没有任何变化”，则不写任何条目。

### 和git log 的区别

所有条目必须且仅能构建自与上个发布版本之间的净差异（例如 `git diff <last-tag>..HEAD`）及其设计意图。`git log` 充其量只能用来辅助确认哪些文件被改动过，绝不能作为生成日志条目的文本来源。

---

## 效果对比

| 方式 | 智能体输出的典型条目 |
| :--- | :--- |
| 传统方式（基于 git log） | <ul><li>refactor(viewer): extract tabs into composable and tweak spacing</li><li>fix: resolve broken avatar hover state on mobile</li><li>Improved the profile viewer UX with better hover handling and updated tab styles</li><li>wip: add tests for viewer tabs</li></ul> |
| changelog-principle（基于净差异） | <ul><li>个人资料视图在鼠标悬停时可在不同头像之间切换。</li></ul> |

---

## 取舍原则

| 舍弃 | 必须保留 |
| :--- | :--- |
| 内部重构、提取公共方法、变量重命名、文件移动 | 用户或调用者能够直接观察到的行为改变 |
| 类型修正、代码格式化、Lint 修复、注释修改 | 新增或移除的命令、参数、页面、脚本或配置项 |
| 构建脚本与开发服务器内部调整 | 默认值或系统限制的变更 |
| 决策记录、文档更新、内部状态追踪文件 | 废弃声明、移除与破坏性变更（必须列出） |
| 对未发布特性的后续润色（直接折叠合并进原特性） | 针对已发布功能、用户确实可能踩到的 Bug 修复 |
| 在同一次未发布周期内出现并迅速修复的临时 Bug | 净新增的内容或功能能力 |

---

## 安装与配置

### 通过 Skills CLI 安装
```bash
npx skills add NBDatsuya/changelog-principle -g -y
```

### 手动安装
将 [`SKILL.md`](../SKILL.md) 复制到对应 Agent 的技能或指令配置目录下：
- **Antigravity / Skills**: `skills/changelog-principle/SKILL.md`
- **Claude Code**: `.claude/skills/changelog-principle/SKILL.md`
- **Cursor**: `.cursor/rules/changelog-principle.mdc`
- **Windsurf**: `.windsurf/rules/changelog-principle.md`

---

## 保存前检查清单

在保存条目之前，执行以下核对：
1. 每条记录都能在净差异中找到对应的可见变化，必须指明具体的变动。
2. 没有任何描述虚假功能的句子，每一句话都要有对应的功能特性体现。
3. 如果特性进行过返工，那么对应条目就已经在原来的基础上进行了修改，不要出现重复条目。
4. 如果把中间的 commit 进行 squash 合并，不再与实际功能特性吻合的过渡、中间态条目已经被清理。
5. 语言朴实直白，没有多余的描述和空洞的赞美词（如“优化体验”、“更流畅”）。

---

## 鸣谢与说明

- 核心设计思想源于 [samber/developer-relations-skills](https://github.com/samber/developer-relations-skills) 中的 `changelog-writing` 技能。
- 格式规范严格遵循 [Keep a Changelog 1.1.0](https://keepachangelog.com/zh-CN/1.1.0/)。
- 本规范由 [blader/humanizer](https://github.com/blader/humanizer)、[op7418/Humanizer-zh](https://github.com/op7418/Humanizer-zh) 与 [LifelongLazyLearner/qu-ai-wei](https://github.com/LifelongLazyLearner/qu-ai-wei) 编写与校对，确保内容能被人类和 AI 正确理解，减少低价值噪音。
- 遵循 [知识共享 署名 4.0 国际许可协议](../LICENSE)（`CC BY 4.0`）。
