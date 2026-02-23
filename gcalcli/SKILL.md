---
name: gcalcli
description: Use when the user asks about their calendar, schedule, upcoming events, or wants to create, search, or manage Google Calendar events from the command line. Also use when you need to check availability or find scheduling conflicts.
---

# gcalcli - Google Calendar CLI

Google Calendar CLI tool (v4.5.1). Installed at `/opt/homebrew/bin/gcalcli`.

## Non-Interactive Constraint

You are running from Claude Code (no tty). **Only use non-interactive commands.**

- `delete` and `edit` require Y/N prompts per event — **avoid these**
- `delete --iamaexpert` skips prompts but is dangerous (deletes ALL matches)
- If the user needs to delete/edit, explain this limitation and suggest they run the command manually
- For adding events, always use `--noprompt` with `add`, or use `quick`
- **Always specify `--calendar "<name>"`** when creating events (`--noprompt` does NOT skip the calendar picker — it will hang waiting for interactive input). Run `gcalcli list` to discover calendar names.

## Quick Reference

| Task | Command |
|------|---------|
| View agenda | `gcalcli agenda --nocolor --military --details all "today" "2 weeks"` |
| Machine-readable | `gcalcli agenda --tsv --nocolor --military "today" "1 week"` |
| Week view | `gcalcli calw --nocolor --military [weeks]` |
| Month view | `gcalcli calm --nocolor --military` |
| Search events | `gcalcli search --nocolor --military "text" [start] [end]` |
| Quick-add | `gcalcli quick --calendar "<name>" "natural language"` |
| Add event | `gcalcli add --noprompt --calendar "<name>" --title "..." --when "..." ...` |
| Find conflicts | `gcalcli conflicts --nocolor --military [start] [end]` |
| List calendars | `gcalcli list` |

## Key `add` Flags

| Flag | Description |
|------|-------------|
| `--noprompt` | **Required** for non-interactive use |
| `--calendar "<name>"` | **Required** to avoid calendar picker prompt (use `gcalcli list` to find names) |
| `--title` | Event title |
| `--when` | Start time (ISO 8601 with offset, e.g. `"2026-03-01T10:00-08:00"`) |
| `--end` | End time (alternative to `--duration`) |
| `--duration N` | Duration in minutes (or days with `--allday`) |
| `--where` | Location |
| `--description` | Event body/notes |
| `--who` | Attendee email (repeatable) |
| `--allday` | All-day event |
| `--color` | Event color: lavender, sage, grape, flamingo, banana, tangerine, peacock, graphite, blueberry, basil, tomato |
| `--reminder "N METHOD"` | e.g. "30 popup", "1h email" |

Only include flags the user provided — do not add empty `--description ""` or guess values.

## Time Formats

gcalcli accepts flexible time strings: `"tomorrow"`, `"next monday"`, `"2026-02-24 14:00"`, `"Feb 24 2pm"`, `"3:30pm"`, `"today"`, `"1 week"`.

For `--when`/`--end`, always use ISO 8601 with timezone offset to match the event's location (e.g. `"2026-03-01T10:00-08:00"`).

## Useful Read Flags

| Flag | Purpose |
|------|---------|
| `--nocolor` | Strip ANSI codes (always use when parsing output) |
| `--tsv` | Tab-separated output (machine-readable) |
| `--military` | 24-hour time format |
| `--nodeclined` | Hide declined events |
| `--nostarted` | Hide events that already started |
| `--details all` | Show all event details |

## Configuration

- Config dir: `~/Library/Application Support/gcalcli/`
- Config file: `config.toml`
- OAuth: stored in platform data dir

## See Also

- `examples.md` — Copy-paste-ready command examples for common event types
