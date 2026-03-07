# Social Media Content — Ready to Post

## Reddit: r/ClaudeAI

**Title:** I built a Claude Code skill that auto-detects your timezone so Claude never shows UTC again

**Body:**

**The problem:** Every Claude Code session starts from scratch. Claude doesn't know your timezone, so it shows "08:00 UTC" when you need "15:00 (UTC+7)". Even worse — you have to manually tell Claude your timezone every. single. time.

I got frustrated after Claude showed me a server schedule in UTC for the third time. I speak German but my macOS locale is en_US. Claude kept responding in English.

**The fix:** I built `detect-user-preferences` — a Claude Code skill that:

1. Auto-detects your timezone, locale, OS, and shell via simple shell commands
2. Detects your preferred language from the conversation (not just locale!)
3. Saves everything to Claude Code's persistent memory
4. Every future session automatically uses your preferences

**Before:**
> "The scraper is scheduled to start at 08:00 UTC on 2026-03-07."

**After:**
> "Der Scraper startet um 15:00 (UTC+7) am 07.03.2026."

**Install:**
```
npx skills add held0/claude-skill-detect-preferences -g -y
```

**GitHub:** https://github.com/held0/claude-skill-detect-preferences

Open source (MIT). PRs welcome! Would love feedback on what other preferences should be auto-detected.

---

## Reddit: r/commandline

**Title:** Auto-detect timezone & locale for Claude Code CLI sessions

**Body:**

Built a skill for Claude Code (Anthropic's CLI tool) that runs `date +%z`, `$LANG`, `uname -s`, and `$SHELL` to auto-detect your system preferences and saves them to persistent memory.

Solves the annoying problem of Claude showing UTC times and suggesting Linux commands when you're on macOS.

```
npx skills add held0/claude-skill-detect-preferences -g -y
```

https://github.com/held0/claude-skill-detect-preferences

---

## Twitter/X: Launch Thread

**Tweet 1:**
Claude Code doesn't know your timezone.

Every session: "The task starts at 08:00 UTC"
You: *does mental math* "So that's 3pm my time?"

I built a skill to fix this forever. Thread 🧵

**Tweet 2:**
`detect-user-preferences` auto-detects:
- Timezone (date +%z)
- Locale ($LANG)
- Language (from conversation, not locale!)
- OS (uname -s)
- Shell ($SHELL)

One detection. Saved to memory. Applied forever.

**Tweet 3:**
Before: "The scraper starts at 08:00 UTC on 2026-03-07"

After: "Der Scraper startet um 15:00 (UTC+7) am 07.03.2026"

Yes, it even detects your language from conversation — not just locale. A German dev with en_US locale gets German responses.

**Tweet 4:**
Install in one command:

npx skills add held0/claude-skill-detect-preferences -g -y

Open source (MIT): https://github.com/held0/claude-skill-detect-preferences

If you use Claude Code, this saves you from repeating "I'm in UTC+7" every session.

---

## Hacker News: Show HN

**Title:** Show HN: Auto-detect timezone/locale for Claude Code sessions

**Body:**

I got tired of Claude Code showing me UTC times and responding in English when I speak German. Built a simple skill that detects system preferences on first use.

Detection: shell commands (date +%z, $LANG, uname -s, $SHELL)
Storage: Claude Code's persistent MEMORY.md
Application: automatic in every subsequent session

Key insight: language ≠ locale. A German speaker with en_US locale should get German responses. The skill detects conversation language separately from system locale.

Install: npx skills add held0/claude-skill-detect-preferences -g -y

https://github.com/held0/claude-skill-detect-preferences

---

## LinkedIn

**Post:**

Every AI coding assistant has the same blind spot: they don't know your context.

Claude Code shows UTC times. Cursor doesn't know you prefer German. GitHub Copilot suggests Linux commands on macOS.

I built an open-source skill for Claude Code that solves this:

1. Auto-detect timezone, locale, language, OS, shell
2. Save to persistent memory (once)
3. Apply automatically in every session

The interesting part: locale ≠ language. Many international developers have en_US systems but communicate in their native language. The skill detects this from the conversation itself.

Simple solution to a daily annoyance.

Install: npx skills add held0/claude-skill-detect-preferences -g -y
GitHub: https://github.com/held0/claude-skill-detect-preferences

#ClaudeCode #DeveloperExperience #OpenSource #AITools

---

## Dev.to / Medium Article

**Title:** How I Made Claude Code Remember My Timezone (And You Can Too)

**Subtitle:** Building a Claude Code skill that auto-detects system preferences

**Outline:**

1. **The Problem** (with screenshot/code example)
   - Every session starts fresh
   - UTC times everywhere
   - Wrong language
   - Wrong OS commands

2. **Why This Happens**
   - Claude Code's ephemeral context
   - No built-in preference detection
   - Skills system to the rescue

3. **The Solution Architecture**
   - Shell command detection
   - Persistent memory via MEMORY.md
   - Language vs locale distinction

4. **Building It Step by Step**
   - The SKILL.md format
   - Detection commands explained
   - Memory storage pattern
   - Testing the skill

5. **Install & Use**
   - One-command installation
   - What happens on first use
   - Customization options

6. **What's Next**
   - Community contributions welcome
   - Potential extensions (IDE detection, project language, etc.)
   - Link to GitHub

---

## SkillHub.club Submission

**Name:** detect-user-preferences

**Description:** Auto-detect and remember system preferences (timezone, locale, language, date format, OS, shell) for Claude Code. Detects once, applies forever.

**Category:** Productivity

**Tags:** timezone, locale, language, preferences, developer-tools, i18n

**Install Command:** npx skills add held0/claude-skill-detect-preferences -g -y

**GitHub:** https://github.com/held0/claude-skill-detect-preferences

---

## awesomeclaude.ai Submission

Check if manual submission is possible at https://awesomeclaude.ai/
If form-based, use same description as SkillHub above.
