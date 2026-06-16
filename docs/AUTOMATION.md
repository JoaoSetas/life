# Making it run every hour

The check-in logic (`/checkin`) works **right now** the moment you open a Claude
Code session on this repo. The only question is how to make it fire **on its own,
every hour, without you opening anything.** Here are your options, simplest first.

## Option A — Scheduled Claude Code sessions (recommended, no API key) ✅
Claude Code on the web can run on a **schedule/trigger**. Point a recurring
trigger at this repo with the prompt `Run /checkin`.

- **Pros:** native to what you're already using; no secrets; full intelligence;
  you can reply in the session to log what you did.
- **How:** in the Claude Code web app, create a scheduled trigger for this repo
  (e.g. hourly, 08:00–22:00) with prompt `Run /checkin`. See
  https://code.claude.com/docs/en/claude-code-on-the-web for triggers.
- **Delivery:** the nudge shows in the session; enable notifications to get pinged.

## Option B — GitHub Actions cron (fully hands-off, sends notifications) 🤖
The included workflow `.github/workflows/hourly-checkin.yml` runs hourly, updates
the log, and posts the nudge to a GitHub issue (which notifies your phone via the
GitHub app/email).

**Setup (one time):**
1. **Add the API key:** repo → Settings → Secrets and variables → Actions →
   *New repository secret* → `ANTHROPIC_API_KEY` = your key.
2. **Create the notification issue:** open one issue titled `📋 Daily Check-ins`,
   note its number, then add a repo *Variable* `CHECKIN_ISSUE_NUMBER` = that number.
3. **Merge to the default branch.** GitHub only runs scheduled workflows from the
   default branch.
4. **Test it now:** Actions tab → *Hourly check-in* → *Run workflow*.
5. **Get notified:** install the GitHub mobile app and enable notifications, or
   make sure issue-comment emails are on. Each hour you'll get the nudge.

- **Pros:** truly autonomous; real phone notifications; auto-commits your log.
- **Cons:** needs an API key (small token cost per run); GitHub cron can lag a few
  minutes; one-way (you log what you did next time you open a session).
- **Tune the hours:** edit the `cron:` line. `0 7-21 * * *` ≈ hourly 08:00–22:00
  Lisbon time in summer (shift 1h in winter — see comment in the file).

## Option C — Both
Use **A** for the interactive, reply-and-log experience when you're free, and **B**
as the always-on safety net that pings you even when you forget. They share the same
log files, so they stay in sync.

## Reducing the cost / noise
- Narrow the hours (you don't need a 3 a.m. nudge).
- Skip nights and maybe mid-day deep-work blocks.
- The nudge is intentionally short so notifications are glanceable.

> Tell me which option you want and I'll wire it up precisely (including the exact
> trigger config or tuning the workflow to your real wake/work hours).
