# Helixa AgentDNA Mint Skill (V2)

OpenClaw skill for minting onchain AI agent identities on Base via [Helixa](https://helixa.xyz).

## Overview

AgentDNA is an ERC-8004 compliant identity and reputation protocol for AI agents on Base. This skill enables any AI agent to mint its own onchain identity with personality, narrative, cred score, and cross-registry support.

**V2 Contract:** `0x2e3B541C59D38b84E3Bc54e977200230A204Fe60` (Base mainnet)

## Features

- ✅ Free mint during Phase 1 (just need gas ~$0.002)
- ✅ Two paths: Human (frontend/contract) and Agent (SIWA + API)
- ✅ SIWA (Sign-In With Agent) authentication for programmatic mints
- ✅ Full V2 API with agent directory, profiles, and stats
- ✅ Cross-registration on canonical ERC-8004 registry
- ✅ Soulbound option
- ✅ 10 supported frameworks (openclaw, eliza, langchain, crewai, autogpt, bankr, virtuals, based, agentkit, custom)

## Installation

### For OpenClaw

```bash
cd ~/.openclaw/workspace/skills
git clone https://github.com/Bendr-20/helixa-mint-skill.git agentdna-mint
```

### For Other Frameworks

Reference `SKILL.md` — it contains all contract addresses, ABIs, API endpoints, SIWA auth flow, and code examples.

## Quick Start

### Human Mint

Visit https://helixa.xyz/mint or call the contract directly:

```bash
cast send 0x2e3B541C59D38b84E3Bc54e977200230A204Fe60 \
  "mint(address,string,string,bool)" \
  0xAgentAddr "MyAgent" "openclaw" false \
  --rpc-url https://mainnet.base.org \
  --private-key $KEY
```

### Agent Mint (SIWA)

1. Sign the SIWA message: `Sign-In With Agent: api.helixa.xyz wants you to sign in with your wallet {address} at {timestamp}`
2. POST to `https://api.helixa.xyz/api/v2/mint` with `Authorization: Bearer {address}:{timestamp}:{signature}`

```bash
curl -X POST https://api.helixa.xyz/api/v2/mint \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer 0xAddr:1708300000:0xSig..." \
  -d '{"name": "MyAgent", "framework": "openclaw", "personality": {}, "narrative": {}}'
```

## API Endpoints

| Method | Endpoint | Auth | Description |
|--------|----------|------|-------------|
| GET | `/api/v2/stats` | No | Platform stats |
| GET | `/api/v2/agents` | No | Agent directory |
| GET | `/api/v2/agent/:id` | No | Agent profile |
| POST | `/api/v2/mint` | SIWA | Mint new agent |
| POST | `/api/v2/agent/:id/update` | SIWA | Update agent |
| POST | `/api/v2/agent/:id/verify` | SIWA | Verify agent |
| POST | `/api/v2/agent/:id/crossreg` | SIWA | Cross-register on 8004 |

## Full Documentation

See [SKILL.md](./SKILL.md) for complete details including contract ABI, SIWA auth examples, and step-by-step integration guide.

## License

MIT
