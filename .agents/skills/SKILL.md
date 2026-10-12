---
name: my-skills
description: "Use when Codex 需要为开发请求选择流程强度和当前阶段，尤其适用于需求设计、计划、实现、排障、审查、验证与架构改进。"
---

# 我的开发工作流

用最小但足够可靠的流程推进开发。只负责判断强度和路由，不在这里重复子 skill 的详细规则。

## 核心关卡

1. 用户指令高于本 skill；项目内 `AGENTS.md`、`CLAUDE.md` 和既有约定高于通用流程。
2. 先判断任务强度，再选择当前阶段的一个主 skill；不要同时启动多个重叠流程。
3. 模糊的新功能先进入 `shape-work`；范围已确认且需要技术方案时进入 `design-work`；未知根因的故障先进入 `debug-work`。
4. 设计确认的适用范围与批准复用遵循 `AGENTS.md`；新功能、观测链路、接口契约、流程和 skill 修改仍须先呈现简要设计并获批准，轻量路径不能绕过此要求。
5. 完成、修复和通过的结论须符合下述证据规则。

## 公共执行与证据规则

- 精确定位相关文件、函数或事件，阅读附近实现和同类模式；保持既有边界，只做本次授权范围内的最小安全改动。
- 验证选择遵循 `AGENTS.md` 和当前阶段：先定向验证，完成时做最终相关验证；只有新失败或跨组件风险才增加相邻验证。
- 证据必须对应当前产物版本、相关输入和运行环境。三者未变化且证据可核验时，可以复用并说明验证时间；发生变化时重跑受影响检查。不得把旧结果冒充新运行结果。
- 证据能支持的结论才可声称成立；lint 不代替行为测试，一次成功运行不证明长期稳定性。

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
| 澄清需求、比较方案、批准设计 | `shape-work` |
| 把已确认范围转成架构、数据模型、状态流和接口契约 | `design-work` |
| 把设计变成规格、任务或实施步骤 | `plan-work` |
| 按明确需求或计划实现 | `build-work` |
| 定位 Bug、失败、异常或性能回退 | `debug-work` |
| 审查变更或处理审查意见 | `review-work` |
| 验证完成、合并、PR 或移交 | `finish-work` |

常规阶段顺序：`shape-work → design-work → plan-work → build-work → review-work → finish-work`。

完成当前关卡后才能路由到下一阶段。事实能从代码库查到时直接调查；只有需要取舍的决策才询问用户。

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


## 子 skills 的位置与加载

本目录集中保存个人开发 skills。表中的路径相对于本文件；选定阶段后读取对应 `SKILL.md`，不要一次加载全部内容。若当前会话未单独列出子 skill，直接按这些路径读取即可。用户显式指定子 skill 时也按相同路径加载。

| Skill | 入口 |
| --- | --- |
| `backend-work` | [backend-work/SKILL.md](backend-work/SKILL.md) |
| `brief-work` | [brief-work/SKILL.md](brief-work/SKILL.md) |
| `build-work` | [build-work/SKILL.md](build-work/SKILL.md) |
| `debug-work` | [debug-work/SKILL.md](debug-work/SKILL.md) |
| `defense-work` | [defense-work/SKILL.md](defense-work/SKILL.md) |
| `design-work` | [design-work/SKILL.md](design-work/SKILL.md) |
| `finish-work` | [finish-work/SKILL.md](finish-work/SKILL.md) |
| `frontend-work` | [frontend-work/SKILL.md](frontend-work/SKILL.md) |
| `fuck-u-code-analysis` | [fuck-u-code-analysis/SKILL.md](fuck-u-code-analysis/SKILL.md) |
| `plan-work` | [plan-work/SKILL.md](plan-work/SKILL.md) |
| `project-retrospective` | [project-retrospective/SKILL.md](project-retrospective/SKILL.md) |
| `review-work` | [review-work/SKILL.md](review-work/SKILL.md) |
| `shape-work` | [shape-work/SKILL.md](shape-work/SKILL.md) |
| `token-retrospective` | [token-retrospective/SKILL.md](token-retrospective/SKILL.md) |

`backend-work`、`frontend-work` 按技术领域配合当前阶段；`brief-work` 用于已验证技术结论的说明；`defense-work` 保持其手动调用条件；代码质量扫描和复盘按对应 skill 的触发条件使用。共享规范位于 `references/`，子 skill 专属资料位于各自目录。
