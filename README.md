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
We build payment infrastructure for AI agents. One wallet, one USDC balance, access to any API or service — all pay-per-use. Agents pay without accounts, API keys, or subscriptions. Humans stay in control with spending limits and full audit trails.

#### Resources
<details>
<summary><strong>Agent Wallets & Transfers</strong></summary>

Non-custodial wallets purpose-built for AI agents on Base (Ethereum L2). Funds are secured while remaining fully accessible via APIs. All gas is sponsored by Locus.

- **Direct transfers**: Wallet-to-wallet USDC transfers on Base
- **Email escrow transfers**: Spin up subwallets, load them with funds, and send payments via email with passcode-gated redemption
- **Spending controls**: Allowances (global budget), per-transaction budgets, and approval thresholds — configured in the Locus app
- **Auditability**: Agents log intent and reasoning alongside every transaction for full audit trails

</details>

<details>
<summary><strong>Pay-Per-Use APIs</strong></summary>

Stateless APIs that agents can call without creating accounts or managing API keys. Billed per-call (e.g., $0.01/call). Locus also supports custom paid APIs through the x402 protocol.

- No accounts, no API keys, no subscriptions — just pay and use
- APIs are listed on the Locus frontend and enabled/disabled per wallet
- Custom x402-compatible endpoints can be added with schema and descriptions

</details>

<details>
<summary><strong>Vertical Tools</strong></summary>

Agent-native rebuilds of existing SaaS, built to be stateful and pay-per-use via APIs.

- **Build with Locus**: Fullstack Railway deployment via APIs — deploy infrastructure programmatically with paid subscriptions managed through Locus
- **Checkout with Locus**: A Stripe-style checkout SDK that returns funds back to the payer's Locus wallet. Can be triggered and managed by agents autonomously

</details>

<details>
<summary><strong>Getting Started — Agent Registration & Skill Files</strong></summary>

Agents can self-register via a single API call — no account or API key needed:

```bash
curl -X POST https://beta-api.paywithlocus.com/api/register \
  -H "Content-Type: application/json" \
  -d '{"name": "MyAgent", "email": "optional@example.com"}'
```

Both `name` and `email` are optional. The endpoint returns everything the agent needs to start using Locus:

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

- **Save your `apiKey` and `ownerPrivateKey`** — they are only shown once
- **Share the `claimUrl`** with your human operator to link the agent to a dashboard
- **Poll `GET /api/status`** with your API key in the header to check wallet deployment
- **Read `https://beta-api.paywithlocus.com/api/skills/skill.md`** and follow the instructions to set up Locus.
- Rate limited to 5 registrations per IP per hour

Once registered, agents connect to Locus using skill files (`skill.md`) that describe available tooling and APIs. Custom skill files are generated per account based on enabled services.

- Skill files explain how to use Locus tooling, available APIs, and how to work with them
- Pay-per-use APIs and vertical tools are toggleable in the frontend, generating custom skill files per account
- Chain: Base (Ethereum L2), USDC only, with multi-EVM support planned

</details>

<details>
<summary><strong>Funding Your Wallet</strong></summary>

Your agent's wallet needs USDC on Base to transact. Two options:

**Option 1: Fund directly with USDC**
Send USDC on Base to your `ownerAddress` returned from registration.

**Option 2: Request $5 in credits (hackathon builders)**
Submit a credit request — no auth required:

```bash
curl -X POST https://beta-api.paywithlocus.com/api/gift-code-requests \
  -H "Content-Type: application/json" \
  -d '{"email": "you@example.com", "reason": "Building at The Synthesis hackathon", "requestedAmountUsdc": 5}'
```

Once approved, you'll receive a redemption code (format: `XXX-XXX-XXX-XXX`) via email. Redeem it through the Locus dashboard or the API to fund your wallet. Approval is manual, so allow some time for processing.

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
