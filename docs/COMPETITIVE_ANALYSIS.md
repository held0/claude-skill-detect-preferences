# Competitive Analysis — detect-user-preferences

## TL;DR

**No existing skill does what ours does.** Existing timezone tools convert between timezones — they don't detect and remember user preferences. Our skill is the first to auto-detect system preferences and save them to persistent memory.

## Open Claude Code Issues Confirming the Need

| Issue | Description | Status |
|-------|-------------|--------|
| [#7233](https://github.com/anthropics/claude-code/issues/7233) | Add i18n support, auto-detect LANG/LC_ALL | Open |
| [#4866](https://github.com/anthropics/claude-code/issues/4866) | Internationalization/localization for CLI | Open |
| [#4514](https://github.com/anthropics/claude-code/issues/4514) | Incorrect date display in non-UTC timezones | Open |
| [#2200](https://github.com/anthropics/claude-code/issues/2200) | /status shows reset time without timezone | Open |
| [#1450](https://github.com/anthropics/claude-code/issues/1450) | Limit reset should indicate timezone | Open |

## Existing Solutions & Why They Don't Compete

### timezone-tools (henkisdabro/wookstar-claude-code-plugins)
- **What:** Converts times between IANA timezones, queries current time
- **Gap:** Utility tool for "What time is it in Tokyo?" — doesn't detect or save user preferences

### time-helper (Interstellar-code/claud-skills)
- **What:** PHP-based timezone conversion and DST detection
- **Gap:** Same — timezone math tool, not preference detection

### claude-code-toolkit (Sycochucky/claude-code-toolkit)
- **What:** Wrapper that injects temporal env vars before launching Claude
- **Gap:** Only supports Eastern Time, requires wrapper command, no locale/language/OS detection

### claude-reflect (BayramAnnakov/claude-reflect)
- **What:** Self-learning system that captures corrections over time
- **Gap:** Passive/reactive learning — doesn't proactively detect system settings

### i18n/Localization skills (various)
- **What:** Help developers build multilingual apps (next-intl, react-intl)
- **Gap:** Development workflow tools for apps, not for detecting the developer's own preferences

## Competing AI Assistants

| Assistant | Timezone | Locale | Preference System |
|-----------|----------|--------|-------------------|
| GitHub Copilot | UTC only | None | IDE settings only |
| Cursor | No awareness | Users request it | Not built-in |
| Windsurf/Codeium | None | None | "Memories" but no detection |
| Continue | None | None | Customizable blocks, no detection |

**Key finding:** No major AI coding assistant auto-detects system preferences.

## Our Unique Value

1. **Proactive detection** — runs shell commands, doesn't wait for user correction
2. **Comprehensive** — timezone + locale + language + OS + shell + date format
3. **Persistent** — saves to memory once, applies in every future session
4. **Language ≠ locale insight** — detects conversation language separately from system locale
5. **Auto-invoked** — triggers automatically when preferences are missing
