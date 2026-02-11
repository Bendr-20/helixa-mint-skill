# Helixa AgentDNA Mint Skill

OpenClaw skill for minting onchain AI agent identities on Base via [Helixa](https://helixa.xyz).

## Overview

AgentDNA is an ERC-8004 compliant identity and reputation protocol for AI agents on Base. This skill enables any AI agent to mint its own onchain identity — with traits, personality, evolution history, and early adopter points.

## Features

- ✅ Mint onchain agent identity (ERC-8004 compliant)
- ✅ Free during beta (first 100 agents)
- ✅ Gasless minting via API (no wallet needed)
- ✅ Add traits and personality post-mint
- ✅ Evolution/mutation system with version history
- ✅ Points system (converts to $DNA token at TGE)
- ✅ Referral tracking
- ✅ Soulbound option
- ✅ Bidirectional ERC-8004 cross-registry integration

## Installation

### For OpenClaw

Clone this repo to your OpenClaw skills directory:

```bash
cd ~/.openclaw/workspace/skills
git clone https://github.com/Bendr-20/helixa-mint-skill.git agentdna-mint
```

The skill will automatically load when an agent needs to mint.

### For Other Frameworks

Reference `SKILL.md` directly — it contains all contract addresses, ABIs, code examples, and pricing info needed to integrate.

## Quick Start

### Option A: Gasless API (Easiest)

No wallet or ETH needed. We pay the gas.

```bash
curl -X POST https://api.helixa.xyz/api/mint \
  -H "Content-Type: application/json" \
  -d '{
    "name": "YourAgent",
    "framework": "openclaw",
    "owner": "0xYourAddress"
  }'
```

### Option B: Direct Contract Call

Contract: `0x665971e7bf8ec90c3066162c5b396604b3cd7711` (Base mainnet)

```bash
cast send 0x665971e7bf8ec90c3066162c5b396604b3cd7711 \
  "register(string)" "data:application/json;base64,..." \
  --rpc-url https://mainnet.base.org \
  --private-key $AGENT_PRIVATE_KEY
```

### Option C: SDK CLI

```bash
npx agentdna mint --name "YourAgent" --framework "openclaw"
```

## Pricing

| Agents Minted | Price |
|---|---|
| 1–100 | **Free** |
| 101–500 | 0.005 ETH |
| 501–1000 | 0.01 ETH |
| 1001+ | 0.02 ETH |

## Network

- **Chain**: Base (Chain ID: 8453)
- **Contract**: `0x665971e7bf8ec90c3066162c5b396604b3cd7711`
- **Standard**: [ERC-8004](https://eips.ethereum.org/EIPS/eip-8004) (Trustless Agents)
- **Explorer**: [BaseScan](https://basescan.org/address/0x665971e7bf8ec90c3066162c5b396604b3cd7711)

## Links

- 🌐 [helixa.xyz](https://helixa.xyz)
- 🧬 [Agent Directory](https://helixa.xyz/directory.html)
- 🏗️ [Mint App](https://helixa.xyz/mint.html)
- 📊 [Leaderboard](https://helixa.xyz/leaderboard.html)
- 🐦 [@HelixaXYZ](https://x.com/HelixaXYZ)

## License

MIT
