# Agent Playbook

一套面向 Codex 的个人开发工作流。`AGENTS.md` 记录通用协作约定，各项 skill 提供对应阶段的执行方法。

## 包含内容

- [项目约定](AGENTS.md)涵盖设计、检索、验证、文档和 Windows 环境。
- [开发流程入口](.agents/skills/SKILL.md)说明如何选择阶段和验证范围。
- `backend-work` 和 `frontend-work` 提供前后端领域约定，与当前阶段的 skill 配合使用。
- [md-work](.agents/skills/md-work/SKILL.md)提供 Markdown 写作和检查方法。

## 使用方式

将 `AGENTS.md` 和 `.agents/` 复制到目标项目根目录。项目已有 `AGENTS.md` 时，将需要的约定合并到原文件。

```text
your-project/
├─ AGENTS.md
└─ .agents/
   └─ skills/
```

启动 Codex 后，你可以在提示中显式使用 `$shape-work`、`$plan-work` 或 `$build-work`，也可以按任务匹配适用的 skill。

阶段型开发通常按以下顺序推进。

```text
shape-work → plan-work → build-work → review-work → finish-work
```

`shape-work` 负责对齐目标、范围和验收，再补齐架构、数据、状态和接口等技术决定。设计确认后，`plan-work` 将它拆成实施步骤和验证任务。遇到根因不明的故障，先用 `debug-work`。

## 设计原则

1. 通用规则留在这里，业务、客户、设备和仓库专属规则留在对应项目。
2. 先澄清并确认设计，再进行有行为影响的实现。
3. 用精确检索定位责任边界，避免无关的大范围搜索。
4. 以当前回合的验证证据为准，不把推测当成完成结论。
5. 不提交密钥、令牌、私人路径、内部地址、设备标识或项目专属数据。

## 维护

本仓库只收录可公开、跨项目复用的个人规则与 Skills。修改 Skill 时请遵守其中的阶段约定，并确认所有相对 `references/` 链接仍然有效。

## 许可证

[MIT License](LICENSE)。
