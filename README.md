# hmz-paperclip-ceo-loop
Paperclip AI CEO Loop — autonomous strategic decision engine running 24/7 as company co-founder.

![loop](https://img.shields.io/badge/mode-24%2F7_autonomous-orange?style=flat&labelColor=555)
![paperclip](https://img.shields.io/badge/platform-Paperclip_AI-blue?style=flat&labelColor=555)
![status](https://img.shields.io/badge/status-always_on-green?style=flat&labelColor=555)
![tier0](https://img.shields.io/badge/cost-Tier0_models-brightgreen?style=flat&labelColor=555)
![license](https://img.shields.io/badge/license-MIT-blue?style=flat&labelColor=555)

[Concepts](#-concepts) · [Architecture](#️-architecture) · [Tips](#-tips-and-tricks-20) · [Kills](#️-startups--businesses) · [Stars](#star-history)

## 🧠 CONCEPTS

| Feature | Location | Description |
|---------|----------|-------------|
| [**OODA Decision Loop**](loop/ooda.js) | `loop/ooda.js` | Observe-Orient-Decide-Act at company level — runs every 15 minutes [![core](https://img.shields.io/badge/pattern-OODA-orange?style=flat&labelColor=555)] |
| [**KPI Observer**](loop/observe.js) | `loop/observe.js` | Ingests revenue, pipeline, traffic, ROAS — builds current-state snapshot |
| [**Strategic Orienter**](loop/orient.js) | `loop/orient.js` | Models opportunities vs threats — priority ranking from KPI deltas |
| [**Decision Engine**](loop/decide.js) | `loop/decide.js` | Commits to action plan — no flip-flopping, logs every decision with rationale |
| [**Action Executor**](loop/act.js) | `loop/act.js` | Dispatches actions to BDM, Content, Intel engines — measures outcomes |
| [**Memory Layer**](loop/memory.js) | `loop/memory.js` | Persists decisions + outcomes — feeds next OODA cycle |
| [**Escalation Handler**](loop/escalate.js) | `loop/escalate.js` | Flags decisions above threshold to human (Slack/email) — human-in-loop |
| [**Tier 0 Dispatcher**](loop/dispatch.js) | `loop/dispatch.js` | Routes every sub-task to cheapest capable model — never Claude for internals |
| [**LaunchAgent Config**](launchagent/ai.hmz.ceo-loop.plist) | `launchagent/ai.hmz.ceo-loop.plist` | KeepAlive daemon — CEO loop restarts within 10s of crash |

### 🔥 Hot

| Feature | Location | Description |
|---------|----------|-------------|
| [**Paperclip Sync**](paperclip/sync.js) | `paperclip/sync.js` | Syncs decisions to Paperclip AI OS at 127.0.0.1:3100 — company ID c5066522 |
| [**Revenue Radar**](loop/revenue-radar.js) | `loop/revenue-radar.js` | Detects MRR drops >10% — triggers emergency BDM outreach automatically |
| [**Weekly CEO Report**](reports/weekly.py) | `reports/weekly.py` | ReportLab CEO summary — decisions made, outcomes, pipeline status |

## ⚙️ ARCHITECTURE

```
CEO Loop (15-min cycle):

  OBSERVE: KPIs + pipeline + content metrics
      │
  ORIENT: delta analysis + opportunity ranking
      │
  DECIDE: action selection + rationale log
      │
  ACT: dispatch to engines
      │
      ├─ BDM Engine (lead gen + outreach)
      ├─ Content Engine (posts + case studies)
      ├─ Intel Engine (competitor + trends)
      └─ KPI Monitor (alert on threshold breach)
      │
  MEMORY: store decision + outcome
      │
  LOOP (15 min later)
```

| Decision Type | Threshold | Action | Model |
|-------------|----------|--------|-------|
| Revenue drop | >10% MRR | Emergency BDM sweep | Groq |
| Pipeline dry | <3 active leads | LinkedIn outreach burst | GPT-4o-mini |
| Content gap | >48h since post | Generate + schedule | Gemini |
| Competitor move | Price change detected | Update proposals | DeepSeek |
| Positive: new client | Signed contract | Update pipeline + celebrate | Groq |

## 💡 TIPS AND TRICKS (20)

[loop](#tips-loop) · [decisions](#tips-decisions) · [escalation](#tips-escalation) · [integration](#tips-integration)

<a id="tips-loop"></a>■ **Loop Configuration (5)**

| Tip | Source |
|-----|--------|
| 15-minute cycle sweet spot — faster wastes tokens, slower misses time-sensitive actions | [HMZ](https://github.com/hmzainjamil) |
| `KeepAlive=true` in LaunchAgent — CEO never stops, even after crash or sleep | [HMZ](https://github.com/hmzainjamil) |
| Log every OODA cycle to `~/.claude/logs/ceo-loop.log` — weekly review mandatory | [HMZ](https://github.com/hmzainjamil) |
| Memory layer uses append-only JSONL — never overwrite, always append decisions | [HMZ](https://github.com/hmzainjamil) |
| `curl localhost:3100/health` — verify Paperclip OS running before loop starts | [HMZ](https://github.com/hmzainjamil) |

<a id="tips-decisions"></a>■ **Decision Quality (5)**

| Tip | Source |
|-----|--------|
| Every decision needs rationale logged — why this action, why now, expected outcome | [HMZ](https://github.com/hmzainjamil) |
| Never reverse a decision within same cycle — OODA says commit and measure | [HMZ](https://github.com/hmzainjamil) |
| Priority: revenue protection > growth > optimization — in that order always | [HMZ](https://github.com/hmzainjamil) |
| Small decisions: autonomous. Large decisions (>$500 impact): escalate to human | [HMZ](https://github.com/hmzainjamil) |
| Measure every action's outcome in next OODA cycle — feedback loop is mandatory | [HMZ](https://github.com/hmzainjamil) |

<a id="tips-escalation"></a>■ **Human-in-Loop (5)**

| Tip | Source |
|-----|--------|
| Slack webhook for escalations — CEO pings human for decisions above threshold | [HMZ](https://github.com/hmzainjamil) |
| Escalation criteria: irreversible actions, >$500 impact, reputation risk | [HMZ](https://github.com/hmzainjamil) |
| Always include context in escalation: KPI snapshot + decision rationale + options | [HMZ](https://github.com/hmzainjamil) |
| If no human response in 2h, CEO selects lowest-risk option autonomously | [HMZ](https://github.com/hmzainjamil) |
| Weekly CEO report PDF — human reviews decisions made, outcomes, next week plan | [HMZ](https://github.com/hmzainjamil) |

<a id="tips-integration"></a>■ **Paperclip Integration (5)**

| Tip | Source |
|-----|--------|
| Company ID `c5066522-bacc-4a28-b700-6590cbe366ec` — required for all Paperclip calls | [HMZ](https://github.com/hmzainjamil) |
| All CEO decisions sync to Paperclip memory — persists across sessions | [HMZ](https://github.com/hmzainjamil) |
| Paperclip OS at 127.0.0.1:3100 — local, zero cloud cost for core loop | [HMZ](https://github.com/hmzainjamil) |
| CEO loop and Paperclip share same memory layer — one source of truth | [HMZ](https://github.com/hmzainjamil) |
| Always route CEO loop sub-tasks to Tier 0 — never Claude tokens for internals | [HMZ](https://github.com/hmzainjamil) |

## ☠️ STARTUPS / BUSINESSES

| Feature | Replaced |
|-|-|
| **Autonomous CEO Loop** | [Lindy AI](https://lindy.ai), [Beam AI](https://beam.ai), [Artisan](https://artisan.co), [11x.ai](https://11x.ai) |
| **OODA Decision Framework** | [Notion AI](https://notion.so/ai), [Monday AI](https://monday.com/ai) |
| **Human-in-Loop Escalation** | [Zapier](https://zapier.com), [Make.com](https://make.com) |
| **KPI-Driven Actions** | [Databox](https://databox.com), [Klipfolio](https://klipfolio.com) |
| **Memory + Decision Log** | [Mem.ai](https://mem.ai), [Rewind AI](https://rewind.ai) |

## Star History

[![Star History Chart](https://api.star-history.com/svg?repos=hmzainjamil/hmz-paperclip-ceo-loop&type=Date)](https://star-history.com/#hmzainjamil/hmz-paperclip-ceo-loop&Date)
