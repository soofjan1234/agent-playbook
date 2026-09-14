---
name: plan-work
description: "Use when an approved design needs to be converted into an implementation plan, task breakdown, sequencing, test strategy, migration steps, or risk-managed execution checklist. Also use when the user asks to write, save, or land something as plan.md; treat plan.md as shorthand for the default dated plan document unless an exact path or literal filename is specified."
---

# 实施计划

把已批准的系统设计转化成没有隐藏上下文的可执行工作。

## 核心关卡

1. 从已批准的系统设计开始；目标、范围或验收不清时退回 shape-work，架构、数据、状态或契约不清时退回 design-work。
2. 先映射相关文件、模块责任和测试接缝，再拆任务。
3. 每个任务形成可独立验证的纵向切片，而不是按技术层横向分割。
4. 明确文件路径、步骤、命令、预期结果和任务依赖。
5. 不写 `TODO`、`TBD`、“适当处理”或“与上一步类似”等占位内容。

## 按规模选择产物

| 场景 | 产物 |
| --- | --- |
| 小型明确改动 | 对话内短计划 |
| 中型需求 | 一份实施计划 |
| 大型明确需求 | 总计划＋按交付阶段拆分的子计划 |
| 大型且路线未知 | 调查地图；逐项消除未知后再规划 |

项目已配置 Issue 平台时，可以发布任务；否则默认保存在同一主题目录中，不强制引入外部平台。

## 技术选型依赖

如果计划依赖尚未决定或验证的技术选型，不得在计划中代替设计阶段作决定，应退回 design-work 补齐候选、事实依据、验证条件和选择结论。

## 任务格式

每项任务至少包含：

- 创建、修改和测试的精确文件。
- 先写哪个失败测试，以及预期为什么失败。
- 最小实现步骤。
- 目标测试、相关测试和最终验证命令。
- 阻塞它的前置任务。

计划与设计归属同一主题。MVP 优先使用 `docs/mvp/plan.md`；后续变更优先使用 `changes/<topic>/plan.md`。项目约定、既有主题目录或用户指令可覆盖。

复杂计划按可独立验证的交付结果拆分：总计划只保留阶段目标、依赖、顺序、子计划入口和整体验收入口；子计划记录本阶段文件、关键函数、行为变化、测试和通过条件。不要按 controller、service、database 等技术层拆分。

用户说“写到 plan.md”、“落成 plan.md”或类似简写时，按默认日期主题命名保存；只有用户明确给出完整路径或明确要求文件名字面叫 `plan.md`，才使用字面文件名。

正式计划落盘后，按 [状态账本规范](../references/status-ledger.md) 创建或更新 `待实现` 工作项的主要文档、下一步和日期。没有设计记录时由计划首次创建记录；已有记录时不得为同一工作项创建新的月度记录。

## 自检

1. 每项已批准设计和整体验收标准都映射到至少一个任务或验证。
2. 名称、路径、类型、函数和命令前后一致。
3. 没有占位内容、范围漂移或无法验证的任务。
4. 计划可交给没有当前会话历史的 agent 执行。

## 红旗

- 设计未批准就把猜测固化成计划。
- 在计划中重新定义需求范围、系统架构或接口契约。
- 一个任务同时横跨多个独立子系统。
- 用文件层级代替用户可观察的纵向行为。
- 计划只有动作，没有测试和预期结果。
