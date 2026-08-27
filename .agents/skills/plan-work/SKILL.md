---
name: plan-work
description: "Use when an approved design needs to be converted into an implementation plan, task breakdown, sequencing, test strategy, migration steps, or risk-managed execution checklist. Also use when the user asks to write, save, or land something as plan.md; treat plan.md as shorthand for the default dated plan document unless an exact path or literal filename is specified."
---

# 规格与实施计划

把已确认的目标转化成没有隐藏上下文的可执行工作。

## 核心关卡

1. 从已批准设计或具体需求开始；存在关键歧义时退回 `shape-work`。
2. 先映射相关文件、模块责任和测试接缝，再拆任务。
3. 每个任务形成可独立验证的纵向切片，而不是按技术层横向分割。
4. 明确文件路径、步骤、命令、预期结果和任务依赖。
5. 不写 `TODO`、`TBD`、“适当处理”或“与上一步类似”等占位内容。

## 按规模选择产物

| 场景 | 产物 |
| --- | --- |
| 小型明确改动 | 对话内短计划 |
| 中型需求 | 规格＋实施计划 |
| 大型明确需求 | 规格＋纵向任务＋实施计划 |
| 大型且路线未知 | 调查地图；逐项消除未知后再规划 |

项目已配置 Issue 平台时，可以发布规格和任务；否则默认保存在仓库文档中，不强制引入外部平台。

## 技术选型依赖

如果计划依赖尚未验证的技术选型，必须先引用 `shape-work` 产出的候选矩阵、事实搜索结果、truth test 和不测方案理由；缺少这些证据时，不得拆实施任务，应退回 `shape-work` 补齐。

## 任务格式

每项任务至少包含：

- 创建、修改和测试的精确文件。
- 先写哪个失败测试，以及预期为什么失败。
- 最小实现步骤。
- 目标测试、相关测试和最终验证命令。
- 阻塞它的前置任务。

默认将正式计划保存到 `docs/my-skills/plans/YYYY-MM-DD-<topic>.md`，项目约定或用户指令可覆盖。

用户说“写到 plan.md”、“落成 plan.md”或类似简写时，按默认日期主题命名保存；只有用户明确给出完整路径或明确要求文件名字面叫 `plan.md`，才使用字面文件名。

正式计划落盘后，按 [状态账本规范](../references/status-ledger.md) 创建或更新 `待实现` 工作项的主要文档、下一步和日期。没有设计记录时由计划首次创建记录；已有记录时不得为同一工作项创建新的月度记录。

## 自检

1. 每个需求都映射到至少一个任务。
2. 名称、路径、类型、函数和命令前后一致。
3. 没有占位内容、范围漂移或无法验证的任务。
4. 计划可交给没有当前会话历史的 agent 执行。

## 红旗

- 设计未批准就把猜测固化成计划。
- 一个任务同时横跨多个独立子系统。
- 用文件层级代替用户可观察的纵向行为。
- 计划只有动作，没有测试和预期结果。
