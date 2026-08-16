# 定时投递设置

仅在用户明确要求定时或周期性投递时读取并执行本文件。

## 需要确认的设置

一次性确认：

- 每天或每周
- 投递时间与 IANA 时区
- 周报对应星期
- 当前对话、Telegram 或 Email
- 中文、英文或中英双语
- 产品推荐重点人群，例如产品经理、开发者或内容创作者

## ChatGPT Work

优先使用 Automations 创建周期任务。任务提示应要求运行 `follow-builders` 的准备脚本，核验最新 AI 市场情况，生成 Builder 摘要，推荐 2–3 款带官方链接的产品，并给出 AI 产品经理行动建议。使用用户个人时区。创建成功后，以工具返回结果为准。

## OpenClaw

先检测平台：

```bash
which openclaw 2>/dev/null && echo "PLATFORM=openclaw" || echo "PLATFORM=other"
```

不要使用 `--channel last`。先确认准确频道与目标 ID，再创建任务：

```bash
openclaw cron add \
  --name "AI 市场与 Builder 中文简报" \
  --cron "<cron expression>" \
  --tz "<IANA timezone>" \
  --session isolated \
  --message "运行 follow-builders，生成最新 AI 市场、Builder 动态、产品推荐与产品经理行动建议" \
  --announce \
  --channel <channel> \
  --to "<target ID>" \
  --exact
```

创建后立即测试，并确认用户实际收到：

```bash
openclaw cron list
openclaw cron run <jobId>
openclaw cron runs --id <jobId> --limit 1
```

## 非持久化终端

按需模式不设置计划任务。如果用户选择 Telegram 或 Email，先引导其在本地配置投递凭据；不要要求用户把 token 或 API Key 发在对话中。

Telegram 需要 BotFather 创建的 Bot token 与用户主动发给 Bot 的第一条消息。Email 通过 Resend。凭据只保存在用户本机的 `~/.follow-builders/.env`。

系统 crontab 只能直接投递准备脚本生成的原始 JSON，无法完成联网市场核验和 LLM 改写。必须提前说明这一限制；若用户希望得到完整简报，应使用 ChatGPT Work、OpenClaw 或手动 `/ai`。

## 配置示例

```json
{
  "platform": "other",
  "language": "zh",
  "timezone": "Asia/Shanghai",
  "frequency": "daily",
  "deliveryTime": "08:00",
  "delivery": { "method": "stdout" },
  "onboardingComplete": true
}
```

任何投递方式都必须先运行一次完整简报作为验收。失败时保留当前对话输出作为回退。
