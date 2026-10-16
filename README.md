# Context Anchor｜让 AI 接得上之前的要求

一个用于保存和恢复任务上下文的通用 Agent Skill。适合长对话、阶段交接和换聊天继续工作。核心流程是：提取关键要求 → 保存接续记录 → 恢复时核对 → 交付前逐项检查。

它帮助降低遗漏，不是模型长期记忆插件；不能扩展上下文窗口、恢复没有提供的聊天历史，或保证 AI 永远不忘。没有后台服务、API 调用、遥测或自动同步。

## 快速体验

安装并让宿主识别后，发送：

> 使用 context-anchor：把当前任务的目标、硬性要求、我后来的修正和未完成事项整理成接续记录。有文件工具时保存到当前任务目录，否则给我可复制版本。

新聊天发送：

> 使用 context-anchor：读取这份接续记录，核对仍有效的要求，接着完成下一步。

需要同时提供记录文件或可读取的路径；仅仅新开聊天不会自动带入旧上下文。

## 安装

下载本仓库，将包含 `SKILL.md` 的整个文件夹命名为 `context-anchor`，复制到宿主的 Skill 目录。下列 `~` 表示你的用户主目录：

| 宿主 | 常见个人安装位置 | 注意 |
| --- | --- | --- |
| Codex | `~/.codex/skills/context-anchor/` | 按当前客户端的加载方式重新加载或开启会话；可用 `$context-anchor` 明确调用 |
| OpenClaw | `~/.openclaw/skills/context-anchor/` | 受代理的技能配置、白名单和权限影响，可用 `openclaw skills check` 排查 |
| 其他 Agent Skills 客户端 | 使用该产品文档指定的位置 | 格式支持不等于工具、权限和触发方式完全一致 |
| 普通聊天工具 | 把 `SKILL.md` 正文和记录作为输入 | 这是手动使用流程，不是原生安装，也不自动持久化 |

本项目只使用通用 Markdown 规则，不绑定某个 API 或命令名称。有文件工具时可持久化，没有时可复制记录。自动选用取决于宿主；需要可靠接续时显式调用并提供记录。

兼容性状态：已检查 Skill 结构；尚未在 OpenClaw 或其他独立客户端实机验证，不承诺所有平台即装即用。

## 文件说明

- `SKILL.md`：Skill 主入口。
- `references/checkpoint-template.md`：记录格式。
- `references/example.md`：虚构的用户修正示例。
- `EVALUATION.md`：手动行为验收场景与已完成检查。
- `LICENSE`：MIT 许可证。

## 记录与隐私

真实接续记录应存放在使用者的任务目录，默认 `.context-anchor/<task-id>.md`，不放在 Skill 安装目录。

本仓库的 `.gitignore` 排除了默认记录目录及常见本地秘密文件，但忽略规则不能保证无泄漏：它不作用于已经被 Git 跟踪的文件，也不能覆盖任意命名的自定义记录。公开前检查所有待上传文件，真实聊天、路径和密钥不要放入示例。

## 上传 GitHub

1. 在 GitHub 创建一个仓库，可命名为 `context-anchor`。
2. 上传本文件夹里的内容，让 `SKILL.md` 和 `README.md` 位于仓库根目录；不要只上传 ZIP，也不要上传整个个人工作目录。
3. 保留 MIT `LICENSE`。本包使用项目贡献者署名，你可以在发布前改成自己的公开署名。
4. 用虚构任务试用，并把遇到的具体遗漏和期望行为写入 Issue。真实对话先脱敏。

上传前请确认仓库只包含通用规则、文档和虚构示例。

## 设计依据

- [Agent Skills 格式规范](https://agentskills.io/specification)
- [OpenClaw Skills 文档](https://docs.openclaw.ai/skills)

## License

MIT。允许依照许可证使用、修改和分发；完整条款见 LICENSE。
