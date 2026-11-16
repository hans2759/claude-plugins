# claude-cleanup (plugin)

Claude 本机清理插件，支持 **macOS 与原生 Windows**：审计、备份、清理 Claude Code / Claude Desktop 的缓存、日志及可选登录状态。插件内含一个 skill（`claude-cleanup`），需要 **Python 3.10+**，无第三方依赖。

配套页面：[Claude 本机清理](https://www.agenai.cc/claude-cleanup)；源码仓库：<https://github.com/hans2759/claude-cleanup>。

## 这个插件会做什么（完整披露）

- **运行什么**：只运行插件自带的本地脚本（`skills/claude-cleanup/scripts/` 下的 Python / PowerShell 文件），处理本机 Claude 数据目录。先只读审计；实际清理必须由用户在可交互的终端里运行，检查完整路径清单并输入一次 `CONFIRM` 后才写盘。脚本没有跳过确认的参数，不自动结束 Claude 进程。
- **发送什么**：不联网、不上传、不发送任何数据。脚本是纯本地文件操作，无第三方依赖。
- **获取什么**：不下载任何东西。更新只来自插件市场或目录的正常版本更新。
- **改动范围**：第一个写操作是完整备份现存 `.claude` 与 `.claude.json`（Windows 逐文件 SHA-256 校验）。文件移除只进可恢复位置（macOS 的 `~/.Trash` 批次目录、Windows 的 `%USERPROFILE%\ClaudeCleanupTrash` 隔离目录），不永久删除。缓存与日志自动进入候选清单；本地 ID 轮换、登录凭据、Desktop 登录态、应用移除（仅 macOS）、台北时区（仅 macOS）、精简模式 `CLAUDE_CODE_SIMPLE` 都是风险操作，由用户逐项选择。
- **绝不动**：`projects`、`sessions`、`history.jsonl`、`skills`、`plugins`、`hooks`、`commands`、`agents`、`mcp-servers`、`CLAUDE.md`、设置文件与其他项目、Git 仓库、Codex 数据。遥测三键（`DISABLE_TELEMETRY`、`DISABLE_ERROR_REPORTING`、`CLAUDE_CODE_DISABLE_NONESSENTIAL_TRAFFIC`）逐值保留，不主动开关。

## 用法

安装后在 Claude Code 里调用 `/claude-cleanup:claude-cleanup`，或直接让 Claude 审计、清理本机 Claude 状态，它会按 SKILL.md 的流程走：先审计，再由用户在独立终端执行清理。正在运行的 Claude Code 只能启动只读审计，不能修改自己的配置。

手动运行（在插件目录 `skills/claude-cleanup/` 下）：

```bash
# macOS 只读审计
python3 scripts/claude_cleanup.py --audit
```

```powershell
# Windows 只读审计
& .\scripts\claude_cleanup_windows.ps1 -Audit
```

平台范围、白名单与恢复步骤见 skill 内的 `references/macos.md` 与 `references/windows.md`。

## 边界

用于本机隐私与排障。不删除云端聊天，不保证撤销所有登录方式或远程令牌，不用于规避封禁、支付检查、设备/IP 信誉或任何平台风控；清理不承诺防封。

## License

MIT，见 [LICENSE](LICENSE).
