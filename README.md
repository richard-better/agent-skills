# Claude Code Skills

A personal collection of reusable [Claude Code](https://docs.anthropic.com/en/docs/claude-code) skills.

## Skills

| Skill | Description |
|-------|-------------|
| [gcalcli](./gcalcli/) | Manage Google Calendar from the command line — read events, create events, handle timezones |

## Usage

### As a submodule

```bash
git submodule add git@github.com:richard-better/claude-code-skills.git .claude/skills-shared

# Symlink individual skills into .claude/skills/
ln -s ../skills-shared/gcalcli .claude/skills/gcalcli
```

### Manual copy

```bash
cp -r gcalcli/ ~/.claude/skills/gcalcli
```
