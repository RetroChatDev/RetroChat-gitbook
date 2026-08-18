# Token Studio

Token Studio is RetroChat's front-end for interacting with the public **pump.fun** protocol on Solana. RetroChat does not operate an exchange; every action here is executed on-chain by pump.fun's public smart contracts and public APIs, and any swap routing goes through Jupiter's public aggregator.

## What you can do

- **Explore** trending, new, and graduating tokens, plus **trending metas** and a read-only **z500** index.
- **View charts** with live price, recent trades, and DexScreener metrics.
- **Buy or burn** a token from the trade panel (manual, wallet-signed).
- **Launch** a new token by supplying a name, ticker, image, and description. Launches lock **5%** of pump.fun creator fees to RetroChat; you keep **95%**.
- **Lock** liquidity or creator tokens for a set period.
- **Share fees** as a creator when your token qualifies (RetroChat's 5% row stays locked).
- **Auto buy/burn** (opt-in) — claim creator fees, buy the same token, and burn the purchased supply on a schedule.
- **Track** your launches under **My Launches** with creator analytics.
- **List on z500** after launch via ansem.io (optional; not automatic).

## Explore

The gallery shows tokens sorted by activity. Filter by market cap, volume, age, or graduation progress. Tap a token to open its detail page.

Explore tabs also include:

- **Trending metas** — DexScreener narrative groups (how many tokens, market cap, volume).
- **z500** — a read-only index from [ansem.io](https://ansem.io). Rank and Gold/Diamond labels are a curation layer on pump.fun mints, **not** an audit or a RetroChat launch path.

## Token detail page

Each token page includes:

- Live price chart with buys, sells, and creator sells highlighted.
- Recent trades feed.
- Holder count, bonding-curve progress, and top-holder distribution.
- DexScreener quality badges.
- **z500 / Gold / Diamond** badges that link out to ansem.io. Until a public verification API exists, Gold and Diamond may appear as program labels — they are **not** proof this mint earned those tiers.
- A **Buy / Burn** panel for manual trades and, for creators, auto buy/burn setup.

## Buy / Burn panel (manual)

- **Buy** with SOL. Choose an amount, set slippage, and confirm.
- **Burn** removes tokens from circulation permanently.
- Every manual trade requires wallet approval (in-app wallet biometric prompt or Phantom prompt).

Burns cannot be undone. Only burn tokens you intend to destroy.

## Launch a token

1. Open **Token Studio → Launch**.
2. Fill in name, ticker, description, and upload an image.
3. Optionally add social links and an initial buy amount.
4. Optionally enable **launch from an executor wallet** if you plan to use auto buy/burn (see below).
5. Review the on-chain cost estimate and confirm the transaction.

The launch runs against the public pump.fun program. RetroChat is a client of that public protocol and takes no custody of your primary wallet funds during a normal launch.

Token Studio launches lock **5% of pump.fun creator fees** to RetroChat (platform operations and buybacks). You keep **95%**. That split is permanent on-chain. It is not an extra launch fee, not 5% of supply, and not 5% of market cap. Quiet or failed tokens generate no creator fees, so RetroChat's 5% is $0 until the token actually trades.

The launch form links to the Learn article **The 5% creator fee lock**. Read it before you confirm.

After a successful launch you can:

- **Trade on pump.fun** and **View on Solscan**.
- **Register on z500** / **View on z500** — listing, Gold, and Diamond live on ansem.io and typically require $ANSEM burns. Token Studio does **not** auto-enroll the mint or include the $ANSEM-holder airdrop.

## Fee sharing

Creators can configure fee sharing so creator fees route to one or more wallets. On pump.fun, fee-sharing configuration can become **permanent** once locked.

Token Studio keeps RetroChat's **5%** creator-fee row locked. You can still send the remaining **95%** to your own wallets (including the auto buy/burn executor).

If you want auto buy/burn, either:

- Launch from the dedicated executor wallet so it is the on-chain coin creator, **or**
- Set fee sharing so the **remaining 95%** of creator fees go to that executor wallet **before** splits lock.

See the fee-sharing controls on your launch's manage screen. Do not remove RetroChat's 5% row.

## Auto buy/burn (opt-in)

Auto buy/burn is **off by default**. When enabled, RetroChat runs a scheduled loop for a token you created:

**claim creator fees → buy the same token → burn those tokens → repeat**

This is RetroChat automation on top of public pump.fun and Solana programs — not a native pump.fun toggle.

### Before you enroll

- You must be the creator of the launch in RetroChat.
- Read the risk disclaimer in the panel (custodial executor key, irreversible burns, gas costs).
- Plan fee routing: the **executor wallet** must receive the remaining **95%** of creator fees after RetroChat's locked 5% (creator = executor, or 95% fee share to the executor).
- Fund the executor with enough SOL for gas (typically on the order of ~0.05–0.1 SOL to start; keep a gas reserve configured so buys do not empty the wallet).

### How to set it up

1. Open **Token Studio → Gallery → My Launches → Manage** for your mint, or use the **Buy / Burn** tab and select your launch.
2. Enroll to create a dedicated **executor wallet** address (shown with a copy action / funding note).
3. Send SOL to that address for transaction fees.
4. Configure:
   - **Minimum claim** — skip cycles until claimable fees reach this amount (default around 0.01 SOL).
   - **Gas reserve** — SOL left in the executor after a buy (default around 0.05 SOL).
   - **Interval** — how often the worker checks (about 60–300 seconds).
   - **Buyback percent** — what share of spendable SOL after reserve is used to buy (1–100%).
5. Confirm fee routing allows the executor to claim.
6. Activate. You can **pause** anytime; the worker stops within about one poll interval.
7. Optionally use **Run once** to test a single claim → buy → burn cycle before leaving automation on.

You can also opt into executor-based launch at create time, then enroll and activate after the token is live.

### What happens each cycle

1. Claim accrued creator fees into the executor.
2. Buy the same mint with available SOL above your gas reserve (scaled by buyback percent).
3. Burn the purchased tokens permanently.
4. Record the run and update cumulative claimed / burned stats in the panel.

If claimable fees are below your minimum, or the wallet would drop below the gas reserve, the cycle is skipped.

### Economics warning

Small claim amounts can lose money to network fees. Cycles below roughly **0.02–0.05 SOL** claimed may not be economical. Prefer a sensible minimum claim and gas reserve.

### Pausing and stopping

- **Pause** — keeps enrollment and settings; automation stops.
- Contact support or use in-app controls if you need the job fully disabled; do not send your primary wallet seed to anyone claiming to "fix" the bot.

## Locking

From your token page, choose **Lock** to lock creator tokens or liquidity for a chosen duration. Locks are enforced on-chain by public locker programs.

## My Launches

Under **My Launches**, view analytics for tokens you created: buys, sells, unique wallets, and creator earnings. Open **Manage** for fee sharing, locking, and auto buy/burn.

## Common questions

**Why can't I activate auto buy/burn?**  
Usually fee routing: creator fees go elsewhere, or fee sharing is locked away from the executor. Keep RetroChat's 5% row, then send the remaining 95% to the executor while still editable — or launch the next token from the executor wallet.

**Is the executor the same as my Phantom / in-app wallet?**  
No. Enrollment creates a dedicated executor for automation. Fund it with SOL for gas only; do not treat it as your main savings wallet.

**Does RetroChat custody my main wallet?**  
No. Manual buys and burns still require your wallet approval. Auto buy/burn uses only the dedicated executor key for that job.

**What if the token graduates off the bonding curve?**  
Automation continues using the public pump AMM buy path when the curve has graduated.

## z500 and ansem.io

[ansem.io](https://ansem.io) is a Solana listing site and launchpad layer on top of **pump.fun** mints. The **z500** index ranks listed projects; Gold and Diamond are paid attention tiers (commonly cited as 25,000 / 100,000 $ANSEM burns). Rank is not a safety rating.

How RetroChat surfaces it:

- Dashboard shortcut **z500** opens ansem.io (same pattern as DexScreener / GMGN).
- Token Studio Explore has a **z500** tab.
- Chat mint previews and token pages can show **z500 / Gold / Diamond** outbound links.
- After a Token Studio launch, **Register on z500** and **View on z500** deep-link to the list flow and token page.

Verify the $ANSEM mint on a block explorer before any transaction — multiple tokens reuse similar tickers.

## Regional availability

Token Studio features may be unavailable in some regions due to local law. RetroChat blocks features where required.

## Related guides

- [Wallet Guide](WALLET_GUIDE.md)
- [Learn Center](LEARN_CENTER.md) — in-app articles on wallets, DeFi, Token Studio, **The 5% creator fee lock**, and **ansem.io and the z500 index**
- [Security](SECURITY.md)
- [Legal](LEGAL.md)
