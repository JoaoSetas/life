# Check-in Protocol

> This is the **engine** of the system. It defines exactly what happens on every check-in — whether I run `/checkin` myself or it's triggered automatically. Keep it tight: I have limited bandwidth, especially at work.

## Goals of a check-in
1. Remind me of the **daily musts** that are still open.
2. Give me **one concrete thing to do right now**, suited to the time of day and day of week.
3. Keep my **wife and the pregnancy** front of mind with one specific caring nudge.
4. **Log everything** so there's a memory of what was suggested and done.

## Steps (what Claude does)
1. **Get the moment.** Determine today's date, time, and day of week (run `date`). Compute pregnancy week from `context/pregnancy.md`.
2. **Load context.** Read `context/*`, `routines/daily-musts.md`, `memory/remember.md`, and today's log `logs/YYYY-MM-DD.md` (create it from `logs/TEMPLATE.md` if missing).
3. **Assess.**
   - Which daily musts are still unchecked in today's log?
   - What does the **time block** call for (see below)?
   - Is it **Monday** (Porto) or a special day? Anything in `memory/remember.md` due now?
   - Pick **one** relationship/care action from the menu in `context/relationship-goals.md` (rotate — don't repeat the last one logged today).
4. **Output the nudge** in the short format below.
5. **Log it.** Append a check-in entry to today's log with the timestamp, what was suggested, and (if I reply) what I did.
6. **If interactive**, ask the 1–2 quick questions at the end and update the log + checklists from my answers.

## Time blocks (what to emphasize)
| Block | Time | Emphasis |
|-------|------|----------|
| 🌅 Morning | wake–09:00 | Warm greeting to wife; empty dishwasher after coffee; tidy breakfast; plan the day. |
| 💼 Work AM | 09:00–13:00 | Quick dishwasher check on a break; one warm text (esp. Mondays from Porto). Stay focused but not absent. |
| 🍽️ Midday | 13:00–14:30 | Eat; dishwasher check; tidy up after lunch; message her. |
| 💼 Work PM | 14:30–18:00 | Wind-down planning; remember the garbage; think about an evening gesture. |
| 🏡 Evening | 18:00–21:00 | **Be present.** Ask about her day first. Help with/clean up dinner. Garbage + dog walk. Caring act. |
| 🌙 Night | 21:00–sleep | Tidy shared spaces; prep for tomorrow; final dishwasher check; wind down together, not on the phone. |

(Outside ~07:00–22:30, stay quiet unless I initiate.)

## Output format (keep it this short)
```
🕐 Check-in · <Weekday> <HH:MM> · pregnancy ~<N>w
👉 Right now: <one concrete action for this time block>
✅ Still open today: <only the unchecked musts, e.g. dishwasher · garbage>
💛 For <wife>: <one specific caring idea, not repeated today>
📌 Remember: <due/important item> (omit line if none)
```
Then ask (interactive only): **"What have you knocked out since the last check-in?"** and log the answer.

## Principles
- **One headline action.** Don't dump a list; lead with the single most useful thing.
- **Never nag emptily.** If everything's done, celebrate it briefly and suggest a bonus caring act.
- **Always log**, even on automated runs, so the daily log is a real record.
- **Adapt to the day:** Mondays = Porto (reach her remotely); weekends = bigger proactive help + quality time.
