# Agent Playbook

一套面向 Codex 的个人开发工作流：用 `AGENTS.md` 固定通用协作约定，用 Skills 按任务阶段提供可复用的执行方法。

## 包含内容

- `AGENTS.md`：通用的设计、检索、验证、文档和 Windows/Codex 环境约定。
- `.agents/skills/`：需求澄清、计划、实现、排查、审查、完成验证和架构改善等阶段型 Skills。
- `.agents/skills/backend-work/` 与 `frontend-work/`：后端和前端变更时配合阶段型 Skill 使用的领域约定。
- `.agents/skills/references/`：阶段型 Skills 共用的工作流等级和状态账本说明；它不是一个可直接调用的 Skill。

## 使用方式

将本仓库内容复制到目标项目根目录：

```text
your-project/
├─ AGENTS.md
└─ .agents/
   └─ skills/
```

启动 Codex 后，它会从项目根目录的 `AGENTS.md` 读取约定，并发现 `.agents/skills/*/SKILL.md` 中的 Skills。你可以在提示中显式使用 `$shape-work`、`$build-work`、`$review-work` 等，也可以让 Codex 按 Skill 的描述自动匹配。

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
