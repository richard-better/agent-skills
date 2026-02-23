# gcalcli Command Examples

Copy-paste-ready examples for common calendar operations. Replace `<calendar>` with your calendar name (run `gcalcli list` to find it).

## Reading Calendar

### View upcoming events
```bash
gcalcli agenda --nocolor --military --details all "today" "2 weeks"
```

### Machine-readable agenda (for parsing)
```bash
gcalcli agenda --tsv --nocolor --military "today" "1 week"
```

### Week/month views
```bash
gcalcli calw --nocolor --military         # This week
gcalcli calw --nocolor --military 2        # Next 2 weeks
gcalcli calm --nocolor --military          # This month
```

### Search for events
```bash
gcalcli search --nocolor --military "dentist" "today" "3 months"
gcalcli search --nocolor --military --details all "standup" "2026-03-01" "2026-03-31"
```

### Check for conflicts
```bash
gcalcli conflicts --nocolor --military "today" "1 week"
```

### List calendars
```bash
gcalcli list
```

## Creating Events — Flights

Use `--when` with departure timezone and `--end` with arrival timezone (not `--duration`) so the calendar shows the correct flight duration across time zones.

### Domestic flight
```bash
gcalcli add --noprompt --calendar "<calendar>" \
  --title "SFO to JFK" \
  --when "2026-03-01T10:00-08:00" \
  --end "2026-03-01T18:30-05:00" \
  --where "SFO" \
  --description "UA 123 / PNR: ABC456"
```

### International flight (crossing timezones)
```bash
gcalcli add --noprompt --calendar "<calendar>" \
  --title "LHR to NRT" \
  --when "2026-03-02T11:00+00:00" \
  --end "2026-03-03T07:30+09:00" \
  --where "LHR" \
  --description "BA 5 / PNR: XYZ789"
```

## Creating Events — With Duration

### Event with duration in minutes
```bash
gcalcli add --noprompt --calendar "<calendar>" \
  --title "Team Standup" \
  --when "2026-03-05T09:00-08:00" \
  --duration 30
```

### Event with location and description
```bash
gcalcli add --noprompt --calendar "<calendar>" \
  --title "Dentist Appointment" \
  --when "2026-03-10T14:00-08:00" \
  --duration 60 \
  --where "123 Main St, Suite 200" \
  --description "Cleaning + checkup"
```

## Creating Events — With End Time

Use `--end` instead of `--duration` when you know the exact end time, or when start and end are in different timezones.

```bash
gcalcli add --noprompt --calendar "<calendar>" \
  --title "Conference Workshop" \
  --when "2026-03-15T09:00+01:00" \
  --end "2026-03-15T17:00+01:00" \
  --where "Berlin Convention Center"
```

## Creating Events — All-Day

```bash
gcalcli add --noprompt --calendar "<calendar>" \
  --title "Company Offsite" \
  --when "2026-03-20" \
  --end "2026-03-22" \
  --allday
```

## Creating Events — With Attendees

```bash
gcalcli add --noprompt --calendar "<calendar>" \
  --title "Project Kickoff" \
  --when "2026-03-05T10:00-08:00" \
  --duration 60 \
  --who alice@example.com \
  --who bob@example.com \
  --description "Q2 planning"
```

## Creating Events — With Reminders and Color

```bash
gcalcli add --noprompt --calendar "<calendar>" \
  --title "Submit Tax Return" \
  --when "2026-04-15T09:00-07:00" \
  --duration 60 \
  --reminder "1d popup" \
  --reminder "1h email" \
  --color tomato
```

## Quick-Add (Natural Language)

```bash
gcalcli quick --calendar "<calendar>" "Lunch with Sarah noon tomorrow at Cafe Roma"
gcalcli quick --calendar "<calendar>" "Team standup 9:30am every weekday"
```

## Timezone Reference

Use ISO 8601 offsets in `--when`/`--end` to match the event's location:

| Timezone | Offset | Example cities |
|----------|--------|----------------|
| PST | -08:00 | San Francisco, Los Angeles |
| PDT | -07:00 | San Francisco, Los Angeles (summer) |
| EST | -05:00 | New York, Boston |
| EDT | -04:00 | New York, Boston (summer) |
| CET | +01:00 | Berlin, Paris, Rome |
| CEST | +02:00 | Berlin, Paris, Rome (summer) |
| CST (China) | +08:00 | Shanghai, Beijing |
| JST | +09:00 | Tokyo, Osaka |
| GMT/UTC | +00:00 | London (winter) |
| BST | +01:00 | London (summer) |
