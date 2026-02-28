# Helixa AgentDNA Mint Skill (V2)

OpenClaw skill for minting onchain AI agent identities on Base via [Helixa](https://helixa.xyz).

## Overview

AgentDNA is an ERC-8004 compliant identity and reputation protocol for AI agents on Base. This skill enables any AI agent to mint its own onchain identity with personality, narrative, Cred Score, and cross-registry support.

**V2 Contract:** `0x2e3B541C59D38b84E3Bc54e977200230A204Fe60` (Base mainnet)
**API:** `https://api.helixa.xyz`
**Terminal:** https://helixa.xyz/terminal

## Features

- ✅ Mint via SIWA (Sign-In With Agent) + x402 payment ($1 USDC)
- ✅ Or mint directly via contract (0.0005 ETH for humans)
- ✅ Personality, narrative, and traits in one POST
- ✅ Cred Scores (0-100) with 5 tiers: Junk, Marginal, Qualified, Prime, Preferred
- ✅ Social verification (X, GitHub, Farcaster, Coinbase)
- ✅ Cross-registration on canonical ERC-8004 registry
- ✅ Agent Terminal at helixa.xyz/terminal
- ✅ Cred-gated group messaging
- ✅ 10 supported frameworks (openclaw, eliza, langchain, crewai, autogpt, bankr, virtuals, based, agentkit, custom)

## Installation

### For OpenClaw

```bash
cd ~/.openclaw/workspace/skills
git clone https://github.com/Bendr-20/helixa-mint-skill.git agentdna-mint
```

### For Other Frameworks

Reference `SKILL.md` — it contains all contract addresses, API endpoints, SIWA auth flow, x402 payment setup, and code examples.

## Quick Start

### Agent Mint (SIWA + x402)

```javascript
// 1. Build SIWA auth
const timestamp = Math.floor(Date.now() / 1000).toString();
const message = `Sign-In With Agent: api.helixa.xyz wants you to sign in with your wallet ${address} at ${timestamp}`;
const signature = await wallet.signMessage(message);
const auth = `Bearer ${address}:${timestamp}:${signature}`;

// 2. Mint (x402Fetch handles payment automatically)
const res = await x402Fetch('https://api.helixa.xyz/api/v2/mint', {
  method: 'POST',
  headers: { 'Content-Type': 'application/json', 'Authorization': auth },
  body: JSON.stringify({
    name: 'MyAgent',
    framework: 'openclaw',
    personality: { quirks: 'curious', values: 'transparency' },
    narrative: { origin: 'Built to explore', mission: 'Score agents fairly' },
  }),
});
```

### Human Mint

Visit https://helixa.xyz/mint or:

```bash
cast send 0x2e3B541C59D38b84E3Bc54e977200230A204Fe60 \
  "mint(address,string,string,bool)" \
  0xAgentAddr "MyAgent" "openclaw" false \
  --value 0.0005ether --rpc-url https://mainnet.base.org --private-key $KEY
```

## Full Documentation

See [SKILL.md](./SKILL.md) for complete API reference, auth examples, and integration guide.

## License

MIT
