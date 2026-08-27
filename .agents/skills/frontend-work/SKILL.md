---
name: frontend-work
description: 当 Codex 处理前端代码时使用，尤其是 Vue 组件、路由、store、缓存行为、UI 状态、composable、Vitest 测试、模板、样式、TypeScript 类型、构建链路或浏览器侧行为。若实现、排查、审查或验证涉及前端行为，应与当前阶段型 skill 一起使用，例如 build-work、debug-work、review-work 或 finish-work。
---

# 前端开发

使用这个 skill，让前端改动保持一致、隔离良好，并且可测试。

## 工作流程

1. 先识别精确的前端改动面：组件、路由、store、composable、缓存 key、事件、prop、emit 或测试。
2. 优先用精确名称搜索。使用组件名、路由路径、store action、事件名、测试名或可见文案，避免宽泛关键词。
3. 编码前先阅读同类组件、store、路由、样式和测试。
4. 匹配现有 UI 模式、数据流、命名、错误展示、加载状态和测试结构。
5. 将改动限制在用户要求的可见行为范围内。
6. UI、路由、缓存、状态或行为变化必须补充或更新 Vitest 用例。
7. 先运行最小有意义的测试；涉及模板、类型、路由或构建链路时再运行构建。

## Vue 与 Vitest

- Vue 组件测试必须启用自动卸载：

```ts
import { enableAutoUnmount } from '@vue/test-utils';
import { afterEach } from 'vitest';

enableAutoUnmount(afterEach);
```

- 如果组件可能在用例之间泄露状态，每轮用例都要清理缓存、全局 store、定时器、事件监听和 mock 的浏览器状态。
- 尽量测试公共行为，不测试实现细节。
- 每个组件测试用例聚焦一个行为。

## 验证

- 针对单个 Vitest 文件，运行 `npm run test -- <TestFile>.test.ts`。
- 改动涉及模板、TypeScript 类型、路由、打包配置、生成导入或构建链路时，运行 `npm run build`。
- 如果 Windows 下运行 `npm run test` 或 `npm run build` 时，在 `AppData\Roaming\nvm` 路径报 `EPERM`，提升权限重跑，并说明是 NVM 路径权限导致重试。
- 无法运行的验证必须说明原因。
