# Distribution Plan — detect-user-preferences

## Ziel

Maximale Verbreitung des Skills in der Claude Code Community, sodass möglichst viele Entwickler den Skill installieren und nutzen.

---

## Phase 1: Grundlagen (Tag 1)

### 1.1 GitHub Repository

- [x] Repo erstellen: `held0/claude-skill-detect-preferences`
- [x] README.md mit Installation, Beispielen, Screenshots
- [x] SKILL.md im korrekten Format
- [x] LICENSE (MIT)
- [x] package.json mit Keywords
- [ ] GitHub Topics setzen: `claude-code`, `claude-skill`, `timezone`, `locale`, `developer-tools`
- [ ] GitHub Description: "Auto-detect timezone, locale & language for Claude Code"

### 1.2 Skills.sh Marketplace

- [ ] Skill auf skills.sh listen lassen
- [ ] Sicherstellen dass `npx skills add held0/claude-skill-detect-preferences` funktioniert
- [ ] Skill-Seite auf skills.sh verifizieren

### 1.3 SkillHub.club

- [ ] Skill auf skillhub.club einreichen
- [ ] Beschreibung und Tags optimieren

---

## Phase 2: Community Seeding (Tag 1-3)

### 2.1 Reddit

**Subreddits:**
- r/ClaudeAI (~150k Members) — Hauptzielgruppe
- r/anthropic — Anthropic-Community
- r/coding — Allgemeine Entwickler
- r/commandline — CLI-Enthusiasten

**Post-Strategie:**
- Titel: "I built a Claude Code skill that auto-detects your timezone so you never see UTC again"
- Format: Problem → Solution → How it works → Install command
- Kein reiner Promo-Post, sondern Mehrwert zeigen
- Cross-post zwischen Subreddits mit angepasstem Ton

### 2.2 Twitter/X

**Tweets:**
1. Launch-Tweet mit Before/After-Screenshot
2. Thread: "5 annoying things Claude Code does wrong — and how skills fix them"
3. Tag: @AnthropicAI, @alexalbert__, #ClaudeCode
4. Hashtags: #ClaudeCode #AITools #DeveloperTools #OpenSource

**Timing:** Dienstag-Donnerstag, 9-11 Uhr EST (US Tech Peak)

### 2.3 Hacker News

- "Show HN: Auto-detect timezone/locale for Claude Code sessions"
- Technisch formuliert, Problem-fokussiert
- Am Wochenmorgen US-Zeit posten (weniger Konkurrenz)

### 2.4 Dev.to / Medium

**Artikel: "How I Made Claude Code Remember My Timezone (And You Can Too)"**
- Problem mit konkretem Beispiel (UTC vs Lokalzeit)
- Technische Erklärung der Skill-Architektur
- Installationsanleitung
- Call-to-Action: GitHub Star + Install

### 2.5 LinkedIn

- Post über Developer Experience und AI-Tools
- Professioneller Ton, fokussiert auf Produktivität
- Hashtags: #ClaudeCode #DeveloperExperience #AITools

---

## Phase 3: Ecosystem Integration (Woche 1-2)

### 3.1 Awesome Lists

- [ ] PR an `ComposioHQ/awesome-claude-skills` — größte kuratierte Liste
- [ ] PR an `mhattingpete/claude-skills-marketplace`
- [ ] Eigene awesome-list suchen/erstellen

### 3.2 Skill Directories

- [ ] LobeHub Skills Marketplace einreichen
- [ ] skills.sh Listing optimieren
- [ ] SkillHub.club Listing optimieren

### 3.3 Blogging & SEO

- [ ] Blog-Post auf eigener Website (offenesprechstunden.de/blog oder held0.com)
- [ ] Keywords: "claude code timezone", "claude code locale", "claude code preferences"
- [ ] Interne Verlinkung zu anderen Projekten

---

## Phase 4: Partnerschaften (Woche 2-4)

### 4.1 YouTube / Content Creator

- Kontakt zu Claude Code Tutorial-Erstellern
- Skill als "Featured Tool" in Videos anbieten
- Kurze Demo-Clips bereitstellen

