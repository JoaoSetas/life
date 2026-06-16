# 🏡 Life

A personal system to help **João** balance demanding work (he leads AI for his whole
company) with what matters most: his pregnant wife, their home, and their pets — without
relying on willpower or memory alone.

> **The problem this solves:** deep focus at work eats the mental space needed to be
> attentive at home. This repo offloads the remembering, nudges proactively every hour,
> and keeps a memory of what was done and what's promised.

## How it works
1. **It knows your life** — durable facts live in [`context/`](context/) (you, your wife,
   the pregnancy, the house, your relationship goals).
2. **It checks in on a rhythm** — the [`/checkin`](.claude/skills/checkin/SKILL.md) routine
   (defined in [`routines/checkin-protocol.md`](routines/checkin-protocol.md)) gives you, every
   hour: one concrete action for *right now*, the daily musts still open, a specific caring
   nudge for your wife, and any due reminder — then logs it.
3. **It remembers** — tell it things (`/remember`), ask for ideas (`/idea`); it stores them in
   [`memory/`](memory/) and writes a [daily log](logs/).

## Daily musts (the headliners)
- 🍽️ **Empty the dishwasher every day** — before she does.
- 🗑️ **Take out the garbage every day** — easiest on the dog walk.
- 🧹 **Keep things tidy** — clean up as you go, leave no mess.
- 💛 **One caring act for your wife** + ask about her day first.

## The three commands
| Command | What it does |
|---------|--------------|
| `/checkin` | Run a check-in: reminders + one action + a caring nudge, all logged. |
| `/remember` | Save something to remember (a task, a promise, an appointment). |
| `/idea` | Get fresh, specific ideas to care for your wife — or bank one. |

You can also just **talk to it**: "remember to call the clinic Monday", "what should I do
for her tonight?", "I emptied the dishwasher and brought her tea."

## Make it run every hour
The hourly check-in runs as a **Claude Code Routine** (cloud scheduler) — set up at
[claude.ai/code/routines](https://claude.ai/code/routines), hourly 8am–10pm. The full
setup, the cron (`0 8-22 * * *`), and the prompt are in
[`docs/AUTOMATION.md`](docs/AUTOMATION.md). Each run is a session you can open on web or
mobile to read the nudge and reply.

## Make it yours (2-minute setup)
- [ ] Add your **wife's name** and the **pets' names** in [`context/family.md`](context/family.md).
- [ ] Confirm the **due date** and add **appointment dates** in [`context/pregnancy.md`](context/pregnancy.md).
- [ ] Confirm your **work week** (remote days, hours) in [`context/about-me.md`](context/about-me.md).
- [ ] Merge this to `main` so the hourly [Routine](docs/AUTOMATION.md) has something to run.

## Layout
```
context/    who & what matters (durable facts)
routines/   daily musts, weekly rhythm, the check-in engine
memory/     things to remember · ideas backlog · wins log
logs/        dated daily logs
.claude/    /checkin, /remember, /idea skills + CLAUDE.md guide
docs/       automation setup
```

---
*Small, consistent care compounds. This is a tool to make sure it actually happens.* 💛
