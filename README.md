# NexusAI — The A2A Orchestrator for CROO

> *One task. Multiple agents. One bill. One receipt.*

---

## The Problem

Right now, if you want to do something serious in Web3 — say, invest in a new DeFi protocol — you have to do five things manually:

- Audit the smart contract for vulnerabilities
- Check if the deployer wallet has a suspicious history
- Monitor if any stablecoins in the protocol are at risk of depegging
- Research the protocol's on-chain track record
- Pull all of that together into one decision

Each of those is a separate tool, a separate tab, a separate cost, and a separate wait. There is no single agent that does all of it for you, pays the right specialists automatically, and hands you back one clean answer with a verifiable record of what was done.

That gap is exactly what NexusAI fills.

---

## What NexusAI Does

NexusAI is an A2A orchestrator built on the CROO Agent Protocol. You give it one task in plain English. It figures out which specialist agents to hire, shows you the cost upfront, pays them on-chain in USDC, collects their outputs, and assembles everything into a single professional report — with a tamper-proof receipt of every transaction logged on Base.

You deal with one agent. NexusAI deals with the rest.

---

## How It Works — Step by Step

```
You → "Audit this contract, check this wallet, alert me of DeFi risks"
         ↓
   NexusAI reads your task
   LLM builds an execution plan
         ↓
   Cost Preview shown to you
   "Aegis 0.01 + Intel 0.05 + DepegGuard 0.02 = 0.08 USDC. Approve?"
         ↓  you say yes
   NexusAI hires agents via CROO CAP
   ┌─────────────┬──────────────────┬──────────────┐
   │   Aegis     │  Address Intel   │  DepegGuard  │
   │  (audit)    │  (wallet check)  │  (DeFi risk) │
   └─────────────┴──────────────────┴──────────────┘
         ↓  all run in parallel
   Results collected
   Final report assembled by LLM
   On-chain receipt generated (SHA-256 hash)
         ↓
   You receive: report + receipt + agent ratings
```

---

## Key Features

**Cost Preview / Shopping Cart**
Before a single USDC moves, NexusAI shows you exactly which agents it will hire, what each costs, and the total. You approve or cancel. No surprises.

**Parallel Execution**
Independent sub-tasks run simultaneously — not one after another. A 3-agent job takes the time of the slowest agent, not the sum of all three.

**On-chain Job Receipt**
Every completed job produces a receipt: agents hired, amounts paid, transaction hashes, and a SHA-256 hash of the final report. This is verifiable, permanent proof of what was done and what was paid.

**Agent Reputation Scoring**
After each job, NexusAI lets you rate sub-agents 1–5 stars. Ratings are submitted back to CROO, contributing to the network's trust layer.

**Automatic Key Rotation**
NexusAI runs four Groq API keys in rotation — if one hits a rate limit, it switches to the next automatically. No downtime mid-job.

**Mock Mode for Testing**
When real agents are not yet live on the CROO Store, NexusAI falls back to realistic mock responses so the full pipeline can be tested end-to-end at any time.

---

## Why This Wins on the Judging Criteria

| Criterion | How NexusAI addresses it |
|---|---|
| Technical execution (30%) | Full CAP integration — negotiate, lock, deliver, clear. Parallel + sequential execution engine. On-chain settlement on Base. |
| A2A composability (25%) | NexusAI actively hires other agents as dependencies — Aegis, Address Intel, DepegGuard. This is the composability CROO is built for. |
| Innovation (20%) | No other submission orchestrates multiple agents, previews cost, and issues a verifiable receipt in one flow. |
| Usability / adoption (15%) | Plain English input. Cost preview builds trust. One output instead of five. Anyone can use it. |
| Presentation (10%) | Clean demo — one task in, full report out, receipt on-chain. |

---

## Tracks

- **Open — Any A2A Agents** (primary) — NexusAI is a pure A2A orchestrator that proves multi-agent composability end-to-end.
- **Developer Tooling Agents** (secondary) — NexusAI makes it easy for anyone to access the CROO agent ecosystem through a single natural-language interface.

---

## Tech Stack

| Layer | What |
|---|---|
| Orchestration brain | Groq API — `llama-3.3-70b-versatile` (primary), `mixtral-8x7b-32768` (assembly) |
| Sub-agent communication | CROO SDK (`croo-sdk`) via CAP |
| Payment | USDC on Base via CROO escrow |
| Execution | Python — parallel via `ThreadPoolExecutor`, async via `asyncio` |
| Deployment | Railway (always-on, WebSocket persistent) |

---

## Setup Instructions

**1 — Clone the repo**
```bash
git clone https://github.com/Tamil27092005/nexusai-croo
cd nexusai-croo
```

**2 — Install dependencies**
```bash
pip install croo-sdk groq requests nest_asyncio
```

**3 — Set environment variables**
```bash
export CROO_API_URL="https://api.croo.network"
export CROO_WS_URL="wss://api.croo.network/ws"
export CROO_SDK_KEY="croo_sk_..."
export GROQ_KEY_1="gsk_..."
export GROQ_KEY_2="gsk_..."
export GROQ_KEY_3="gsk_..."
export GROQ_KEY_4="gsk_..."
```

**4 — Run**
```bash
python croo.py
```

**5 — Or test in Google Colab**
Open `nexusai_colab.ipynb`, paste your keys into Cell 2, run cells 1–15 in order. Cell 14 runs a full live job. Cell 15 runs automatically with no prompts.

---

## SDK Methods Used

- `AgentClient` — initialises agent identity and wallet on CROO
- `Config` — sets base URL and WebSocket URL
- `/v1/agent/me` — verifies agent registration and connection
- `/v1/services` — discovers available agents on the CROO Store
- `/v1/orders/negotiate` — initiates A2A negotiation with a sub-agent
- `/v1/orders/{id}/pay` — locks funds into escrow
- `/v1/orders/{id}` — polls order status (lock → deliver → clear)
- `/v1/orders/{id}/delivery` — retrieves completed delivery from sub-agent
- `/v1/orders/rate` — submits reputation rating for a completed order

---

## CROO Agent Store Listing

**Agent name:** NexusAI Orchestrator
**Price:** 0.10 USDC per job
**Role:** Provider + Requester (full pair)
**Network:** Base Mainnet
**Capability:** Multi-agent task orchestration — research, audit, verification, DeFi risk — in one call

---

## License

MIT License — open source, freely usable, forkable.

---

## Team

Built for the CROO AI Agent Hackathon 2026.
Submitted via DoraHacks — dorahacks.io/hackathon/croo-hackathon
