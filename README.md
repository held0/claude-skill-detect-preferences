# detect-user-preferences

A Claude Code skill that automatically detects and remembers your system preferences — timezone, locale, language, date format, OS, and shell — so Claude always communicates in the right context.

## The Problem

Every new Claude Code session starts from scratch. Claude doesn't know your timezone, your language, or your OS. This leads to frustrating experiences:

- Claude shows you times in UTC instead of your local timezone
- Claude responds in English when you prefer German
- Claude suggests Linux commands on macOS (or vice versa)
- You have to repeat your preferences every session

## The Solution

This skill auto-detects your system preferences on first use and saves them to Claude Code's persistent memory. From then on, every conversation automatically knows:

- **Your timezone** — times are always shown in your local time
- **Your language** — detected from conversation, not just locale
- **Your OS & shell** — correct commands for your system
- **Your date format** — DD.MM.YYYY for German, MM/DD/YYYY for US, etc.

## Installation

### Via Skills CLI (recommended)

```bash
npx skills add held0/claude-skill-detect-preferences
```

### Via GitHub (manual)

```bash
# Clone to your Claude Code skills directory
git clone https://github.com/held0/claude-skill-detect-preferences.git \
  ~/.claude/skills/detect-user-preferences
```

### Via Direct Copy

Copy the `SKILL.md` file to `~/.claude/skills/detect-user-preferences/SKILL.md`.

## How It Works

### 1. Detection (automatic on first use)

The skill runs these detection commands:

```bash
date +%Z        # Timezone name (CET, PST, +07)
date +%z        # UTC offset (+0100, -0800)
echo $LANG      # Locale (en_US.UTF-8)
uname -s        # OS (Darwin, Linux)
echo $SHELL     # Shell (/bin/zsh, /bin/bash)
```

### 2. Storage (persistent memory)

Detected preferences are saved to Claude Code's `MEMORY.md`:

```markdown
## User System Preferences
- Timezone: UTC+7 (Asia/Bangkok) — always show times in this timezone
- Locale: en_US.UTF-8
- Preferred language: German (detected from conversation)
- Date format: DD.MM.YYYY
- OS: macOS (Darwin)
- Shell: zsh
```

### 3. Application (every session)

Claude automatically applies these preferences:
- Shows times as "15:35 (UTC+7)" instead of "08:35 UTC"
- Communicates in your preferred language
- Uses correct OS commands (`pbcopy` vs `xclip`)
- Formats dates correctly for your locale

## Examples

### Before (without skill)

```
User: Wann startet der Scraper?
Claude: The scraper is scheduled to start at 08:00 UTC on 2026-03-07.
```

### After (with skill)

```
User: Wann startet der Scraper?
Claude: Der Scraper startet um 15:00 (UTC+7) am 07.03.2026.
```

## Supported Settings

| Setting | Detection Method | Fallback |
|---------|-----------------|----------|
| Timezone | `date +%z` | UTC |
| Locale | `$LANG` | en_US.UTF-8 |
| Language | Conversation analysis | Locale language |
| Date format | Locale-based inference | ISO 8601 |
| OS | `uname -s` | — |
| Shell | `$SHELL` | /bin/bash |

## Language Detection

The skill distinguishes between **locale** (system setting) and **language** (communication preference). A German-speaking developer might have `en_US.UTF-8` as their locale but prefer German communication. The skill detects this from the conversation language, not just the locale.

## Updating Preferences

If your preferences change (e.g., you travel to a new timezone), simply tell Claude:

```
User: Ich bin jetzt in Berlin, bitte Timezone updaten.
Claude: Timezone auf UTC+1 (Europe/Berlin) aktualisiert.
```

Or trigger a fresh detection:

```
User: Bitte erkenne meine Systemeinstellungen neu.
```

## Compatibility

- **Claude Code** (CLI) — full support
- **macOS** — full support
- **Linux** — full support
- **Windows (WSL)** — should work via WSL shell

## Contributing

Contributions welcome! Please open an issue or PR on GitHub.

### Development

```bash
# Clone the repo
git clone https://github.com/held0/claude-skill-detect-preferences.git
cd claude-skill-detect-preferences

# Install locally for testing
cp -r . ~/.claude/skills/detect-user-preferences/

# Test by starting a new Claude Code session
claude
```

## License

MIT — see [LICENSE](LICENSE) for details.
