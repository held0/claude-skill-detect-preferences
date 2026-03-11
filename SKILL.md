---
name: detect-user-preferences
description: Use when starting a new conversation or when the user mentions timezone, locale, language, date format, or system preferences. Also use when Claude gives times in UTC instead of local time, or uses the wrong language or date format.
---

# Detect User Preferences

## Overview

Auto-detect the user's system preferences (timezone, locale, language, date format, OS, shell) and save them to Claude Code's auto memory so all future sessions use the correct settings.

**Core principle:** Detect once, apply forever. No user should have to manually tell Claude their timezone or language twice.

## When to Use

- First conversation with a new user (no preferences in memory yet)
- User complains about wrong timezone, language, or date format
- User asks to update their preferences
- When MEMORY.md has no "User System Preferences" section

## Quick Reference

| Setting | Detection Command | Example Output |
|---------|------------------|----------------|
| Timezone | `date +%Z && date +%z` | `CET`, `+0100` |
| Locale | `echo $LANG` | `en_US.UTF-8` |
| OS | `uname -s` | `Darwin`, `Linux` |
| Shell | `echo $SHELL` | `/bin/zsh` |
| Hostname | `hostname` | `MacBook-Pro.local` |

## Detection Commands

Run these shell commands to detect preferences:

```bash
# Timezone
date +%Z        # Zone name (e.g., CET, PST, +07)
date +%z        # UTC offset (e.g., +0100, -0800, +0700)

# Locale & Language
echo $LANG       # e.g., en_US.UTF-8, de_DE.UTF-8
locale           # Full locale settings

# OS & Shell
uname -s         # Darwin, Linux
echo $SHELL      # /bin/zsh, /bin/bash

# Date format preference (infer from locale)
# de_DE → DD.MM.YYYY
# en_US → MM/DD/YYYY
# en_GB → DD/MM/YYYY
# ja_JP → YYYY/MM/DD
```

## Save to Memory

Write detected preferences to the project's `MEMORY.md` (or global `~/.claude/MEMORY.md`) under a "User System Preferences" section:

```markdown
## User System Preferences
- Timezone: UTC+7 (Asia/Bangkok) — always show times in this timezone
- Locale: en_US.UTF-8
- Preferred language: German (detected from conversation, not locale)
- Date format: YYYY-MM-DD (ISO) or DD.MM.YYYY (German)
- OS: macOS (Darwin)
- Shell: zsh
```

## Rules

1. **Timezone is king**: Always convert any UTC/server times to the user's local timezone before displaying
2. **NEVER guess the current time**: Always run `date` to get the actual time. LLMs cannot know the current time — they will hallucinate. This is non-negotiable.
3. **Language from conversation, not locale**: The user's spoken language may differ from their OS locale (e.g., German speaker with en_US locale)
4. **Don't re-detect if already saved**: Check MEMORY.md first. Only re-detect if user asks or preferences are missing
5. **Update, don't duplicate**: If preferences exist, update the existing section rather than adding a new one
6. **Show timezone in output**: When displaying times, always show both local time and offset: "15:35 (UTC+7)"

## Applying Preferences

Once saved, in every conversation:
- Show times in local timezone: "15:35 (UTC+7)" not "08:35 UTC"
- Use the user's preferred language for communication
- Use appropriate date format for their locale/language
- Reference their OS/shell when giving terminal commands (e.g., `pbcopy` on macOS vs `xclip` on Linux)

## Common Mistakes

| Mistake | Fix |
|---------|-----|
| Guessing the current time | ALWAYS run `date` — LLMs hallucinate times |
| Showing UTC times | Convert to user's timezone before displaying |
| Assuming locale = language | Check conversation language separately |
| Re-detecting every session | Read MEMORY.md first, detect only if missing |
| Hardcoding timezone name | Use UTC offset (+7) since zone names vary |
| Not showing offset | Always include "(UTC+X)" for clarity |
| Wrong date format | Match to locale: de→DD.MM, en_US→MM/DD, ISO→YYYY-MM-DD |
