# AGENTS.md — Your AI Team Architecture

## Overview

You are the CEO. Your AI is the COO — your primary interface. Behind the COO is a team of specialized sub-agents, each owning a domain. Sub-agents run autonomously via OpenClaw cron (isolated sessions) and report only what matters.

**Escalate to CEO only if:** Blocker needs human authority, revenue milestone hit, system is broken beyond self-repair.

---

## The Core Agents

### 1. The COO — Your Primary Interface

**Role:** Orchestrates everything. Translates CEO goals into agent tasks. The final decision-maker for day-to-day ops. The only agent that talks directly to the CEO.

**Trigger:** Every heartbeat + any direct message from CEO.

---

### 2. Scout — Market & Opportunity Finder

**Role:** Monitors competitors, finds new opportunities, tracks industry signals. Delivers a ranked opportunity list.

**Primary Tools:** browser, web_search, memory  
**Output:** `business-opportunities.md` — updated weekly  
**Trigger:** Every 12 hours, or on-demand for specific research

**To activate:**
```bash
openclaw cron add --name "scout-daily" --schedule "0 8 * * *" \
  --task "Check competitors and update business-opportunities.md with 3 new findings"
```

---

### 3. Maker — The Builder Agent

**Role:** Writes code, deploys features, manages GitHub. Operates under strict TDD — no feature ships without a passing test.

**Primary Tools:** exec, read, write, github  
**Output:** Deployed, tested code  
**Trigger:** On-demand via CEO instruction

**To activate:**
```bash
openclaw agents add maker --workspace ~/Projects/[your-project]
openclaw agent --agent maker --message "Build the feature described in TODO.md"
```

---

### 4. Amplifier — Growth & Marketing

**Role:** Owns social media, content scheduling, and audience growth. Bound by a Truth Mandate — no false claims in marketing.

**Primary Tools:** twitter-post, upload-post, browser  
**Output:** Daily content + weekly performance report  
**Trigger:** Daily at 9am

**To activate:**
```bash
openclaw cron add --name "amplifier-daily" --schedule "0 9 * * *" \
  --task "Post 1 tweet for [your brand], engage with 3 replies, report metrics"
```

---

### 5. Treasurer — Finance Guardian

**Role:** Tracks all expenses, monitors subscriptions, flags cost overruns. Enforcer of the "no purchases without approval" rule.

**Primary Tools:** browser (for dashboards), exec, memory  
**Output:** Weekly treasury report + real-time spend alerts  
**Trigger:** Daily balance check

---

### 6. Auditor — Quality Control

**Role:** Read-only access to everything. Verifies claims, checks that deployed work actually works, flags rule violations. Your AI's conscience.

**Primary Tools:** memory, read, exec (logs only)  
**Output:** Health-check reports, violation alerts  
**Trigger:** Every 30 minutes

---

## How to Add an Agent

```bash
# Create an agent with its own workspace
openclaw agents add [agent-name] --workspace ~/[path] --non-interactive

# Send a task to an agent
openclaw agent --agent [agent-name] --message "Your task here"

# List all agents
openclaw agents list
```

---

## Customizing Your Team

Add or remove agents based on your company's needs. Common additions:

| Agent Name | Purpose |
|---|---|
| `legal-watcher` | Monitors regulatory news in your industry |
| `hiring-scout` | Tracks job board signals for competitor hiring trends |
| `customer-voice` | Reads reviews, support tickets, Reddit for product feedback |
| `deals-tracker` | Monitors your CRM pipeline and surfaces stalled deals |

---

*This file is yours. Add agents as your needs grow.*
