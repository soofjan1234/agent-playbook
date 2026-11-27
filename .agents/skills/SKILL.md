---
name: my-skills
description: "Use when Codex needs to choose the right development workflow stage and rigor for a request, especially for aligning product requirements, designing systems, planning, building, debugging, reviewing, validating, or improving architecture. Route unclear goals, scope, acceptance, or implementation design to shape-work before planning or implementation."
---

# 我的开发工作流

用最小但足够可靠的流程推进开发。只负责判断强度和路由，不在这里重复子 skill 的详细规则。

创建或实质修改 Markdown 文档时，必须配合使用 [md-work](md-work/SKILL.md)；它负责写作质量，不替代主阶段流程或新增审批。纯聊天回答和小幅文字修正不额外加载。

## 核心关卡

1. 用户指令高于本 skill；项目内 `AGENTS.md`、`CLAUDE.md` 和既有约定高于通用流程。
2. 先判断任务强度，再选择当前阶段的一个主 skill；不要同时启动多个重叠流程。
3. 目标、范围、验收或关键方案未明确时进入 `shape-work`；未知根因的故障先进入 `debug-work`。
4. 先确认简洁的总体设计，再调查技术缺口、按需用 `tmp-discuss.md` 集中讨论；用户明确确认正式写入后整理技术专项，再进入计划或实现。总体设计确认不等于技术方案全部确认，讨论稿不代表正式设计；已有授权不重复询问。文档组织遵循[文档管理规则](references/documentation-policy.md)。
5. 没有当前回合的新鲜验证证据，不得声称完成、修复或通过。
6. 开始工作流时先读取当前主题的 `status.md`，分别检查设计确认状态与计划执行状态；项目已有账本或 Issue 约定时遵循该约定。

## 状态账本

MVP 默认使用 `docs/mvp/status.md`，后续变更使用 `docs/changes/YYYY-MM-DD-<主题>/status.md`。日期是主题首次创建日；后续更新复用同一目录，不因跨月新建平行主题。每个主题用设计表和计划表分别记录确认结论、执行进度与完成结果，表内写文档名而非链接。字段和状态转换见 [references/status-ledger.md](references/status-ledger.md)。

状态账本是工作状态的唯一来源；不要向每份沉淀文档添加状态头部。没有持久化文档的轻量任务不强制登记。

## 强度分级

| 等级 | 场景 | 行为 |
| --- | --- | --- |
| 0 对话 | 解释、比较、建议、非修改讨论 | 直接回答，不加载开发流程 |
| 1 轻量 | 单文件、明显配置或文档、小范围修复 | 最短检查表、精确定位、一次针对性验证 |
| 2 标准 | 正常功能、行为变化、测试、重构 | 使用当前阶段的完整子 skill |
| 3 严格 | 跨模块、迁移、权限、安全、并发、生产故障 | 设计、计划、实现、审查和验证完整串联 |

出现公共 API、数据结构、权限、持久化、核心用户流程、多子系统或非显然测试失败时，至少提升一级。详细判断见 [references/workflow-levels.md](references/workflow-levels.md)。

## 路由

| 当前需要 | 主 skill |
| --- | --- |
| 用非技术语言解释问题、解决结果或任务结论，并形成可汇报摘要 | `brief-work` |
| 对齐需求、范围、验收并确定实现方案，包括架构、数据、状态和接口 | `shape-work` |
| 把已批准设计变成任务或实施步骤 | `plan-work` |
| 按明确需求或计划实现 | `build-work` |
| 定位 Bug、失败、异常或性能回退 | `debug-work` |
| 审查变更或处理审查意见 | `review-work` |
| 验证完成、合并、PR 或移交 | `finish-work` |
| 统一领域语言、改善模块边界和接口 | `shape-work` |
| 复盘项目任务并创建仓库级沉淀 | `project-retrospective` |

实现、调试、审查或完成验证若涉及后端代码，应同时使用 `backend-work`。
实现、调试、审查或完成验证若涉及前端代码，应同时使用 `frontend-work`。

完成当前关卡后才能路由到下一阶段。进入任务时先读取项目文档入口和当前主题所需材料；详细规则见 [文档管理规则](references/documentation-policy.md)。事实能从代码库查到时直接调查；只有需要取舍的决策才询问用户。

## 轻量路径

1. 用一句话确认目标。
2. 用精确文件、函数、事件或测试名定位责任位置。
3. 做最小安全改动。
4. 运行最具体的有效验证。
5. 报告改动、证据和残余风险。

不要为一级任务创建设计文档、宽泛计划、worktree 或多轮审查，除非用户明确要求或风险升级。

## 红旗

- 因为“流程完整”而同时加载所有子 skill。
- 未理解任务就创建规格或开始编码。
- 同一阶段重复生成两份设计、计划或审查。
- 为互相依赖或会修改同一文件的工作启用并行。
- 用“应该、可能、看起来”代替验证证据。
