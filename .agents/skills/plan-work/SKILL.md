---
name: plan-work
description: "Use when an approved design needs to be converted into an implementation plan, task breakdown, sequencing, test strategy, migration steps, or risk-managed execution checklist. Also use when the user asks to write, save, or land something as plan.md; treat plan.md as shorthand for the default dated plan document unless an exact path or literal filename is specified."
---

# 实施计划

把已批准的系统设计转化成没有隐藏上下文的可执行工作。

计划文档的表达和组织遵循 [文档管理规则](../references/documentation-policy.md)。

创建或实质修改 Markdown 文档时，必须同时使用 [md-work](../md-work/SKILL.md)，落实写入前的组织与写后精简检查；纯聊天回答或小幅文字修正不额外加载。

## 核心关卡

1. 从已确认的总体设计及本次实施所需的技术方案开始，沿总体设计链接检查 `architecture/` 和已有专项；不能只凭 `design.md` 获批就进入计划。目标、范围、验收、架构、数据、状态、权限或契约存在影响本次实施的未决项时，退回 shape-work，只补充未决定部分。简单任务无需强制创建专项文档。
   `tmp-discuss.md` 是讨论工作稿，不能代替正式技术设计；使用该工作稿的任务，相关结论须经用户确认并授权整理到正式文档后，才进入实施计划。
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

如果计划依赖尚未决定或验证的技术选型，不得在计划中代替设计阶段作决定，应退回 shape-work 补齐候选、事实依据、验证条件和选择结论。

## 任务格式

每项任务至少包含：

- 创建、修改和测试的精确文件。
- 先写哪个失败测试，以及预期为什么失败。
- 最小实现步骤。
- 目标测试、相关测试和最终验证命令。
- 阻塞它的前置任务。

计划与设计归属同一主题。MVP 优先使用 `docs/mvp/plan.md`；后续变更保存在 `changes/YYYY-MM-DD-<topic>/plans/`，复用主题创建时确定的日期目录。已有主题使用 `plan/` 时沿用该目录；项目约定或用户明确指定的路径、文件名优先。

`changes/` 下计划目录中的新文件使用 `i.xxx.md`：`i` 为从 1 开始的整数，`xxx` 为简短主题，例如 `1.sdk-integration.md`。新增前检查同一目录的编号，取最大编号加 1；总计划和子计划都按此规则命名。更新原文保留编号，不自动重排或重命名旧文件。

复杂计划按可独立验证的交付结果拆分：总计划只保留阶段目标、依赖、顺序、子计划入口和整体验收入口；子计划记录本阶段文件、关键函数、行为变化、测试和通过条件。不要按 controller、service、database 等技术层拆分。

用户说“写到 plan.md”、“落成 plan.md”等简写时，按以上主题目录和编号规则保存；只有明确给出完整路径或要求文件名字面叫 `plan.md`，才使用指定文件名。

正式计划落盘后，按 [状态账本规范](../references/status-ledger.md) 在主题计划表登记文档名、`待实现` 状态、完成结果、下一步和日期。已有计划更新原行，跨月或跨年继续维护同一主题文件。

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
