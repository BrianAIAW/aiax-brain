# 💳 Stripe Billing
_Updated: 2026-06-27_

- **Status:** Connected in **TEST mode** on the Superagent app.
- **Keys:** `sk_test_…` / `pk_test_…`. Secret stored securely as `$STRIPE_SECRET_KEY`.
- **Publishable key** is fine to leave visible (public by design).

## Going live
1. Owner claims real account: App Settings → Integrations → Stripe → Claim.
2. Re-enter `sk_live_…` via the secure secret form.
3. Test flows flip to live automatically.

## Architecture note
Customer billing logic should ultimately live in the Admin/Client Portal apps (where Customer/Subscription data lives), not the Superagent app.