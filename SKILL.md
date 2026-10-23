---
name: gongzi-teaches-code-debt
description: >
  【技术债账本】把代码里所有 ponytail: 简化注释收集成一张表，逐条列出
  「简化了什么 / 上限在哪 / 什么时候该升级」，防止「以后再说」变成「永远不做」。
  只读不改。触发词：/ponytail-debt、ponytail 欠了什么、列出偷懒的地方、
  技术债清单。
---

Every deliberate ponytail shortcut is marked with a `ponytail:` comment naming
its ceiling and upgrade path. This collects them into one ledger so a deferral
can't quietly become permanent.

## Scan

Grep the repo for comment markers, skipping `node_modules`, `.git`, and build
output:

`grep -rnE '(#|//) ?ponytail:' .`  (add other comment prefixes if your stack uses them)

Each hit is one ledger row. The comment prefix keeps prose that merely mentions
the convention out of the ledger.

## Output

One row per marker, grouped by file:

`<file>:<line>, <what was simplified>. ceiling: <the limit named>. upgrade: <the trigger to revisit>.`

The convention is `ponytail: <ceiling>, <upgrade path>`, so pull the ceiling
and the trigger straight from the comment. Want an owner per row too? add
`git blame -L<line>,<line>`.

Flag the rot risk: any `ponytail:` comment that names no upgrade path or
trigger gets a `no-trigger` tag, those are the ones that silently rot.

End with `<N> markers, <M> with no trigger.` Nothing found: `No ponytail: debt. Clean ledger.`

## Boundaries

Reads and reports only, changes nothing. To persist it, ask and it writes the
ledger to a file (e.g. `PONYTAIL-DEBT.md`). One-shot. "stop ponytail-debt" or
"normal mode" to revert.

---

## 来源

本项目基于 [Ponytail](https://github.com/DietrichGebert/ponytail)（MIT License，作者 DietrichGebert）改写，
保留了原作者的版权声明（见 `LICENSE`）。核心思路一致，表述与结构按中文语境重写。

触发词：欠了什么、列出偷懒的地方、技术债清单
