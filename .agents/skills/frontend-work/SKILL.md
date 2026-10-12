---
name: frontend-work
description: "处理前端实现、排障或审查中的组件、状态、路由、样式和构建约束；配合当前阶段使用，验证跟随项目技术栈。"
---

# 前端开发

使用这个 skill，让前端改动保持一致、隔离良好，并且可测试。

## 前端关注点

公共定位、最小改动和验证范围遵循 [公共执行与证据规则](../SKILL.md#公共执行与证据规则)，实施或排障细节由当前阶段负责。

- 沿用项目实际技术栈、UI 模式、数据流、命名、错误展示和加载状态。
- 状态、路由、缓存和逻辑变化用相关行为测试覆盖；纯布局、配色和样式变化做必要渲染或截图检查，不机械添加 Vitest 用例。

## Vue 与 Vitest

- 已使用 Vue Test Utils 与 Vitest 的项目，组件测试必须启用自动卸载：

```ts
import { enableAutoUnmount } from '@vue/test-utils';
import { afterEach } from 'vitest';

enableAutoUnmount(afterEach);
```

- 如果组件可能在用例之间泄露状态，每轮用例都要清理缓存、全局 store、定时器、事件监听和 mock 的浏览器状态。
- 尽量测试公共行为，不测试实现细节。
- 每个组件测试用例聚焦一个行为。

## 验证

- 使用项目实际包管理器、测试和构建配置。若项目的 test 脚本使用 Vitest，可定向运行单文件；`npm run test -- <TestFile>.test.ts` 仅作为该配置下的示例。
- 涉及模板、类型、路由、打包配置、生成导入或构建链路时，按实际影响运行相关类型或构建检查；`npm run build` 仅适用于项目有该脚本的情况。
- 如果 Windows 下运行 `npm run test` 或 `npm run build` 时，在 `AppData\Roaming\nvm` 路径报 `EPERM`，提升权限重跑，并说明是 NVM 路径权限导致重试。
- 无法运行的验证必须说明原因。
