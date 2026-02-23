# gcalcli Skill for Claude Code

A Claude Code skill that enables managing Google Calendar from the command line.

## Files

| File | Purpose |
|------|---------|
| `SKILL.md` | Main skill definition — constraints, flags, quick reference |
| `examples.md` | Copy-paste-ready command examples |
| `INSTALL.md` | Installing and authenticating gcalcli |

## Usage

Once installed, Claude Code automatically uses this skill when you ask about calendar events:

```
"What's on my calendar this week?"
"Add a meeting with Alice tomorrow at 2pm"
"Do I have any conflicts next Monday?"
"Create a flight event from SFO to JFK"
```

## Limitations

gcalcli's `delete` and `edit` commands require interactive Y/N confirmation, which doesn't work in Claude Code's non-interactive environment. For those operations, run the commands manually in your terminal.
