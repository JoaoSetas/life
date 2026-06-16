# Automation — the hourly check-in routine

The hourly check-in runs as a **Claude Code Routine** (cloud scheduler), set up at
[claude.ai/code/routines](https://claude.ai/code/routines). Each run is a full cloud
session that clones this repo, runs `/checkin`, logs the result, and can ask me a
question I answer later from web or mobile. See the official docs:
https://code.claude.com/docs/en/routines

## How it's configured
- **Repository:** `life`, with **Allow unrestricted branch pushes** enabled (Permissions
  tab) so each run can commit the daily log to `main` — that's how this hour's check-in
  carries into next hour's.
- **Environment:** Default (Trusted network is enough; the check-in only touches repo files).
- **Schedule:** hourly, **08:00–22:00 Lisbon**, via the cron `0 8-22 * * *`.
- **Prompt:** the tough-love check-in prompt (below).

## ⚠️ The routine clones `main`
Every run starts from the repository's **default branch (`main`)** and uses the `/checkin`
skill committed there. So the system files must be **merged to `main`** for the routine to
do anything — a routine pointed at an empty/stale `main` runs but accomplishes nothing.

## Setting the 8am–10pm window (cron)
The web form only offers presets (hourly / daily / weekdays / weekly) — no hour range.
A custom cron is set with **`/schedule update` in a local terminal CLI** (the `/schedule`
command is disabled inside web sessions, and the minimum interval is 1 hour):

```
0 8-22 * * *
```

Fires at minute 0 of hours 8–22 daily = 8am…10pm, 15 runs/day. Schedules are entered in
your local zone and converted automatically; `/schedule update` confirms the absolute
times — verify it reads 08:00–22:00 Lisbon. If the raw cron is treated as UTC, use
`0 7-21 * * *` (Lisbon is UTC+1 in summer).

No local terminal? The web UI can only do the `hourly` preset (24/7); pause overnight with
the **Repeats** toggle.

## The routine prompt
```
You are João's tough-love life coach. Run the /checkin skill for this repo,
following routines/checkin-protocol.md exactly.

Each run is a session I can open later on web or mobile, so DO talk to me.

On the automated run (before I reply):
- Run `date` for the real local date/time; compute the pregnancy week from context/pregnancy.md.
- Create today's log logs/YYYY-MM-DD.md from logs/TEMPLATE.md if missing; append this check-in.
- Commit and push to main now, so it's recorded even if I never open this run:
    git add -A && git commit -m "checkin" && git push
- Then output the short nudge block, and ASK me: what have I knocked out since the last
  check-in, and is there anything to remember or want ideas for?

When I reply in the session:
- Tick today's checkboxes, log what I did, add wins to memory/wins.md, save anything to
  remember in memory/remember.md — then commit and push again.

TONE: tough-love coach — direct, hold me accountable, call out dropped musts and broken
streaks, push me to do better. No fluff.
```

## Managing it
- **Run now / pause / edit:** on the routine's detail page (Run now button, Repeats toggle,
  pencil icon).
- **Read a nudge / reply:** open the run as a session (web or Claude mobile app) and continue
  the conversation; your reply gets logged and pushed on the next turn.
- **Usage:** routines draw down subscription usage and have a daily run cap — see
  [claude.ai/settings/usage](https://claude.ai/settings/usage).
