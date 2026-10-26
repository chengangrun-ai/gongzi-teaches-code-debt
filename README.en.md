English | [中文](README.md)

# gongzi-teaches-code-debt

An agent skill that collects every `ponytail:` shortcut comment in your code into one ledger: **what was simplified, what the ceiling is, when to upgrade**.

Read-only. Its job is to stop "later" from quietly becoming "never".

![欠账本：把 ponytail: 注释收成一张表](screenshots/hero.png)

## Why it exists

"We'll fix it later" is the most expensive sentence in engineering. Six months on, nobody remembers why it was written that way or when it will break — so it just stays.

The Ponytail convention is: every deliberate shortcut leaves a comment naming its ceiling and its upgrade path.

```python
# ponytail: UTF-8 only, switch to chardet detection when multi-encoding shows up
```

The comments exist. Nobody goes looking for them. This skill drags them all into the light.

## What it does

1. Greps the repo for the marker (skips `node_modules`, `.git`, and build output)

```bash
grep -rnE '(#|//) ?ponytail:' .
```

2. Each hit becomes one ledger row, grouped by file
3. Format: `<file>:<line>, <what was simplified>. ceiling: <the limit>. upgrade: <the trigger>.`
4. Flags the rot: any comment that names **no upgrade trigger** gets a `no-trigger` tag — those are the ones that silently rot

Ends with `<N> markers, <M> with no trigger.` Nothing found: `No ponytail: debt. Clean ledger.`

## What it looks like

```
src/parse.py:14, parses JSON only, no YAML. ceiling: all config is JSON.
  upgrade: when a .yaml config appears.  no-trigger
src/cache.py:33, in-memory cache, no eviction. ceiling: single process < 500MB.
  upgrade: wire in LRU past 300MB.
api/list.py:88, pagination loads the full table. ceiling: table < 10k rows.
  upgrade: cursor pagination past 10k rows.  no-trigger

3 markers, 2 with no trigger.
```

## Install

```bash
git clone https://github.com/chengangrun-ai/gongzi-teaches-code-debt.git \
  ~/.workbuddy-ai/skills/gongzi-teaches-code-debt
```

No dependencies, no pip install.

## Usage

```
/ponytail-debt
```

Or just ask: "what did ponytail defer?" / "list the shortcuts" / "show me the tech debt."

Want the ledger written to a file (say `PONYTAIL-DEBT.md`)? Ask for it and it will.

## Boundaries

- Reads and reports only, changes nothing.
- Only counts markers with a comment prefix — prose that merely mentions the convention stays out of the ledger.
- One-shot. To exit: say "normal mode" or `stop ponytail-debt`.

## The series

<p>
  <a href="https://github.com/chengangrun-ai/gongzi-teaches-code"><img src="https://raw.githubusercontent.com/chengangrun-ai/gongzi-teaches-code/main/screenshots/01-main.png" width="32%" alt="主技能"></a>
  <a href="https://github.com/chengangrun-ai/gongzi-teaches-code-review"><img src="https://raw.githubusercontent.com/chengangrun-ai/gongzi-teaches-code/main/screenshots/02-review.png" width="32%" alt="改动审查"></a>
  <a href="https://github.com/chengangrun-ai/gongzi-teaches-code-audit"><img src="https://raw.githubusercontent.com/chengangrun-ai/gongzi-teaches-code/main/screenshots/03-audit.png" width="32%" alt="整仓审计"></a>
</p>
<p>
  <a href="https://github.com/chengangrun-ai/gongzi-teaches-code-gain"><img src="https://raw.githubusercontent.com/chengangrun-ai/gongzi-teaches-code/main/screenshots/05-gain.png" width="32%" alt="效果看板"></a>
  <a href="https://github.com/chengangrun-ai/gongzi-teaches-code-help"><img src="https://raw.githubusercontent.com/chengangrun-ai/gongzi-teaches-code/main/screenshots/06-help.png" width="32%" alt="速查卡"></a>
</p>

> Five companions, one idea: the best code is the code you never wrote.

## Credits

Rewritten from [Ponytail](https://github.com/DietrichGebert/ponytail) (MIT, by DietrichGebert). The original copyright notice is preserved in `LICENSE`.

## License

MIT. See [LICENSE](LICENSE).

Made by [Gongzi](https://github.com/chengangrun-ai).
