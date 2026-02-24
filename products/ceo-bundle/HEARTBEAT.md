# HEARTBEAT.md — Daily Operating Rhythm

## Morning Brief (runs at 9am by default)
On each heartbeat, your AI checks in and surfaces what matters:

1. Read TODO.md. If the "Now" section is empty, ask your CEO for the next priority.
2. If "Now" has items, verify progress in the last 30 minutes. If stalled, surface the next concrete action and resume.
3. Only message if something needs attention. Stay silent otherwise.

## Setup

Add this to your OpenClaw cron to activate the morning brief:

```bash
openclaw cron add \
  --name "morning-brief" \
  --schedule "0 9 * * *" \
  --task "Read TODO.md. Report today's top 3 priorities to CEO. Flag anything stalled or blocked."
```

## Quiet Hours

Do not proactively message CEO between 10pm and 7am in their timezone.
Add your timezone to USER.md to activate this.

## Checks to Add

Customize what your AI monitors on each heartbeat. Common additions:

| Check | How to add |
|---|---|
| API cost balance | Add billing URL to check in HEARTBEAT.md |
| Social media metrics | Add handle and platform to check weekly |
| Key SaaS uptime | Add webhook or status page URL |
| Revenue dashboard | Add Stripe dashboard URL for daily check |

## TODO.md Format

Create `~/.openclaw/workspace/TODO.md` with this structure:

```markdown
# TODO.md

## Now
- [Active task with owner and deadline]

## Next
- [Queued tasks in priority order]

## Later
- [Backlog — not urgent]

## Done
- [Completed items with date]
```

---

*Your AI reads this file on every heartbeat. Keep it current.*
