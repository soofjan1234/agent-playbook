---
name: token-retrospective
description: "Use to retrospect why an agent turn consumed too much time, tokens, tool calls, context, or exploratory work, especially before turning the lesson into AGENTS.md or skill guidance."
---

# Token 复盘

## 目标

从一次高成本回合里提炼最小、可复用的持久经验。除非证据不足，否则不要重新运行大范围搜索。

## 检查清单

1. **说清触发原因：** 是什么让这轮变长？例如：目标文件不明确、缺少本地 fixture、看错来源、重复验证、搜索过宽、工具失败、沙箱/网络提权、或假设过时。
2. **区分必要与浪费：** 保留真正改变答案的工作；标出只是为了弥补可避免含糊而产生的工作。
3. **找出最早的更省分支：** 找到第一个本可以通过文件检查、一个澄清问题、更窄命令或本地 fixture 来缩短路径的时刻。
4. **提炼一条规则：** 写出一条能防止复发的持久指令。习惯类问题优先写入仓库/全局 `AGENTS.md`；可复用流程才适合做成 skill。
5. **保持规则很小：** 一句话或一个短 bullet。不要把事后复盘叙事写进持久上下文。

## 输出格式

```text
为什么耗时：
- ...

下次更省：
- ...

AGENTS.md 候选：
- ...

skill.md 候选：
- ...
```

## 常见值得加入的规则

- 在进行网络或远程调试前，先检查是否有本地 fixture，并询问是否应该使用它们。
- 复盘失败时，先打印数量和第一个差异位置，而不是直接倾倒巨大值。
- 面对宽泛问题时，先给一个紧凑的默认回答，再询问是否需要检查本地文件。
- 不要把终端乱码复制进源文件；使用明确 UTF-8 读取，或用稳定锚点定位。
