# hmz-paperclip-ceo-loop
Autonomous CEO strategy loop — reviews all DigiMinds goals, agents, and KPI tasks every 6 hours. Zero human input for routine operations.

![schedule](https://img.shields.io/badge/schedule-every_6h-blue?style=flat&labelColor=555) ![agents](https://img.shields.io/badge/agents-50_reviewed-green?style=flat&labelColor=555) ![goals](https://img.shields.io/badge/goals-20_active-orange?style=flat&labelColor=555) [![api](https://img.shields.io/badge/API-127.0.0.1%3A3100-white?style=flat&labelColor=555)](http://127.0.0.1:3100)

[Concepts](#-concepts) · [Hot](#-hot) · [Loop](#️-loop-architecture) · [Tips](#-tips-and-tricks-16) · [Replaced](#️-startups--businesses) · [Stars](#star-history)

---

## 🧠 CONCEPTS

| Feature | Location | Description |
|---------|----------|-------------|
| [**LaunchAgent daemon**](launchagent/ai.hmz.paperclip.plist) | `ai.hmz.paperclip.plist` | `KeepAlive=true` `RunAtLoad=true` — auto-restarts within 30s of crash |
| [**Goals review**](http://127.0.0.1:3100/api/goals) | `GET /api/goals` | All 20 active strategic goals with progress + gap analysis |
| [**Agent review**](http://127.0.0.1:3100/api/agents) | `GET /api/agents` | All 50 agents: last run, output quality, current assignment |
| [**Task triage**](http://127.0.0.1:3100/api/tasks) | `GET /api/tasks` | 28 KPI tasks: re-prioritize by urgency + impact |
| [**Decision log**](http://127.0.0.1:3100/api/decisions) | `POST /api/decisions` | Every decision logged with timestamp + reasoning |
| [**Escalation**](http://127.0.0.1:3100/api/alerts) | `POST /api/alerts` | Critical-only escalation to HMZ — threshold: budget >$500 or KPI RED |
| [**Intel injection**](http://127.0.0.1:3100/api/intel) | `GET /api/intel/latest` | Competitor intel + market trends injected into CEO context every cycle |

### 🔥 Hot

| Feature | Location | Description |
|---------|----------|-------------|
| [**Manual trigger**](http://127.0.0.1:3100/api/ceo-loop/trigger) | `POST /api/ceo-loop/trigger` | Force immediate CEO cycle — useful after major changes |
| [**Idempotent design**](launchagent/) | Built-in mutex | Second trigger exits immediately if loop already running — no duplicate actions |
| [**Context enrichment**](http://127.0.0.1:3100) | All engines feed CEO | Intel + trends + KPI + leads all auto-inject into CEO context each cycle |

---

## ⚙️ LOOP ARCHITECTURE

```
Every 6 hours (LaunchAgent):
────────────────────────────
1. GET /api/goals        → identify gaps + progress
2. GET /api/agents       → health check all 50 agents
3. GET /api/tasks        → re-prioritize 28 KPI tasks
4. GET /api/intel/latest → inject competitor context
5. GET /api/trends/latest → inject market signals
6. DECIDE               → reassign, reprioritize, note
7. POST /api/decisions   → log all decisions
8. POST /api/alerts      → escalate critical only
────────────────────────────
Total runtime: ~2-3 minutes
```

---

## 💡 TIPS AND TRICKS (16)

[Ops](#tips-ops) · [API](#tips-api) · [Authority](#tips-auth) · [Debug](#tips-debug)

<a id="tips-ops"></a>■ **Operations (5)**

| Tip | Source |
|-----|--------|
| CEO loop is the master context — all 6 engines report to it | [Architecture](../hmz-digiminds-ceo/) |
| Loop runs silently — check `/api/decisions` not logs for what it decided | [Transparency](http://127.0.0.1:3100) |
| All decisions are idempotent — safe to re-trigger after failures | [Design](launchagent/) |
| Tier 0 models for all CEO reasoning — zero Claude tokens consumed | [G0DM0D3](../hmz-g0dm0d3/) |
| Daily summary auto-generated at midnight — 24h strategic overview | [Feature](http://127.0.0.1:3100) |

<a id="tips-api"></a>■ **API (4)**

| Tip | Source |
|-----|--------|
| `curl http://127.0.0.1:3100/api/status` — first health check on every session | [API ref](http://127.0.0.1:3100) |
| `GET /api/decisions?date=today&limit=10` — last 10 decisions today | [API ref](http://127.0.0.1:3100) |
| `POST /api/ceo-loop/trigger` — manual cycle on demand | [API ref](http://127.0.0.1:3100) |
| Company ID always `c5066522-bacc-4a28-b700-6590cbe366ec` in all API calls | [Config](../hmz-digiminds-ceo/) |

<a id="tips-auth"></a>■ **Authority (4)**

| Tip | Source |
|-----|--------|
| CEO loop never acts on budget >$500 autonomously — hardcoded limit | [Authority matrix](../hmz-digiminds-ceo/) |
| HMZ override: `POST /api/decisions/override` with `{decision_id, override}` | [Override API](http://127.0.0.1:3100) |
| Escalations logged separately in `/api/alerts` — review daily | [Transparency](http://127.0.0.1:3100) |
| "HMZ is irreplaceable" is hardcoded in CEO loop — it never tries to replace HMZ | [Design principle](launchagent/) |

<a id="tips-debug"></a>■ **Debug (3)**

| Tip | Source |
|-----|--------|
| API 503 → `launchctl start ai.hmz.paperclip` | [Runbook](../hmz-digiminds-ceo/) |
| Loop didn't run at expected time → check `launchctl list \| grep paperclip` | [Debug](launchagent/) |
| Logs at `~/Library/Logs/paperclip-ceo-loop.log` + `paperclip-ceo-loop-error.log` | [Log location](launchagent/) |

---

## ☠️ STARTUPS / BUSINESSES

| Feature | Replaced |
|-|-|
| **Autonomous CEO review loop** | Weekly manual CEO meetings + [Notion](https://notion.so) status updates |
| **50-agent health monitoring** | Manual Slack check-ins with team members |
| **KPI task triage (every 6h)** | Monthly OKR reviews — too slow to course-correct |
| **Decision logging** | Verbal decisions in meetings with no audit trail |
| **Critical-only escalation** | Everything escalated to HMZ — bottleneck |

---

## Star History

[![Star History Chart](https://api.star-history.com/svg?repos=hmzainjamil/hmz-paperclip-ceo-loop&type=Date)](https://star-history.com/#hmzainjamil/hmz-paperclip-ceo-loop&Date)