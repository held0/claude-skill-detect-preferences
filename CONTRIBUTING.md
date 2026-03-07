# Contributing

Thanks for your interest in contributing to detect-user-preferences!

## How to Contribute

### Bug Reports

Open a GitHub issue with:
- Your OS and shell
- What you expected vs what happened
- Relevant Claude Code session output

### Feature Requests

Open an issue describing:
- The problem you're solving
- Your proposed solution
- Why this belongs in this skill (vs a separate one)

### Pull Requests

1. Fork the repo
2. Create a branch: `git checkout -b feature/my-feature`
3. Make your changes to `SKILL.md`
4. Test locally by copying to `~/.claude/skills/detect-user-preferences/`
5. Start a new Claude Code session and verify the skill works
6. Submit a PR with a clear description

### Guidelines

- Keep SKILL.md concise — every token costs context
- Detection commands must work on both macOS and Linux
- Don't add features for hypothetical use cases
- Test before submitting

## Ideas for Contributions

- Better timezone name resolution (UTC offset → city name)
- Support for more locales and date formats
- Auto-detect from git config (user.name, user.email)
- Integration with other preference sources (.editorconfig, etc.)
