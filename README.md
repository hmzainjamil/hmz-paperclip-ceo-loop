# hmz-paperclip-ceo-loop

> **Autonomous CEO strategy loop for DigiMinds | runs every 6h | zero human input required**

[![schedule](https://img.shields.io/badge/schedule-every_6h-blue?style=flat)](.) [![api](https://img.shields.io/badge/API-127.0.0.1%3A3100-green?style=flat)](.) [![status](https://img.shields.io/badge/status-always_on-brightgreen?style=flat)](.) [![company](https://img.shields.io/badge/company-DigiMinds-orange?style=flat)](.)

[Overview](#overview) · [Architecture](#architecture) · [Schedule](#schedule) · [API](#api) · [Output](#output) · [Gotchas](#gotchas)

---

## 🧠 OVERVIEW

Paperclip AI CEO Loop is the **central decision engine** of DigiMinds agency. Every 6 hours it reviews all active goals, agent outputs, KPIs, and task backlogs — then re-prioritizes, assigns, and logs decisions autonomously. HMZ (founder) is notified only on critical escalations.

| Component | Value |
|---|---|
| Company | DigiMinds (digiminds.org) |
| Company ID | `c5066522-bacc-4a28-b700-6590cbe366ec` |
| API base | `http://127.0.0.1:3100/api` |
| LaunchAgent | `ai.hmz.paperclip` |
| Trigger | Every 6 hours (RunAtLoad=true, KeepAlive=true) |
| Authority | Full operational — budget, agents, tasks, strategy |

---

## ⚙️ ARCHITECTURE

```
[ LaunchAgent: ai.hmz.paperclip ] (permanent daemon)
        │
        ▼
[ CEO Loop Script: ~/.claude/bin/paperclip-ceo-loop ]
        │
        ├─► GET /api/goals → review all 20 active goals
        ├─► GET /api/agents → review 50 agent assignments
        ├─► GET /api/tasks → review KPI task backlog (28 tasks)
        ├─► POST /api/decisions → log decisions + re-prioritize
        └─► POST /api/alerts → escalate to HMZ if critical
```

| Layer | Tech |
|---|---|
| Daemon manager | macOS LaunchAgent (plist) |
| API server | Paperclip AI REST at port 3100 |
| Decision storage | Paperclip internal DB |
| Notification | Paperclip alert system → HMZ |
| Model | Tier 0 (Groq/Gemini — zero Claude tokens) |

---

## 📅 SCHEDULE

| Loop | Trigger | Action |
|---|---|---|
| CEO Review | Every 6h | Goals, agent status, backlog review |
| Task Triage | Every 6h | Re-prioritize 28 KPI tasks |
| Agent Health | Every 6h | Check all 50 agent outputs |
| Escalation | On anomaly | Alert HMZ with summary |
| Strategy Update | Daily 6AM | Full 24h strategic summary |

---

## 🔌 API REFERENCE

```bash
# Check Paperclip status
curl http://127.0.0.1:3100/api/status

# Get all active goals
curl http://127.0.0.1:3100/api/goals

# Get agent roster
curl http://127.0.0.1:3100/api/agents

# Get pending tasks
curl http://127.0.0.1:3100/api/tasks

# Trigger manual CEO loop
curl -X POST http://127.0.0.1:3100/api/ceo-loop/trigger
```

---

## 💡 TIPS

■ **Operations (4)**
| Tip | Source |
|---|---|
| CEO loop runs silently — check `/api/decisions` to see what it decided | Paperclip logs |
| If API is down, LaunchAgent auto-restarts within 30s | KeepAlive=true |
| Manual trigger via `curl -X POST .../ceo-loop/trigger` for on-demand review | API ref |
| All decisions are idempotent — safe to re-run | Design principle |

■ **Integration (3)**
| Tip | Source |
|---|---|
| Other agents (lead, content, KPI) report back to CEO loop after each run | Agent SOP |
| CEO loop auto-assigns new tasks from goal gaps | Paperclip AI |
| Budget decisions sync to DigiMinds finance tracker automatically | API webhook |

---

## ☠️ TOOLS REPLACED

| CEO Loop | Replaced |
|---|---|
| Autonomous strategy review | Weekly manual CEO meetings |
| Agent task assignment | Trello/Asana manual boards |
| KPI health monitoring | Google Sheets manual dashboards |
| Escalation routing | Slack manual escalations |

---

## ⚠️ GOTCHAS

| Issue | Fix |
|---|---|
| API returns 503 | Paperclip not running — `launchctl start ai.hmz.paperclip` |
| Loop ran but no decisions | All goals/tasks healthy — expected behavior |
| Escalation not received | Check `/api/alerts` for log |
| Company ID mismatch | Always use `c5066522-bacc-4a28-b700-6590cbe366ec` |
| Loop overlaps itself | Built-in mutex — second run exits immediately |

---

## 🚀 SETUP

```bash
# Check LaunchAgent status
launchctl list | grep paperclip

# Start if stopped
launchctl start ai.hmz.paperclip

# View live logs
tail -f ~/Library/Logs/paperclip-ceo-loop.log

# Manual trigger
curl -X POST http://127.0.0.1:3100/api/ceo-loop/trigger
```

---

*Part of [DigiMinds AI Agency Stack](https://github.com/hmzainjamil) — Paperclip AI autonomous CEO system*
