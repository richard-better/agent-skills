# Installing gcalcli

## Prerequisites

- [gcalcli](https://github.com/insanum/gcalcli) installed
- Google OAuth credentials configured

## Install

```bash
# Homebrew (macOS)
brew install gcalcli

# pip
pip install gcalcli
```

## Authenticate

```bash
# First run triggers OAuth flow in browser
gcalcli list
```

This opens a browser for Google OAuth consent. Once authorized, credentials are stored locally:

- **macOS**: `~/Library/Application Support/gcalcli/`
- **Linux**: `~/.local/share/gcalcli/`

Config file: `config.toml` in the same directory.

## Verify

```bash
gcalcli list              # Should show your calendars
gcalcli agenda            # Should show upcoming events
```
