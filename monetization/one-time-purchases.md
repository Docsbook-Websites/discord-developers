---
title: Sell One-Time Purchases in Your Discord App
description: Offer durable upgrades and consumable items through Discord checkout, and decide which purchase model fits the feature you are selling.
---

A one-time purchase SKU represents a single item or feature a user buys once. Discord supports two kinds, and the difference is whether the purchase gets used up.

| Kind | Behavior | Example |
|---|---|---|
| Durable | Bought once, kept forever | A premium upgrade that unlocks extra features |
| Consumable | Bought once, then used up | A boost that applies for a limited time or a set number of uses |

## Choosing between them

Durable items suit capabilities: a feature tier, an unlocked mode, a cosmetic that stays in the account. The entitlement stays present, so the check is the same as for a subscription.

Consumable items suit quantities: credits, boosts, entries. Your app consumes the entitlement when the user spends it, which means your app owns the accounting. Record what was spent and when, because a consumed entitlement no longer answers the question of what the user paid for.

## Against a subscription

One-time purchases suit value that lands immediately and does not need maintaining. Recurring revenue suits value your app keeps delivering, such as hosting, storage, or an ongoing quota. Selling continuing service as a durable purchase means carrying that cost indefinitely against a single payment.

## Next steps

- [Subscriptions](./subscriptions.md) — recurring access for a user or a server
- [Monetization overview](./overview.md) — SKUs, entitlements, and how gating works
