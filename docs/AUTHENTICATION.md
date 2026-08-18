# Authentication

RetroChat offers several ways to sign in. You can link more than one to the same account after your first sign-in.

## Email and password

1. Open RetroChat and choose **Sign up**.
2. Enter an email and a password.
3. Confirm that you are at least **16** years old (age attestation — RetroChat does not collect a date of birth).
4. Verify your email if prompted.
5. Set a screen name and avatar to finish onboarding.

Use **Forgot password** on the sign-in screen to reset your password by email.

## Apple and Google

On the sign-in and sign-up screens, choose **Continue with Apple** or **Continue with Google**. RetroChat uses the same OAuth flow on web, PWA, and the native apps (the native apps open the system browser to complete the provider login).

After you approve access, RetroChat creates or links your account. Age attestation still applies on first use.

## Wallet sign-in (Solana)

Choose **Continue with Wallet** to sign in with an existing wallet:

- **Phantom** (recommended). RetroChat detects Phantom on desktop, mobile, and inside the Phantom in-app browser.
- **In-app wallet**. If you don't have Phantom, RetroChat can create a wallet for you during onboarding. Creating an in-app wallet requires confirming you are at least **18**. Back up the recovery phrase before continuing.

You'll be asked to sign a short "Sign in to RetroChat" message. This message is free, off-chain, and never moves funds.

## X (Twitter) sign-in

Choose **Continue with X** to authorize RetroChat through X's OAuth screen. Your handle, display name, and avatar are imported. You can also link X later from your profile settings to unlock the verified-handle badge.

## Cross-device wallet approval

If you're on a desktop and your wallet lives on your phone, use **Pair device** on the wallet screen. Scan the code with the RetroChat mobile app to approve wallet requests from the phone. The pairing expires when you sign out.

## Deleting your account

Open **Edit Profile → Danger Zone → Delete Account**, type the confirmation phrase, and confirm. Your profile, posts, and messages are removed and you're signed out. On-chain assets in an external wallet remain in that wallet.

## Related guides

- [Getting Started](GETTING_STARTED.md)
- [Install RetroChat](INSTALL.md)
- [Wallet Guide](WALLET_GUIDE.md)
- [Security](SECURITY.md)
