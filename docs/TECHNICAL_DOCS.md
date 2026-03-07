# Technical Documentation — detect-user-preferences

## Architecture

### How Claude Code Skills Work

Claude Code skills are markdown files (`SKILL.md`) with YAML frontmatter that Claude reads when triggered. Skills live in:

- **User-level:** `~/.claude/skills/<skill-name>/SKILL.md`
- **Project-level:** `.claude/skills/<skill-name>/SKILL.md`

When a conversation starts, Claude checks the skill's `description` field against the current context to decide whether to load it.

### Skill File Structure

```
detect-user-preferences/
├── SKILL.md              # The skill itself (required)
├── README.md             # GitHub documentation
├── package.json          # For npx skills CLI discovery
├── LICENSE               # MIT
├── .gitignore
└── docs/
    ├── DISTRIBUTION_PLAN.md
    └── TECHNICAL_DOCS.md
```

### SKILL.md Format

```yaml
---
name: detect-user-preferences
description: Use when [triggering conditions]...
---

# Skill Title

## Overview
Core principle in 1-2 sentences.

## When to Use
Triggering conditions.

## Quick Reference
Scannable table of key info.

## Rules
Numbered rules Claude must follow.

## Common Mistakes
What goes wrong + fixes.
```

**Constraints:**
- Frontmatter: max 1024 characters total
- `name`: letters, numbers, hyphens only
- `description`: third person, starts with "Use when..."

## Detection Logic

### Shell Commands

| Command | Purpose | Example Output |
|---------|---------|----------------|
| `date +%Z` | Timezone abbreviation | `CET`, `PST`, `+07` |
| `date +%z` | UTC offset | `+0100`, `-0800`, `+0700` |
| `echo $LANG` | System locale | `en_US.UTF-8`, `de_DE.UTF-8` |
| `locale` | Full locale config | Multiple LC_* variables |
| `uname -s` | Operating system | `Darwin`, `Linux` |
| `echo $SHELL` | Default shell | `/bin/zsh`, `/bin/bash` |
| `hostname` | Machine name | `MacBook-Pro.local` |

### Locale → Date Format Mapping

| Locale Prefix | Date Format | Example |
|---------------|-------------|---------|
| `de_DE` | DD.MM.YYYY | 07.03.2026 |
| `en_US` | MM/DD/YYYY | 03/07/2026 |
| `en_GB` | DD/MM/YYYY | 07/03/2026 |
| `ja_JP` | YYYY/MM/DD | 2026/03/07 |
| `zh_CN` | YYYY-MM-DD | 2026-03-07 |
| `fr_FR` | DD/MM/YYYY | 07/03/2026 |
| Default | ISO 8601 | 2026-03-07 |

### Language Detection

The skill distinguishes between **locale** and **language**:

- **Locale** = system setting (`$LANG`), affects date/number formatting
- **Language** = communication preference, detected from conversation

Example: A German developer in Thailand might have:
- Locale: `en_US.UTF-8` (English system)
- Timezone: `UTC+7` (Thailand)
- Language: German (speaks German in conversation)

The skill detects language from the first few messages in conversation, not from the locale.

## Storage

### MEMORY.md Location

Claude Code uses auto-memory stored at:
```
~/.claude/projects/<project-hash>/memory/MEMORY.md
```

The skill writes a "User System Preferences" section to this file.

### Memory Format

```markdown
## User System Preferences
- Timezone: UTC+7 (Asia/Bangkok) — always show times in this timezone
- Locale: en_US.UTF-8
- Preferred language: German (detected from conversation, not locale)
- Date format: DD.MM.YYYY
- OS: macOS (Darwin)
- Shell: zsh
```

### Persistence Rules

1. **Check before writing**: Don't overwrite existing preferences
2. **Update in place**: Edit the existing section, don't add duplicates
3. **User can override**: Manual edits to MEMORY.md take priority

## Edge Cases

### Timezone Without Name

Some systems show `+07` instead of `ICT` or `Asia/Bangkok`. The skill uses the UTC offset as the canonical format since it's unambiguous.

### Multiple Projects

Each Claude Code project has its own MEMORY.md. User preferences are written to the current project's memory. For global preferences, the user can also maintain `~/.claude/MEMORY.md`.

### WSL on Windows

On Windows Subsystem for Linux, detection works normally since it runs in a Linux shell. The OS will show `Linux` but the user is effectively on Windows.

### SSH Sessions

When Claude runs commands over SSH (e.g., on a remote server), the detected timezone will be the server's timezone, not the user's local timezone. The skill should note this and prefer the locally-detected timezone.

## Installation Methods

### 1. Skills CLI (recommended)

```bash
npx skills add held0/claude-skill-detect-preferences -g -y
```

This:
1. Clones the repo
2. Symlinks SKILL.md to `~/.claude/skills/detect-user-preferences/`
3. Available immediately in next conversation

### 2. Manual Git Clone

```bash
git clone https://github.com/held0/claude-skill-detect-preferences.git \
  ~/.claude/skills/detect-user-preferences
```

### 3. Direct File Copy

```bash
mkdir -p ~/.claude/skills/detect-user-preferences
curl -o ~/.claude/skills/detect-user-preferences/SKILL.md \
  https://raw.githubusercontent.com/held0/claude-skill-detect-preferences/main/SKILL.md
```

## Testing

### Manual Test

1. Remove any existing preferences from MEMORY.md
2. Start a new Claude Code session
3. Ask Claude "What time is it?"
4. Verify Claude shows your local timezone, not UTC

### Verification Checklist

- [ ] Timezone correctly detected
- [ ] Locale correctly detected
- [ ] OS correctly detected
- [ ] Shell correctly detected
- [ ] Preferences saved to MEMORY.md
- [ ] Next session reads saved preferences
- [ ] Times shown in local timezone
- [ ] Language matches conversation (not locale)
