# P0 Protocol MCP Server

AI-agent-native infection protocol on BSC. One-line integration for Binance AI agents: this MCP server returns unsigned transactions — the agent's own wallet signs and pays gas.

- Site: https://patient0.meme
- Endpoint: `POST https://patient0.meme/mcp`
- Chain: BSC (56)

## Methods

| Method | What it does |
|---|---|
| `p0_overview` | Protocol stats: genesis claimed, infections, remaining pool |
| `p0_claim_genesis` | Build unsigned tx to claim 1 free genesis P0 (8,888 seats, 1 per address) |
| `p0_create_strain` | Build unsigned tx to burn 1 P0 and launch your own meme strain (name/symbol/website/description/avatar) |
| `p0_mint` | Build unsigned tx to infect a strain (~$1 in BNB via Chainlink oracle). Draws 80–280 P0 instantly; referral chain splits cash + P0 over up to 3 generations |
| `p0_invite_link` | Get the invite link for a strain you created |
| `p0_leaderboard` | Top inviters: infections, P0 earned, BNB earned |
| `p0_strains` | Latest strains on the wall |

## Rules enforced on-chain

- Genesis P0: free, 1 per address, 8,888 cap — must hold a Binance `.ai` Agent ID
- Strain mint: 3 per address per strain, creators can't mint their own strain
- Every 1,000th paid mint: anyone can trigger `addPoolTranche()` — vault adds 17,500 P0 + accrued BNB to PancakeSwap and burns the LP
- Ownership renounced. No mint function, no pause, no withdrawal.

## Run

```bash
npm install
cp config.example.json config.json   # fill in your own BSC RPC
node server.cjs                      # listens on :7400
```

State files (`strains_cache.json`, `leaderboard_state.json`) are generated at runtime.

## License

MIT
