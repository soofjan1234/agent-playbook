---
name: improve-design
description: "Use when Codex needs to unify domain language, record architecture decisions, improve module boundaries, design or refine interfaces, or make code easier to test and navigate."
---

# 领域与架构设计

让业务语言、模块边界和代码接口表达同一个模型。

## 核心关卡

1. 先读取现有 `CONTEXT.md`、ADR、公共接口和调用关系。
2. 区分领域概念、实现细节和含糊代称；同一概念只保留一个稳定名称。
3. 用边缘场景检验术语和边界，而不是只整理词汇表。
4. 优先设计深模块：用小而稳定的接口隐藏大量内部行为。
5. 明确测试接缝、所有权和数据流；重构前呈现方案并获得批准。

## 领域建模

- 记录核心术语、定义、非例和关系。
- 发现术语冲突时立即澄清，不在变量、文档和接口中继续扩散。
- 稳定事实写入 `CONTEXT.md`；具有取舍和后果的决定写入 ADR。
- 单体项目默认单一上下文；只有真实大型多领域仓库才建立上下文地图。

## 架构改进

1. 找出调用者必须理解过多内部细节的浅模块。
2. 分析变化经常跨越哪些文件和边界。
3. 提出 2～3 个接口或模块归属方案。
4. 评价复杂度隐藏、局部性、测试性、迁移成本和兼容风险。
5. 选择最小可验证切片交给 `shape-work` 或 `plan-work`。

仅当多个架构候选的关系难以用文字比较时才制作可视化报告。

## 红旗

- 把“service”“manager”“component”等泛词当作领域语言。
- 为了层次感增加只转发调用的浅模块。
- 在没有调用关系证据时大规模移动文件。
- 用重命名掩盖仍未解决的领域歧义。
- 架构扫描结束后直接重构，未经过用户设计批准。
