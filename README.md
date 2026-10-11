# Reminder Intake · 对话提醒助手

A reusable Codex skill that notices actionable dates and unfinished follow-ups, then asks whether to add them to Apple Calendar, Google Calendar, or macOS Reminders.

一个可公开复用的 Codex 技能：识别对话中的截止日期、预约、后续任务和明确暂停的工作，适时询问是否加入日历或提醒事项。

## 能做什么

- 从对话提取事项、日期、通知时间、时区和重复规则。
- 根据任务类型提议日历或提醒事项，沿用已确认的偏好。
- 区分截止时间与提醒时间，核对相对日期与旧消息日期。
- 检查已有记录，避免重复创建；改时间时优先更新原提醒。
- 经用户授权后使用当前可用的连接器或应用工具创建，并核对实际结果。

## 安装到 Codex

将本仓库 `skills/reminder-intake` 文件夹复制到你的 Codex 技能目录，通常为 `~/.codex/skills/`。若使用自定义 `CODEX_HOME`，复制到该目录下的 `skills/`。

```sh
git clone https://github.com/dryan3333/reminder-intake-skill.git
mkdir -p "$HOME/.codex/skills"
cp -R reminder-intake-skill/skills/reminder-intake "$HOME/.codex/skills/"
```

如果已有同名技能，先比较内容，不要直接覆盖。安装后开启一个新对话，检查技能是否出现在可用列表。支持适时自动选择，也可以显式调用：

```text
使用 $reminder-intake 检查这段对话里有哪些时间节点需要提醒。
```

## 示例

| 对话 | 预期行为 |
|---|---|
| 周五前交新版图 | 提议截止任务提醒，核对日期和通知时点 |
| 先放着，明天下午继续 | 询问是否设置跟进提醒 |
| 在提醒事项里明天下午3点提醒我发合同 | 按明确授权执行，不额外发送合同 |
| 去年9月做过这个项目 | 不因历史日期触发提醒 |
| 已经设过了，改到5点 | 查找并更新原记录 |

## 实际能力与限制

这是指令型技能，不含常驻进程、日历API实现或后台聊天监听器。技能本身不能监测窗口停留时间，也不会自动扫描所有聊天。日历写入需要运行环境中可用且已授权的工具；没有写入工具时只准备草稿，不声称已创建提醒。

Apple Calendar、Google Calendar 与 macOS Reminders 是可选目标，并非本仓库已内置或测试的连接器。手机同步和系统通知依赖用户的账号、设备及通知设置。未授权时不会创建事件、邀请他人或复制整段聊天到日历。

## Structure

```text
skills/reminder-intake/
├── SKILL.md
└── agents/openai.yaml
```

The skill instructions and UI metadata are in Chinese. The skill is tool-agnostic: available connectors and app controls determine which destinations can actually be written to.

## Contributing

欢迎提交针对实际使用场景的 issue 或 pull request。请使用虚构示例，不提交聊天备份、账号标识、日历内容、密码或其他私人材料。

## License

MIT. See [LICENSE](LICENSE).
