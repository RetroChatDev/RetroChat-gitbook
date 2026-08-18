# Security

RetroChat takes platform security seriously. Here's how we protect our users and their data.

---

## Authentication

- **Email-based authentication** — Secure sign-up and login powered by Supabase Auth.
- **Apple and Google OAuth** — Continue with Apple or Google; the native apps complete the provider login in the system browser.
- **Password security** — Passwords are hashed and never stored in plain text.
- **Password reset** — Secure email-based password recovery flow.
- **Session management** — Sessions are securely managed with automatic token refresh.
- **Wallet sign-in** — Phantom or in-app wallet sign a free off-chain message; no funds move during login.
- **X (Twitter) OAuth** — Optional social sign-in and handle linking.

---

## Age Verification

- Users confirm they are at least **16** during sign-in / onboarding (attestation). RetroChat does **not** collect a date of birth for this check.
- Creating an **in-app wallet** requires confirming you are at least **18**.
- Age attestation events may be logged for compliance purposes.

---

## Content Moderation

RetroChat provides multiple layers of content moderation:

- **Room-level moderation** — Room creators can manage messages and users within their rooms.
- **Community moderation** — Community owners and moderators can manage posts, members, and reports.
- **Platform-wide moderation** — Administrators can take action across all rooms and communities.
- **User reporting** — Users can report inappropriate posts and messages.
- **Muting** — Rooms and users can be muted by moderators or administrators.
- **Banning** — Users can be banned from specific rooms or the entire platform.

---

## Rate Limiting

- Message sending is rate-limited to prevent spam and abuse.
- API requests are throttled to protect platform stability.
- Visual indicators inform users when they are approaching rate limits.

---

## Data Protection

- **Row-Level Security (RLS)** — Database access is controlled at the row level, ensuring users can only access data they are authorized to see.
- **Secure file uploads** — File attachments are validated for type and size before upload.
- **Input sanitization** — User inputs are sanitized to prevent injection attacks.
- **CSRF protection** — Cross-site request forgery protections are in place.

---

## Wallet Security

- RetroChat **never** has access to your Phantom or in-app wallet private keys or recovery phrases on our servers.
- Phantom connections use standard Solana wallet adapter protocols.
- In-app wallets keep key material on-device and require biometric or passphrase approval for signing.
- Manual trades and transfers require explicit wallet approval.
- Your primary wallet funds remain under your control; RetroChat does not custody them.

### Wallet Relay

Optional [Wallet Relay](WALLET_GUIDE.md) pairs a Chromium extension with your RetroChat signer. Pairing does not authorize a transaction. You review each dApp origin and action. Encrypted request envelopes may transit RetroChat infrastructure; private keys never do. Install only the official [Chrome Web Store listing](https://chromewebstore.google.com/detail/lcikpcjmmijbpmpadpdjfncpijldpacc) and revoke pairings from **Browser Wallet Access** if a device is lost.

### Opt-in auto buy/burn executor

If you enable [Token Studio auto buy/burn](TOKEN_STUDIO.md), RetroChat creates a **dedicated executor wallet** for that job only. That executor key is held so the scheduled claim → buy → burn loop can run without you signing each cycle. Enrollment requires an explicit risk disclaimer. Pause anytime. Do not send more SOL to the executor than you are willing to use for gas and buybacks.

---

## Infrastructure

- Hosted on secure, modern cloud infrastructure.
- HTTPS encryption for all connections.
- Service worker (PWA) configured to avoid caching sensitive authentication data.

---

## Reporting Security Issues

If you discover a security vulnerability, please report it responsibly:

1. Email **support@retrochat.io** with as much detail as possible, or use the in-app **Bug Report** feature for product defects.
2. Do not publicly disclose the vulnerability before it has been addressed.

We take all security reports seriously and will respond promptly.

---

*Your security is our priority.*
