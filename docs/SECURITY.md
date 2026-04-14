# Security

RetroChat takes platform security seriously. Here's how we protect our users and their data.

---

## Authentication

- **Email-based authentication** — Secure sign-up and login powered by Supabase Auth.
- **Password security** — Passwords are hashed and never stored in plain text.
- **Password reset** — Secure email-based password recovery flow.
- **Session management** — Sessions are securely managed with automatic token refresh.

---

## Age Verification

- All users must provide their date of birth during sign-up.
- Users under **13 years old** are not permitted to create accounts.
- Certain features (Web3 wallet integration, token creation, tipping) require users to be **18 or older**.
- Age verification events are logged for compliance purposes.

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

- RetroChat **never** has access to your wallet's private keys.
- Wallet connections use standard Solana wallet adapter protocols.
- All transactions require explicit approval in your wallet app.
- RetroChat does not custody, hold, or manage user funds.

---

## Infrastructure

- Hosted on secure, modern cloud infrastructure.
- HTTPS encryption for all connections.
- Service worker (PWA) configured to avoid caching sensitive authentication data.

---

## Reporting Security Issues

If you discover a security vulnerability, please report it responsibly:

1. Use the **Bug Report** feature within the app.
2. Provide as much detail as possible about the issue.
3. Do not publicly disclose the vulnerability before it has been addressed.

We take all security reports seriously and will respond promptly.

---

*Your security is our priority.*
