---
name: shape-work
description: "Use when the user proposes a new feature, behavior change, experiment, observability setup, API contract, integration path, or any not-yet-approved approach that needs goals, constraints, success criteria, validation, risks, and key decisions clarified before implementation. Also use when the user asks to write, save, or land something as design.md; treat design.md as shorthand for the default dated design document unless an exact path or literal filename is specified."
---

# 澄清需求与设计

把模糊想法变成得到用户批准的设计。

<HARD-GATE>
设计未呈现且未获得用户明确批准前，不得写实现代码、搭建项目骨架或改变业务行为。
</HARD-GATE>

## 核心关卡

1. 先读取最相关的项目事实、现有行为和约定。
2. 明确目标、非目标、约束、成功标准和验证方式。
3. 事实自行调查；决策一次只问一个，并给出推荐答案和理由。
4. 提供 2～3 个有实质差异的方案及取舍。
5. 以与任务规模相称的篇幅呈现推荐设计，并等待批准。

## 持久化设计文档

当需求涉及新功能、接口契约、观测链路、安全边界、流程或 skill 修改，且后续可能反复修订时，优先把设计写入项目文件，避免后续 agent 重新生成游离方案。

- 项目功能设计优先使用 `docs/my-skills/designs/YYYY-MM-DD-<topic>-design.md`；如果已有相关设计文档，更新原文件对应小节，不新建平行文档。
- 用户说“写到 design.md”、“落成 design.md”或类似简写时，按默认日期主题命名保存；只有用户明确给出完整路径或明确要求文件名字面叫 `design.md`，才使用字面文件名。
- skill 修改先在对话中呈现简要设计；获批后直接更新目标 `SKILL.md`。只有修改范围较大或需要多轮审查时，才另建临时设计文档。
- 文档保持短而可改，通常包含：背景与当前事实、目标 / 非目标、方案、接口或行为契约、风险与安全边界、验证标准、待确认问题。
- 用户明确只要口头设计、任务很小且不会跨回合漂移时，可以不落文件，但要说明这个判断。
- 持久化设计时按 [状态账本规范](../references/status-ledger.md) 创建或更新 `待实现` 工作项；若计划或交接文档已经创建记录，则更新同一记录。

## 技术选型前置检查

当任务涉及替换核心技术、选择库/框架/算法/存储/搜索方案时，先冻结候选矩阵，不要直接进入实现或 benchmark。

必须先做事实搜索，覆盖官方文档、主仓库、issue/讨论和项目内已有实验，给出可能遗漏的候选技术建议。若网络不可用，说明缺口并标记需要补查。

候选矩阵至少包含：方案名称、来源链接或本地路径、是否仍维护、是否纯 Go/是否 CGO、是否已有项目集成或 adapter、部署风险、性能风险、可控性、与当前业务场景的匹配度、是否测试以及不测试的理由。

## 快速路径

适用于一级任务：

1. 只读取最窄的相关事实。
2. 最多询问一个真正阻塞的问题。
3. 判断是否需要持久化设计文档；需要时先说明建议路径。
4. 简述目标、方案、受影响行为和验证方法。
5. 询问：“这个设计是否符合你的预期？”

不要创建正式规格或计划。

## 完整路径

适用于二至三级任务：

1. 探索现有结构、相邻实现、领域术语和历史决策。
2. 沿设计决策树逐项确认，不要一次抛出多个无关问题。
3. 比较方案并明确推荐项。
4. 创建或更新持久化设计文档，优先改已有相关文档的对应小节。
5. 呈现完整设计摘要：数据流、接口、状态、错误处理、兼容性、测试和发布影响，并链接设计文件。
6. 需要统一术语或记录关键决策时，调用 `improve-design` 更新 `CONTEXT.md` 或 ADR。
7. 获得批准后，将结果交给 `plan-work`。

## 红旗

- 以“需求很简单”为由跳过成功标准。
- 先写代码再让用户确认设计。
- 询问能从仓库直接找到的事实。
- 只给一个方案，却把它包装成没有选择的结论。
- 追问没有影响实现、验证或取舍的细节。
- 未考虑正确性与规模
- 多点设计只留在聊天里，导致后续回合或其它 agent 重新生成不一致方案。
