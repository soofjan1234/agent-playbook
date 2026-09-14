# 工作流强度与阶段转换

## 升级信号

- 修改公共 API、数据库结构、路由、权限、持久化或核心用户流程。
- 第一次精确定位无法找到明确责任文件。
- 目标测试或构建出现非显然失败。
- 需要修改多个子系统或协调多种运行环境。
- 涉及安全、资金、并发、迁移、破坏性操作或生产事故。
- 用户明确要求规格、计划、审查或长期文档。

## 降级原则

- 不改变代码或外部状态的解释与比较保持零级。
- 单文件、所有者明确、验证命令明确的任务默认一级。
- 没有具体风险时，不创建规格、worktree、多 agent 流程或正式审查。
- 即使降级，也不得跳过设计批准、根因调查和完成前验证等安全关卡。

## 阶段转换

```text
模糊需求 → shape-work → design-work → plan-work → build-work → review-work → finish-work
已明确小改 → build-work → finish-work
未知故障 → debug-work → build-work → finish-work
已有系统的架构问题 → improve-design → plan-work
```

shape-work 只对齐做什么及何时算成功；design-work 决定如何实现。design-work 发现范围不可行时返回 shape-work，plan-work 发现契约或架构未决定时返回 design-work。任何阶段发现关键假设不成立时，返回产生该假设的上游阶段，不要在下游用补丁掩盖。
