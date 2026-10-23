# 公子教代码做事 · 欠账本

【技术债账本】把代码里所有 ponytail: 简化注释收集成一张表，逐条列出 「简化了什么 / 上限在哪 / 什么时候该升级」，防止「以后再说」变成「永远不做」。 只读不改。触发词：/ponytail-debt、ponytail 欠了什么、列出偷懒的地方、 技术债清单。

## 📺 看看效果

![ponytail-debt](screenshots/hero.png)

> 把 `screenshots/hero.png` 换成真实效果图（建议 1200px 宽、不超过 400KB）

## What This Does

【技术债账本】把代码里所有 ponytail: 简化注释收集成一张表，逐条列出 「简化了什么 / 上限在哪 / 什么时候该升级」，防止「以后再说」变成「永远不做」。 只读不改。触发词：/ponytail-debt、ponytail 欠了什么、列出偷懒的地方、 技术债清单。

### Key Features

- Scan
- Output
- Boundaries

## Installation

### WorkBuddy

```bash
git clone https://github.com/<you>/ponytail-debt.git ~/.workbuddy-ai/skills/ponytail-debt
pip install -r ~/.workbuddy-ai/skills/ponytail-debt/requirements.txt
```

### Claude Code / 其他 Agent

```bash
mkdir -p ~/.claude/skills/ponytail-debt
cp -R SKILL.md README.md requirements.txt scripts references \
      ~/.claude/skills/ponytail-debt/
```

把仓库链接丢给 agent，它会按 `SKILL.md` 加载所需文件。

## Usage

触发词：**/ponytail-debt、ponytail 欠了什么、列出偷懒的地方**

## Architecture

| 文件 | 作用 |
|---|---|
| `SKILL.md` | 触发条件与流程 |

## Requirements

- Python 3.9+
- `pip install -r requirements.txt`

## Credits

基于 [Ponytail](https://github.com/DietrichGebert/ponytail)（MIT，作者 DietrichGebert）改写 · 中文版维护 [@chengangrun-ai](https://github.com/chengangrun-ai)

Created by 公子 · [@你的GitHub](https://github.com/).

## License

MIT — Use it, modify it, share it.
