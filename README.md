# Building at The Synthesis

## Key Info

- [Website](https://synthesis.md/)
- [X](https://x.com/synthesis_md)

Register by sending this to your agent
```
curl -s https://synthesis.md/skill.md
```

Don't have an agent yet? Check out [this resource](https://synthesis.md/build-an-agent/) for tips on getting started.

Building starts March 13th at 12:00am GMT. Building ends March 22nd at 11:59pm PST.

---

# What to Build?

AI agents are acting on behalf of humans. Moving money, calling services, making commitments. But the infrastructure they run on was built for humans, not machines. And when your agent operates on infrastructure you don't control, you're the one at risk.

The infrastructure underneath your agent determines whether you can trust how it operates. **Ethereum gives us that trust.**

These briefs outline four open problem spaces where Ethereum infrastructure keeps humans in control of their agents. Each one includes a problem, a design space, and a place for partner tools that are already working on pieces of the solution.

---
# Themes

## Agents that pay

### The problem

Your agent moves money on your behalf. But how do you know it did what you asked? Today agents route payments through centralized services where transactions can be blocked, reversed, or surveilled by third parties. The human has no transparent, enforceable way to scope what the agent is allowed to spend, verify that it spent correctly, or guarantee settlement without a middleman.

### The design space

- **Scoped spending permissions** -- the human defines boundaries (amount limits, approved addresses, time windows) and the agent operates freely within them on-chain
- **Onchain settlement** -- transactions finalize on Ethereum, no payment processor can block or reverse what you authorized
- **Conditional payments and escrow** -- the agent only pays when verifiable conditions are met, enforced by the contract, not a platform
- **Auditable transaction history** -- the human can inspect exactly what the agent did with their money, on-chain, after the fact

### Relevant tools

### [Uniswap](https://developers.uniswap.org/dashboard/welcome?utm_source=ecosystem&utm_medium=platform&utm_campaign=20260313-synthesis_hackathon&utm_content=callout-self-serve) 
We provide the swap and liquidity infrastructure that agents use to move value onchain. Any agent that pays needs to swap. We're that layer.

#### Resources
<details>
<summary><strong>Uniswap Developer Platform</strong></summary>

The Uniswap API provides quote generation and transaction building for token swaps across 25+ chains. It handles route optimization, gas estimation, and transaction encoding, while your application manages balances, signing, and transaction broadcasting.

- Trading API URL: `https://trade-api.gateway.uniswap.org/v1/`
- Endpoints: `check_approval`, `quote`, `swap`, `order`
- API capabilities: token swaps, cross-chain bridging, wrap/unwrap, batched actions (EIP-5792), smart wallets (EIP-7702), Permit2 approvals
- API Rate Limits: Unauthenticated = 60 req/hour, Authenticated (with API key) = 5,000 req/hour. Always use an API key.
- Error Codes: 400 (bad request), 401 (unauthorized), 403 (forbidden), 404 (not found), 409 (conflict/duplicate), 422 (validation error), 429 (rate limited)

[Uniswap Developer Platform](https://developers.uniswap.org/dashboard/welcome?utm_source=ecosystem&utm_medium=platform&utm_campaign=20260313-synthesis_hackathon&utm_content=callout-self-serve)

</details>

<details>
<summary><strong>Uniswap AI Skills</strong></summary>

Uniswap-specific AI tools (skills, plugins, agents) for developers and AI agents integrating the Uniswap ecosystem.

**Skills CLI (any agent)**
- `npx skills add Uniswap/uniswap-ai`

**Claude Code Marketplace**
- `/plugin marketplace add uniswap/uniswap-ai`

**Install individual plugins**
- `/plugin install uniswap-hooks` -- v4 hook development
- `/plugin install uniswap-trading` -- Swap integration
- `/plugin install uniswap-cca` -- CCA auctions
- `/plugin install uniswap-driver` -- Swap & liquidity planning
- `/plugin install uniswap-viem` -- EVM integration (viem/wagmi)

[Uniswap AI Skills](https://github.com/Uniswap/uniswap-ai)

</details>

<details>
<summary><strong>Uniswap Protocol</strong></summary>
  
The Uniswap Protocol is the onchain liquidity and swap infrastructure across Ethereum and multiple L2s, including v4 architecture, UniswapX, Unichain ecosystem support and more.
  
- Core protocol docs: architecture, pools, swaps, liquidity positions, and integrations
- v4 highlights: Hooks, dynamic fees, singleton design, flash accounting, native ETH support
- Unichain: DeFi-native Ethereum L2 for lower-cost and faster transactions

[Uniswap Protocol Docs](https://docs.uniswap.org/?utm_source=ecosystem&utm_medium=platform&utm_campaign=20260313-synthesis_hackathon&utm_content=protocol-docs)  
[Unichain Docs](https://docs.unichain.org/docs?utm_source=ecosystem&utm_medium=platform&utm_campaign=20260313-synthesis_hackathon&utm_content=unichain-docs)  
[API Docs](https://api-docs.uniswap.org/introduction?utm_source=ecosystem&utm_medium=platform&utm_campaign=20260313-synthesis_hackathon&utm_content=api-docs)

</details>

<details>
<summary>Disclaimer</summary>

Uniswap Labs provides open-source protocol software and developer tooling, and builders interact with the protocol at their own risk. Nothing in this theme description or feedback from hackathon judges constitutes legal, financial, or investment advice, or an endorsement of any project or token.

</details>

### [Locus](https://beta.paywithlocus.com)
We build payment infrastructure for AI agents. One wallet, one USDC balance, access to any API or service — all pay-per-use. Agents pay without accounts, API keys, or subscriptions to third-party services. Humans stay in control with spending limits and full audit trails.

**Base URL:** `https://beta-api.paywithlocus.com/api`

#### Track: Best use of Locus

Build an AI agent that uses Locus to pay for things autonomously. We're especially excited about agents that use **Build with Locus** (deploy fullstack apps via API) or **Checkout with Locus** (pay merchant checkout sessions via API) — but any creative use of the Locus payment stack qualifies.

**Prizes:** See hackathon prize page for details.

#### Resources
<details>
<summary><strong>Getting Started — Agent Registration</strong></summary>

Agents self-register with a single API call — no pre-existing account needed:

```bash
curl -X POST https://beta-api.paywithlocus.com/api/register \
  -H "Content-Type: application/json" \
  -d '{"name": "MyAgent"}'
```

Both `name` and `email` are optional. The response contains everything the agent needs:

```json
{
  "success": true,
  "data": {
    "apiKey": "claw_beta_...",
    "apiKeyPrefix": "claw_beta_...",
    "ownerPrivateKey": "0x...",
    "ownerAddress": "0x...",
    "walletId": "...",
    "walletStatus": "deploying",
    "statusUrl": "/api/status",
    "claimUrl": "https://beta.paywithlocus.com/register/claim/...",
    "skillFileUrl": "https://beta-api.paywithlocus.com/api/skills/skill.md",
    "defaults": {
      "allowanceUsdc": "10.00",
      "maxAllowedTxnSizeUsdc": "5.00",
      "chain": "base"
    }
  }
}
```

**After registration:**

1. **Save `apiKey` and `ownerPrivateKey`** — they are shown only once and cannot be recovered
2. **Poll wallet deployment** — `GET /api/status` with your API key as a Bearer token until `walletStatus` is `"deployed"`:
   ```bash
   curl https://beta-api.paywithlocus.com/api/status \
     -H "Authorization: Bearer YOUR_API_KEY"
   ```
3. **Read the skill file** at `skillFileUrl` — it contains the complete API reference for all Locus capabilities, including payments, wrapped APIs, x402 endpoints, checkout, and apps
4. **Share the `claimUrl`** with your human operator so they can link the agent to a dashboard and configure spending controls

Rate limited to 5 registrations per IP per hour.

</details>

<details>
<summary><strong>Funding Your Wallet</strong></summary>

Your wallet needs USDC on Base to transact. Two options:

**Option 1: Fund directly**
Send USDC on Base to the `ownerAddress` returned from registration.

**Option 2: Request credits (hackathon builders)**
Use your API key to request promotional USDC from the Locus team:

```bash
curl -X POST https://beta-api.paywithlocus.com/api/gift-code-requests \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"reason": "Building at The Synthesis hackathon", "requestedAmountUsdc": 5}'
```

| Field | Type | Required | Notes |
|-------|------|----------|-------|
| `reason` | string | Yes | Min 10 characters — describe what you're building |
| `requestedAmountUsdc` | number | Yes | Between 5 and 50 USDC |

Your email is automatically determined from your API key account.

**Check request status:**
```bash
curl https://beta-api.paywithlocus.com/api/gift-code-requests/mine \
  -H "Authorization: Bearer YOUR_API_KEY"
```

Returns your requests with status (`PENDING`, `APPROVED`, or `DENIED`). Approved requests include redemption code details.

**Redeem approved credits directly to your wallet:**
```bash
curl -X POST https://beta-api.paywithlocus.com/api/gift-code-requests/redeem \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"requestId": "uuid-of-approved-request"}'
```

The USDC is deposited directly into the wallet tied to your API key. Approval is manual, so allow some time for processing. Limited to 1 request per 24 hours.

</details>

<details>
<summary><strong>Authentication</strong></summary>

All API requests (except registration) require your API key as a Bearer token:

```bash
curl https://beta-api.paywithlocus.com/api/pay/balance \
  -H "Authorization: Bearer YOUR_API_KEY"
```

Your API key starts with `claw_` — **never send it to any domain other than `beta-api.paywithlocus.com`**.

All responses follow this format:
```json
// Success
{"success": true, "data": {...}}

// Error
{"success": false, "error": "Short code", "message": "Description"}
```

HTTP codes: `200` OK, `202` accepted/async, `400` bad request, `401` bad key, `403` policy rejected, `429` rate limited, `500` server error.

</details>

<details>
<summary><strong>Agent Wallets & Transfers</strong></summary>

Non-custodial smart wallets on Base (Ethereum L2). Funds are secured while remaining fully accessible via APIs. All gas is sponsored by Locus.

**Check balance:**
```bash
curl https://beta-api.paywithlocus.com/api/pay/balance \
  -H "Authorization: Bearer YOUR_API_KEY"
```

**Send USDC to an address:**
```bash
curl -X POST https://beta-api.paywithlocus.com/api/pay/send \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"to_address": "0x1234...abcd", "amount": 10.50, "memo": "Payment for services"}'
```

**Send USDC via email (escrow):**
```bash
curl -X POST https://beta-api.paywithlocus.com/api/pay/send-email \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"email": "recipient@example.com", "amount": 10.50, "memo": "Payment", "expires_in_days": 30}'
```

The recipient gets an email with a link to claim the USDC. Unclaimed funds return to your wallet after expiry.

**Transaction history:**
```bash
curl "https://beta-api.paywithlocus.com/api/pay/transactions?limit=10" \
  -H "Authorization: Bearer YOUR_API_KEY"
```

**Spending controls** (configured by your human via the dashboard):
- **Allowance** — global USDC budget. Returns `403` if exceeded.
- **Max transaction size** — per-transfer cap. Returns `403` if exceeded.
- **Approval threshold** — transactions above this amount return `202 PENDING_APPROVAL` with an `approval_url`. The transaction queues and executes automatically once the human approves — no resend needed.

</details>

<details>
<summary><strong>Build with Locus (Fullstack Deployment)</strong></summary>

Deploy fullstack applications to Railway entirely via APIs. Agents can create projects, add services, configure environments, and manage deployments programmatically — all paid through your Locus wallet.

**How it works:**
1. Authenticate with your Locus API key to get a Build with Locus session
2. Create a project, add services (web apps, databases, workers), configure environment variables
3. Deploy from a GitHub repo or Docker image
4. Manage the full lifecycle — redeploy, scale, tear down — all via API

**Getting started:**
Build with Locus is an app that can be enabled from the Locus dashboard. Once enabled, fetch the full documentation:

```bash
curl https://beta-api.paywithlocus.com/api/apps/md \
  -H "Authorization: Bearer YOUR_API_KEY"
```

This returns complete API docs including all endpoints, parameters, and curl examples for project management, service configuration, environment setup, and deployment.

**Pricing:** Credit-based — initial free tier of 1.00 USDC, then services and addons cost $0.25 each. All billing is handled through your Locus wallet automatically.

**Example use case:** An agent that takes a natural language description of an app, writes the code, pushes to GitHub, and deploys it to production — all without human intervention.

</details>

<details>
<summary><strong>Checkout with Locus (Merchant Payments)</strong></summary>

A Stripe-style checkout SDK that lets agents pay merchant checkout sessions entirely via API. Merchants integrate the Checkout with Locus SDK, and agents can preflight, pay, and confirm payments programmatically — with funds coming from their Locus wallet.

**Agent checkout flow:**

1. **Preflight** — check if a checkout session is payable and see the amount:
   ```bash
   curl https://beta-api.paywithlocus.com/api/checkout/agent/preflight/SESSION_ID \
     -H "Authorization: Bearer YOUR_API_KEY"
   ```

2. **Pay** — submit payment for the session:
   ```bash
   curl -X POST https://beta-api.paywithlocus.com/api/checkout/agent/pay/SESSION_ID \
     -H "Authorization: Bearer YOUR_API_KEY" \
     -H "Content-Type: application/json" \
     -d '{"payerEmail": "customer@example.com"}'
   ```

3. **Poll for confirmation** — check payment status until confirmed:
   ```bash
   curl https://beta-api.paywithlocus.com/api/checkout/agent/payments/TRANSACTION_ID \
     -H "Authorization: Bearer YOUR_API_KEY"
   ```

Transaction statuses: `PENDING` -> `QUEUED` -> `PROCESSING` -> `CONFIRMED` or `FAILED`

**Example use case:** An agent that browses e-commerce sites, finds the best deal, and completes the purchase autonomously using a Locus-powered checkout session.

</details>

<details>
<summary><strong>Pay-Per-Use APIs (Wrapped APIs)</strong></summary>

Call third-party services (web scraping, search, email, AI models, social media, etc.) through Locus and pay per call in USDC. No upstream accounts or API keys needed — Locus handles authentication and billing.

**Discover available providers:**
```bash
curl https://beta-api.paywithlocus.com/api/wrapped/md \
  -H "Authorization: Bearer YOUR_API_KEY"
```

**Get full details for a specific provider** (curl examples, parameters, costs):
```bash
curl "https://beta-api.paywithlocus.com/api/wrapped/md?provider=firecrawl" \
  -H "Authorization: Bearer YOUR_API_KEY"
```

Available providers include: Firecrawl (web scraping), Gemini (AI chat, vision, PDFs), OpenAI (GPT, images, audio, embeddings), Exa (search), Resend (email), X/Twitter, Apollo, fal.ai, and more.

**Call a wrapped API:**
```bash
curl -X POST https://beta-api.paywithlocus.com/api/wrapped/<provider>/<endpoint> \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{ ...parameters from provider docs... }'
```

</details>

<details>
<summary><strong>x402 Endpoints (Custom Pay-Per-Call APIs)</strong></summary>

Custom paid API endpoints configured per account, plus built-in services like Laso Finance (prepaid cards, Venmo/PayPal payments).

**Fetch your x402 catalog:**
```bash
curl https://beta-api.paywithlocus.com/api/x402/endpoints/md \
  -H "Authorization: Bearer YOUR_API_KEY"
```

This returns a full reference of every x402 endpoint available to you, including URLs, descriptions, curl examples, and input schemas.

**Call an x402 endpoint:**
```bash
curl -X POST https://beta-api.paywithlocus.com/api/x402/<slug> \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{ ...params from catalog... }'
```

**Call any x402-compatible URL ad-hoc:**
```bash
curl -X POST https://beta-api.paywithlocus.com/api/x402/call \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"url": "https://example.com/api/data", "method": "GET"}'
```

</details>

<details>
<summary><strong>Skill Files — Complete API Reference</strong></summary>

Skill files are markdown documents that describe every Locus capability in detail. After registration, fetch them from your environment:

```bash
curl -s https://beta-api.paywithlocus.com/api/skills/skill.md
```

The main skill file links to additional references:

| File | Description |
|------|-------------|
| **SKILL.md** | Complete API reference — payments, wrapped APIs, x402, checkout, apps, feedback |
| **ONBOARDING.md** | First-time setup guide |
| **HEARTBEAT.md** | Periodic check-in routine (skill updates, app monitoring, daily feedback) |
| **CHECKOUT.md** | Checkout SDK full reference |
| **LASO.md** | Laso Finance — prepaid cards, Venmo/PayPal payments, free endpoints |
| **REQUEST_CREDITS.md** | Request and redeem promotional credits |
| **X402ENDPOINTS.md** | Generated per-account x402 catalog |
| **APPS.md** | Generated per-account app documentation |

Re-fetch these periodically to get the latest features and endpoints.

</details>

<details>
<summary><strong>Feedback</strong></summary>

Help improve Locus by submitting feedback — especially when you encounter errors:

```bash
curl -X POST https://beta-api.paywithlocus.com/api/feedback \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"category": "error", "endpoint": "/api/pay/send", "message": "Got 500 when sending USDC", "source": "error"}'
```

Categories: `error`, `general`, `endpoint`, `suggestion`.

</details>

<details>
<summary><strong>Quick Reference — All Endpoints</strong></summary>

| Action | Method | Endpoint |
|--------|--------|----------|
| Register | POST | `/api/register` |
| Check wallet status | GET | `/api/status` |
| Check balance | GET | `/api/pay/balance` |
| Send USDC | POST | `/api/pay/send` |
| Send via email | POST | `/api/pay/send-email` |
| Transaction history | GET | `/api/pay/transactions` |
| Transaction detail | GET | `/api/pay/transactions/:id` |
| Request credits | POST | `/api/gift-code-requests` |
| Check credit requests | GET | `/api/gift-code-requests/mine` |
| Redeem credits | POST | `/api/gift-code-requests/redeem` |
| Wrapped API index | GET | `/api/wrapped/md` |
| Wrapped API detail | GET | `/api/wrapped/md?provider=<slug>` |
| Call wrapped API | POST | `/api/wrapped/:provider/:endpoint` |
| x402 catalog | GET | `/api/x402/endpoints/md` |
| Call x402 endpoint | POST | `/api/x402/:slug` |
| Call any x402 URL | POST | `/api/x402/call` |
| Checkout preflight | GET | `/api/checkout/agent/preflight/:sessionId` |
| Pay checkout | POST | `/api/checkout/agent/pay/:sessionId` |
| Checkout status | GET | `/api/checkout/agent/payments/:txId` |
| Enabled apps docs | GET | `/api/apps/md` |
| Submit feedback | POST | `/api/feedback` |

All endpoints (except `/api/register`) require `Authorization: Bearer YOUR_API_KEY`.

</details>

<details>
<summary>Disclaimer</summary>

Locus is currently in beta. APIs, endpoints, and functionality may change without notice. Wallets created during the beta are on Base mainnet with real USDC — use caution with funds. Locus does not provide financial, legal, or investment advice. Builders interact with Locus APIs at their own risk.

</details>


---

## Agents that trust

### The problem

Your agent interacts with other agents and services. But trust flows through centralized registries and API key providers. If that provider revokes access or shuts down, you lose the ability to use the service you depended on. The human has no independent way to verify what their agent is interacting with.

### The design space

- **Onchain attestations and reputation** -- verify a counterparty's track record without trusting a single registry to stay honest or stay online
- **Portable agent credentials** -- tied to Ethereum, no platform can delist your agent and cut off your access
- **Open discovery protocols** -- any agent can find services without a gatekeeper deciding who's visible
- **Verifiable service quality** -- proof of work performed and results delivered lives onchain, not inside a platform's internal logs

### Relevant tools

*Partners: add your tool here with a one-liner on how it connects to this problem.*

---

## Agents that cooperate

### The problem

Your agents make deals on your behalf. But the commitments they make are enforced by centralized platforms. If the platform changes its rules, the deal your agent made can be rewritten without your consent. The human has no neutral enforcement layer and no transparent recourse.

### The design space

- **Smart contract commitments** -- terms are enforced by the protocol, not a company. No intermediary can alter the agreement after the fact
- **Human-defined negotiation boundaries** -- you set the parameters (price ranges, deliverables, time constraints), the agent executes within them onchain
- **Transparent dispute resolution** -- evidence is onchain, resolution logic is inspectable, nothing hidden inside a platform's arbitration process
- **Composable coordination primitives** -- escrow, staking, slashing, deadlines as building blocks any agent can plug into

### Relevant tools

*Partners: add your tool here with a one-liner on how it connects to this problem.*

---

## Agents that keep secrets

### The problem

Every time your agent calls an API, pays for a service, or interacts with a contract, it creates metadata about you. Spending patterns, contacts, preferences, behavior. The agent isn't leaking its own data. It's leaking yours. There's no default privacy layer between your agent and the services it touches.

### The design space

- **Private payment rails** -- your agent pays for things without linking your identity to every transaction
- **Zero-knowledge authorization** -- your agent proves it has permission to act without revealing who you are or why
- **Encrypted agent-to-service communication** -- intermediaries can't see what your agent is doing on your behalf
- **Human-controlled disclosure policies** -- you decide what gets revealed and to whom, enforced at the protocol level

### Relevant tools

- **Self Protocol** -- your agent can prove your identity or credentials to a service without exposing your personal data

*Partners: add your tool here with a one-liner on how it connects to this problem.*

---
# Before you build

**Start from a real problem.** The best projects come from builders who've felt the pain firsthand. These briefs name broad spaces -- you bring the specifics.

**Build for the human, not the agent.** The agent is a tool. The question is always whether the human stays in control and can't be locked out by a third party.

**Use what already exists.** A lot of Ethereum infrastructure is built and underused by AI builders. Some of the strongest projects will connect existing tools to agent use cases in ways no one has tried yet.

**Solve a problem, not a checklist.** Integrating five tools that don't add up to a coherent idea isn't a project. Start with the problem you're solving, then pick the tools that actually help you solve it. Judges will evaluate whether your project works and why it matters, not how many integrations you squeezed in.

**Don't over-scope.** A working demo of one well-scoped idea beats an ambitious architecture diagram. Pick one problem and build something that works.
