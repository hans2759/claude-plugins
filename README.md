# hans2759-plugins

Claude Code 插件市场（自建）：一个 git 仓库即一个市场，无注册、无审核。把本仓库推到 GitHub 后，用户两条命令即可添加与安装。

建议仓库名：`hans2759/claude-plugins`（市场名 `hans2759-plugins` 与仓库名相互独立，改仓库名不影响已备好的任何文件）。

## 用户怎么装

```bash
# 添加市场（一次性）
claude plugin marketplace add hans2759/claude-plugins

# 安装插件
claude plugin install claude-cleanup@hans2759-plugins
```

会话内也可以用 `/plugin` 完成同样两步。更新：`claude plugin update claude-cleanup@hans2759-plugins`（或在 `/plugin` 里给本市场打开自动更新）。

## 当前插件

| 插件 | 说明 |
| --- | --- |
| `claude-cleanup` | Claude 本机清理 skill：审计、备份、清理 Claude Code / Claude Desktop 在 macOS 与原生 Windows 上的缓存、日志与可选登录状态。白名单脚本、先完整备份、一次 `CONFIRM` 才写盘、不联网。 |

## 维护说明（仓库主人看）

- 插件清单在 `plugins/<name>/.claude-plugin/plugin.json`，市场清单在 `.claude-plugin/marketplace.json`；两处 `name` 必须一致（现均为 `claude-cleanup`）。
- 发新版：改插件内文件后，把 `plugin.json` 的 `version` 往上加一位再推送；用户侧靠版本号识别更新，不要改插件 `name`。
- 推送前在本机跑一次官方校验：`claude plugin validate .`（在仓库根目录）。预期结果是 `Validation passed`，可能带一条关于插件名含 "claude" 一词的 warning，属已知项，不影响安装与加载。
- 同一个插件包（`plugins/claude-cleanup/`）也是提交 Anthropic 官方目录（claude.ai/directory/manage，plugin bundle 形态）的同一份材料，不要另做一份。

## License

MIT，见 [LICENSE](LICENSE).
