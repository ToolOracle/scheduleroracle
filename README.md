# SchedulerOracle

**The motor. MemoryOracle is the brain — SchedulerOracle makes it act.**

Persistent autonomous task scheduler for AI agents. Schedule once, run forever. Cron, interval, or one-time. Results auto-stored in MemoryOracle. Optional Decision Preflight gate.

```
npx -y mcp-remote https://mcp.feedoracle.io/scheduler/mcp/
```

## The problem

AI agents are session-bound. When the chat ends, the agent stops. No monitoring. No recurring checks. No autonomous work.

SchedulerOracle turns agents into 24/7 workers:

```
Agent: "Check RLUSD MiCA status every day at 9am"
  → SchedulerOracle: task-dfa88a8101 scheduled (cron: 0 9 * * *)
  → Tomorrow 09:00 UTC: Decision Preflight runs → verdict: CAUTION
  → Result auto-stored in MemoryOracle (mem-ef455216e979)
  → Next session: agent instantly knows RLUSD status changed
```

## Tools

| Tool | Units | Price | What it does |
|------|-------|-------|-------------|
| `schedule_task` | 8 | $0.08 | Create cron, interval, or one-time task |
| `run_now` | 12 | $0.12 | Execute immediately, regardless of schedule |
| `list_tasks` | 2 | $0.02 | Show all tasks with status and next run |
| `cancel_task` | 2 | $0.02 | Delete a task permanently |
| `pause_task` | 2 | $0.02 | Pause or resume a task |
| `task_history` | 3 | $0.03 | Execution log with duration and errors |
| `task_stats` | 1 | $0.01 | Dashboard: active/failed/success rate |
| `export_tasks` | 3 | $0.03 | Export all tasks as JSON |
| `health_check` | 0 | free | Status + available target servers |

## Available target servers

Any MCP server in the ToolOracle + FeedOracle ecosystem:

| Server | Tools available |
|--------|---------------|
| `compliance` | MiCA preflight, evidence bundle, provenance, AI explain |
| `macro` | Fed rates, inflation, yield curve, GDP |
| `risk` | Stablecoin risk, custody, market depth |
| `iso20022` | DTI lookup, SWIFT deadlines, MiCA cross-check |
| `preflight` | Decision Preflight (go/caution/stop) |
| `memory` | Store/query long-term memory |
| `trust` | Verify claims, signed facts, provenance |
| `meme` | Trending memes, rug checks |
| `yield` | DeFi yields, RWA yields |
| `dora` | CVE search, CERT-Bund, breach checks |
| + 10 more | rank, shop, smart, flight, hotel, news, jobs, carbon, reserve, ampel |

## The autonomous agent stack

```
SchedulerOracle (the motor)
    ↓ triggers
Decision Preflight (the gate)
    ↓ if go/caution
Any MCP Tool (compliance, macro, yield...)
    ↓ result
MemoryOracle (the brain)
    ↓ persists
Next session: agent remembers everything
```

## Example: Daily compliance monitoring

```json
{
  "name": "schedule_task",
  "arguments": {
    "name": "Daily RLUSD MiCA Check",
    "schedule_type": "cron",
    "cron": "0 9 * * *",
    "target_server": "preflight",
    "target_tool": "decision_preflight",
    "target_args": {
      "claim": "Recommend RLUSD for EU settlement",
      "asset": "RLUSD",
      "risk_profile": "eu_mica"
    },
    "store_in_memory": true,
    "memory_importance": 8,
    "namespace": "compliance-bot"
  }
}
```

## x402 Pay-per-call

```
POST https://tooloracle.io/x402/scheduler/mcp/
```

No account. No API key. USDC on Base.

## Connect

```json
{
  "mcpServers": {
    "scheduler": {
      "command": "npx",
      "args": ["-y", "mcp-remote", "https://mcp.feedoracle.io/scheduler/mcp/"]
    }
  }
}
```

## Part of ToolOracle

SchedulerOracle completes the autonomous agent stack:

- **MemoryOracle** — persistent memory (the brain)
- **SchedulerOracle** — task scheduling (the motor)
- **Decision Preflight** — compliance gate (the filter)
- **Trust Layer** — evidence verification (the proof)

Together: [ToolOracle](https://tooloracle.io) — 50+ MCP servers, 530+ tools.


## Read More

📝 [We Built an AI Agent That Runs 24/7, Never Forgets, and Checks Its Own Work](https://tooloracle.io/blog/autonomous-ai-agent-memory-scheduler-mcp) — How Memory + Scheduler + Decision Preflight work together as one integrated autonomous agent stack. Real tool outputs, no theory.

## License

MIT
