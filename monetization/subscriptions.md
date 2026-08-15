---
title: Implement Discord App Subscriptions
description: Offer recurring premium access in your Discord app with user and guild subscription SKUs, and check entitlements before unlocking a paid feature.
---

A subscription SKU represents a recurring purchase for a set period. Discord runs the checkout and the recurring billing; your app decides what an entitled user can do.

## User and guild subscriptions

| Type | Who pays | Who becomes entitled |
|---|---|---|
| User subscription | One person | Only the purchasing user |
| Guild subscription | One person, for their server | Every member of that server |

The choice follows the value. A personal utility, a saved profile, or an AI quota belongs to a user subscription. Moderation tooling, server analytics, or anything an admin buys on behalf of a community belongs to a guild subscription, because every member benefits without buying separately.

## The flow

<!-- widget:stepper -->

### Create the SKU

Create a subscription SKU for your application. Each SKU is a distinct offering, so a monthly and an annual plan are separate SKUs.

### Check entitlements when the feature is used

Interactions carry the entitlements that apply to the invoking user and server. Read them at the point of use rather than caching a verdict, so cancellations and expiries take effect.

### Branch on the result

An entitled user gets the feature. Everyone else gets a message explaining what the upgrade unlocks, with a premium button to buy.

### Handle the lifecycle

Subscriptions renew, lapse, and get canceled. Treat entitlement as the current state rather than a one-time grant, and design the downgrade path so a lapsed subscriber keeps their data and loses only the premium behavior.

<!-- /widget -->

## Test before you launch

Grant yourself a test entitlement and exercise both paths: the entitled path and the unentitled prompt. The unentitled path is what most users see first, and it is the one that stays untested when you only ever run the app on an account that owns everything.

## Next steps

- [One-time purchases](./one-time-purchases.md) — durable and consumable alternatives
- [Monetization overview](./overview.md) — SKUs, entitlements, and subscriptions
- [Receiving and responding](../interactions/receiving-and-responding.md) — respond to the interaction that carries entitlements