### 4.2 Newsletter

- "Console.dev" — Developer Tools Newsletter
- "TLDR" — Tech Newsletter
- "Changelog" — Open Source Newsletter
- Pitches vorbereiten mit konkretem Mehrwert

### 4.3 Discord Communities

- Anthropic Discord (falls vorhanden)
- Claude Code Community Channels
- Developer Tools Discord Server

---

## Phase 5: Wachstum & Iteration (Monat 1-3)

### 5.1 Feedback sammeln

- GitHub Issues überwachen
- Reddit/Twitter Mentions tracken
- Feature-Requests priorisieren

### 5.2 Erweiterungen

Basierend auf Community-Feedback:
- **Auto-detect IDE** (VS Code, Cursor, etc.)
- **Auto-detect Projekt-Sprache** (Python, Node, Ruby)
- **Team-Präferenzen** (shared .claude/team-preferences.md)
- **Migration** (wenn User den Rechner wechselt)

### 5.3 Metriken

- GitHub Stars als Hauptmetrik
- `npx skills` Install-Zahlen (falls verfügbar)
- Reddit/HN Upvotes als Engagement-Metrik

---

## Content Templates

### Reddit Post (r/ClaudeAI)

```
Title: I built a Claude Code skill that auto-detects your timezone so Claude never shows UTC again

Body:
**The problem:** Every Claude Code session starts from scratch. Claude doesn't know
your timezone, so it shows "08:00 UTC" when you need "15:00 (UTC+7)". You have to
manually tell Claude your timezone every. single. time.

**The fix:** I built `detect-user-preferences` — a skill that:
1. Auto-detects your timezone, locale, OS, and shell
2. Saves them to Claude Code's persistent memory
3. Every future session automatically uses your preferences

**Before:** "The scraper starts at 08:00 UTC on 2026-03-07"
**After:** "Der Scraper startet um 15:00 (UTC+7) am 07.03.2026"

Install: `npx skills add held0/claude-skill-detect-preferences -g -y`

GitHub: [link]

Open source (MIT). PRs welcome!
```

### Twitter Thread

```
🧵 Claude Code doesn't know your timezone. Here's how I fixed it.

1/ Every new Claude Code session: "The task starts at 08:00 UTC"
   Me: *mental math* "So that's... 3pm my time?"

2/ I built a skill that auto-detects your system preferences:
   - Timezone (date +%z)
   - Locale ($LANG)
   - OS (uname)
   - Shell ($SHELL)

3/ It saves to Claude's memory once, then every future session
   just knows. "15:00 (UTC+7)" — no more UTC math.

4/ Install in one command:
   npx skills add held0/claude-skill-detect-preferences -g -y

5/ Open source, MIT licensed.
   GitHub: [link]

   Star if useful ⭐
```

### Hacker News

```
Title: Show HN: Auto-detect timezone/locale for Claude Code

Body:
I got tired of Claude Code showing me UTC times and responding in English
when I speak German. Built a skill that detects your system preferences
(timezone, locale, language, OS, shell) on first use and saves them to
Claude's persistent memory.

Detection is simple shell commands (date +%z, $LANG, uname). Storage is
Claude Code's MEMORY.md. Every subsequent session automatically applies
your preferences.

Install: npx skills add held0/claude-skill-detect-preferences -g -y

https://github.com/held0/claude-skill-detect-preferences
```

---

## Zeitplan

| Woche | Aktion |
|-------|--------|
| Tag 1 | GitHub Repo live, skills.sh, erste Reddit/Twitter Posts |
| Tag 2-3 | Hacker News, Dev.to Artikel, LinkedIn |
| Woche 1 | Awesome-Listen PRs, SkillHub, Feedback sammeln |
| Woche 2 | Medium Artikel, Newsletter Pitches, YouTube Outreach |
| Woche 3-4 | Erweiterungen basierend auf Feedback, v1.1 Release |
| Monat 2-3 | Community Building, weitere Features, Partnerschaften |
