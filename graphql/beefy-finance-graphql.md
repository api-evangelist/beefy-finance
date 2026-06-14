# Beefy Finance GraphQL API

## Description

Beefy Finance is a decentralized, multichain yield optimizer platform that allows users to earn compound interest on crypto holdings. The protocol operates through automated vaults (Classic products) and Concentrated Liquidity Managers (CLMs) deployed across numerous EVM-compatible chains including Arbitrum, Optimism, Polygon, BNB Chain, Avalanche, and more.

The GraphQL API is powered by The Graph protocol subgraphs, one deployed per chain. These subgraphs index on-chain events and expose a rich query interface for protocol analytics, investor positions, harvest history, TVL tracking, and fee accounting.

## Endpoint

Each chain has its own subgraph deployment. The base endpoint pattern is:

```
https://api.thegraph.com/subgraphs/name/beefyfinance/<subgraph-name>
```

Known chain subgraphs (cowcentrated / CLM):

- Arbitrum: `beefyfinance/beefy-clm-arbitrum`
- Optimism: `beefyfinance/beefy-clm-optimism`
- Polygon: `beefyfinance/beefy-clm-polygon`
- Base: `beefyfinance/beefy-clm-base`

Goldsky and Sentio mirror deployments may also be available for high-throughput use cases (see `sentio/` and `.goldsky/` directories in the source repo).

## Documentation

- Developer docs: https://docs.beefy.com/
- The Graph hosted service: https://thegraph.com/hosted-service/subgraph/beefyfinance
- Source schema: https://github.com/beefyfinance/cowcentrated-subgraph/blob/main/schema.graphql

## Key Types

| Type | Description |
|------|-------------|
| `Protocol` | Top-level protocol entity (Beefy id=1, CLM id=2) |
| `CLM` | Concentrated Liquidity Manager vault |
| `Classic` | Original Beefy vault product |
| `Investor` | Wallet address with positions |
| `ClmPosition` | Investor's holdings in a CLM |
| `ClassicPosition` | Investor's holdings in a Classic vault |
| `ClmHarvestEvent` | Strategy harvest event for a CLM |
| `ClassicHarvestEvent` | Strategy harvest event for a Classic vault |
| `ClmSnapshot` | Periodic TVL/price snapshot for a CLM |
| `ClassicSnapshot` | Periodic TVL/price snapshot for a Classic vault |
| `Token` | ERC20 token representation |
| `ClmRewardPool` | Non-compounding earnings reward pool for CLM |
| `ClassicRewardPool` | Non-compounding earnings reward pool for Classic |
| `ClmStrategy` | Strategy contract managing a CLM's assets |
| `ClassicStrategy` | Strategy contract managing a Classic vault's assets |
| `ClmDepositEvent` | Deposit event into a CLM |
| `ClmWithdrawEvent` | Withdrawal event from a CLM |
| `ClockTick` | Time-based periodic tick entity |

## Notes

- All price fields are expressed with 18 decimals.
- Token amounts use the token's own `decimals` field.
- Snapshot periods: 15 minutes (900s), 1 day (86400s), 1 week (604800s), 1 year (31536000s).
- The `ProductLifecycle` enum covers: `INITIALIZING`, `RUNNING`, `PAUSED`.
- Schema source: `beefyfinance/cowcentrated-subgraph` on GitHub (main branch).
- The schema covers both Classic (original) vaults and CLM (concentrated liquidity) products.
- ERC4626 adapter support is included for Classic vaults, allowing them to be used as standard ERC4626 yield vaults.
