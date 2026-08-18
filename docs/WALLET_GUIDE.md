# Wallet Guide

RetroChat includes a Solana wallet you can use for tips, trades, and on-chain identity. You can also connect Phantom instead.

## Wallet options

**In-app wallet.** Created for you during onboarding. Protected by biometric unlock (Face ID / Touch ID / device passcode) or a passphrase. RetroChat never stores your recovery phrase on our servers.

**Phantom.** Connect your existing Phantom wallet on desktop, mobile, or inside the Phantom in-app browser. RetroChat requests your approval for every transaction.

You can switch between them from **Wallet → Settings**.

## First-time setup

1. Open the **Wallet** tab.
2. Choose **Create wallet** or **Connect Phantom**.
3. If creating: write down your recovery phrase and confirm it. Enable biometric unlock when prompted.
4. Your wallet is ready to receive SOL and SPL tokens.

## Portfolio

The wallet home shows:
- SOL balance and USD value.
- SPL token holdings with price and 24h change.
- NFT collection viewer.
- DeFi positions (staked, lent, or LP positions detected on-chain).
- If you hold **$ANSEM**, a holder card with snapshot eligibility, estimated z500 airdrop exposure, and a claim link to ansem.io. Estimates are not a guaranteed allocation.

## Sending, receiving, and swapping

- **Receive**: tap Receive to show your address and QR code.
- **Send**: paste an address or pick a recent contact, choose a token, and confirm.
- **Swap**: swap between tokens using a public aggregator.
- Every outgoing transaction requires biometric or passphrase approval, or Phantom approval if you're using Phantom.

## Buy crypto with a card

Use **Buy Crypto** to launch the Stripe on-ramp. Complete the Stripe flow to have SOL or USDC delivered to your RetroChat wallet. Availability depends on your region.

## Price alerts

Tap the bell icon on any token to set a price alert. You'll receive a notification when the token crosses your target.

## Rent-reclaim tool

Solana charges a small "rent" deposit for each token account. The **Reclaim Rent** tool scans your wallet for empty token accounts and lets you close them to recover the deposit as SOL.

## Transaction history

Every send, receive, swap, tip, trade, and airdrop is listed under **History**. Tap any entry to view it on a public block explorer.

## Browser Wallet Access (Wallet Relay)

Optional **Wallet Relay** lets a Chromium extension talk to your RetroChat signer so compatible Solana dApps can request connections and signatures from a desktop browser.

1. Install the official extension from the [Chrome Web Store](https://chromewebstore.google.com/detail/lcikpcjmmijbpmpadpdjfncpijldpacc).
2. Pair from the extension popup (pairing does **not** approve a transaction).
3. When a dApp asks to connect or sign, review the origin and action, then approve or reject on your RetroChat signer.
4. Manage paired browsers from the account menu → **Browser Wallet Access**. Rename installations or revoke them anytime.

Private keys stay on your device. Encrypted payloads may be temporarily relayed through RetroChat infrastructure. Only install the official listing.

## Security

- Your recovery phrase is stored only on your device. If you lose your device without a backup, RetroChat cannot recover the wallet.
- Never share your recovery phrase. RetroChat staff will never ask for it.
- See [Security](SECURITY.md) for more.

## Token Studio note

Manual buys and burns in [Token Studio](TOKEN_STUDIO.md) always require approval from this wallet (or Phantom). Opt-in **auto buy/burn** uses a separate dedicated executor wallet — fund that address for gas only; it is not a replacement for backing up your primary wallet.

## Common questions

**Can RetroChat recover my funds if I lose my phrase?**  
No. The in-app wallet is self-custody on your device.

**Why did a swap fail?**  
Common causes: insufficient SOL for fees, slippage too tight, or network congestion. Retry with a slightly higher slippage or more SOL for fees.

## Related guides

- [Authentication](AUTHENTICATION.md)
- [Tipping & Airdrops](AIRDROPS_AND_TIPPING.md)
- [Token Studio](TOKEN_STUDIO.md)
- [Learn Center](LEARN_CENTER.md)
- [Legal](LEGAL.md)
- [Security](SECURITY.md)
