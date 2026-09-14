---
name: design-work
description: "Use when product scope and overall acceptance criteria are already aligned and the system implementation needs to be designed, including architecture, data models, state flows, API contracts, failure handling, compatibility, technical choices, and validation of key risks. Do not use it for initial requirement discovery or file-by-file implementation planning."
---

# 系统设计

把已确认的需求范围转化成可审批、可验证的系统实现方案。

<HARD-GATE>
关键架构、数据、状态或接口契约未呈现且未获得用户明确批准前，不得进入实施计划或实现。
</HARD-GATE>

## 核心关卡

1. 读取已确认的范围、整体验收标准、项目约定和最相关的当前实现；文档组织遵循 [文档管理规则](../references/documentation-policy.md)。
2. 区分当前事实、设计假设和用户决策。范围仍有关键缺口时返回 shape-work。
3. 根据需求覆盖组件架构、数据模型、状态流、接口契约、错误处理、恢复、兼容与观测；没有相关性的部分不机械展开。
4. 对会改变成本、边界或长期维护方式的选择给出 2～3 个实质方案及取舍，并明确推荐项。
5. 用关键风险对应的验证方法检验方案；技术选型需要事实搜索或实验时，先定义候选、条件和成功标准。
6. 以与复杂度相称的篇幅呈现设计，获得用户批准后交给 plan-work。

## 文档职责

- 总体设计串起完整核心流程，使读者无需跳转就能理解系统如何工作；API、数据和选型细节通过链接进入专项正文。
- 同一契约只在一个权威正文维护。设计稿说明拟议行为，当前参考说明已交付行为，必须标明适用性。
- MVP 优先使用 docs/mvp/design.md 及同组专项文档；后续变更优先使用同一 changes/<topic>/ 目录。项目约定或用户路径优先。
- 用户要求写入 design.md 时，按项目约定和既有主题目录选择路径；只有明确指定完整路径或字面文件名时才照字面创建。
- 已有相关设计时更新原文，不新建平行方案。关键长期取舍才建立 ADR，并从设计引用。
- 持久化设计时按 [状态账本规范](../references/status-ledger.md) 创建或更新同一工作项。

## 设计内容

按任务需要选择以下内容：

- 系统边界、组件职责、依赖方向和核心数据流。
- 领域对象、数据关系、约束、事务与生命周期。
- 状态、事件、转换条件、超时、取消、重试和恢复。
- API 或消息契约、错误、幂等、并发、权限和兼容行为。
- 配置、部署、迁移、回滚、观测与安全边界。
- 候选方案、选择理由、代价、待验证假设和受影响的当前文档。

## 与相邻阶段的边界

- shape-work 决定做什么、不做什么及何时算成功；本 skill 决定系统如何满足这些要求。
- plan-work 决定修改哪些文件、按什么顺序执行和运行哪些测试；本 skill 不提前编写逐文件任务清单。
- 设计发现目标、范围或验收不可行时，只将受影响部分退回 shape-work 确认。
- 计划或实现发现未决定的架构、数据、状态或契约问题时，返回本 skill 更新设计并重新批准。
- 已有系统的领域语言和模块边界专项改进可使用 improve-design；涉及新需求交付时仍由本 skill 维护该主题的系统设计。

## 红旗

- 未确认需求范围就开始选择架构或接口。
- 用目录树、类名和文件清单代替系统行为与边界。
- 总体设计复制完整 API 和数据库字段，导致多份正文漂移。
- 只描述正常路径，没有错误、状态、兼容、恢复或验证边界。
- 把关键设计决定留给 plan-work 或实现阶段自行判断。
- 为了文档完整机械创建空章节、空文件或无关方案。
