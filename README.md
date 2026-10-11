# Reminder Intake · 聊完别忘

**Turn actionable conversations into a clear reminder proposal—with fewer decisions.**

[English](README.md) · [简体中文](README.zh-CN.md) · [Download](https://github.com/dryan3333/reminder-intake-skill/releases/latest) · [Report a problem](https://github.com/dryan3333/reminder-intake-skill/issues)

An open-source instruction skill for **Codex and Claude Code**. It spots deadlines, unfinished plans and follow-ups in the current conversation, prepares a sensible proposal, and uses available authorized tools to create and verify a reminder.



## How it feels

> Turn 1: “Any ideas for a date on Friday evening?”
>
> Turn 2: “Something relaxed: dinner, then a walk.”
>
> Turn 3: “I haven’t booked a restaurant yet. I’ll look around.”
>
> AI proposes: “Check restaurants and book a table · Thursday 7 pm · your preferred reminder app.”
>
> Choose: **Add this reminder / Adjust / Not now**.

No explicit “remind me” request is needed. The example demonstrates the intended three-turn behavior, not a recording of a successful live test.

The host determines whether choices appear as buttons or text. Dates and timezones are checked before writing. An explicit request is handled immediately; an actionable plan discussed over three user turns gets one proposal, without repeated nudges.

## Install

Clone once:

```sh
git clone https://github.com/dryan3333/reminder-intake-skill.git
```

**Codex** — copy the skill into your personal skills directory:

```sh
mkdir -p "$HOME/.codex/skills"
cp -R reminder-intake-skill/skills/reminder-intake "$HOME/.codex/skills/"
```

For a custom `CODEX_HOME`, use its `skills/` directory. Start a new conversation and invoke:

```text
Use $reminder-intake to check this conversation for follow-ups worth reminding me about.
```

**Claude Code** — use the same skill:

```sh
mkdir -p "$HOME/.claude/skills"
cp -R reminder-intake-skill/skills/reminder-intake "$HOME/.claude/skills/"
```

Invoke `/reminder-intake`, or let Claude select it when relevant. Compare existing installations before copying; avoid duplicate copies. [Claude Code documentation](https://code.claude.com/docs/en/skills).

**Claude App / claude.ai** — where custom skills are supported on your account, upload `reminder-intake.zip` from [Releases](https://github.com/dryan3333/reminder-intake-skill/releases/latest), then check that it is enabled. Installing a CLI skill does not automatically enable ordinary App chats. [Official help](https://support.claude.com/en/articles/12512180-use-skills-in-claude).

## What you need

A supported skill host, and separately available authorized tools for your destination. Apple Calendar, Google Calendar and macOS Reminders are possible targets; this repository **does not bundle those integrations**. Without a writing tool, the AI prepares a draft and does not report success.

This is an instruction skill, not a background service. It does not watch idle windows, scan all chats, or deliver notifications independently. Device sync and alerts depend on your calendar/reminder account and notification settings.

## Designed to avoid extra work

- Reuse a confirmed destination preference; ask only for missing material details.
- Distinguish a deadline from the notification time.
- Prefer updating an existing reminder when the user changes the time.
- Verify the result when tools permit; keep uncertain writes marked pending.
- Avoid triggering on historical dates, hypothetical plans and already-handled reminders.
- Send only necessary task details to the destination, not an entire private conversation.

The instruction file is currently Chinese; host models may respond in the user's language. English documentation does not imply that the instruction file has been translated or separately evaluated in English.

## Feedback and development

Try a fictional example first. Tell us which host you used, what you expected, and whether a reminder was actually created. Do not include private chat exports, account identifiers, passwords or calendar contents.

[Product review](docs/product-review.md) · [Evaluation scenarios](docs/evaluation.md) · [Commercial direction](docs/commercial-plan.md)

## License

MIT. Free to use, modify and distribute under [LICENSE](LICENSE). No paid hosted service is currently offered.
