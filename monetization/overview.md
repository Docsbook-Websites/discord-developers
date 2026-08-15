---
title: Monetize Your Discord App With Premium Features
description: Sell subscriptions and one-time purchases inside your Discord app using SKUs, entitlements, and Discord's built-in checkout and payment flow.
---

Add subscriptions and one-time purchases to your app using Discord's built-in checkout and payment flow. Monetization applies to bots and Activities.

![Premium app monetization inside Discord](https://raw.githubusercontent.com/discord/discord-api-docs/main/images/monetization/overview.png)

## The three pieces

| Concept | What it represents |
|---|---|
| SKU | A specific item or subscription option your app offers |
| Entitlement | Whether a user has access to a given SKU |
| Subscription | An ongoing agreement to pay for an entitlement until canceled |

Your app never handles payment details. It creates SKUs, and then checks entitlements to decide what a given user may do.

## Two kinds of SKU

<!-- widget:cards -->

- [Subscriptions](./subscriptions.md) — Recurring access for a user or for a whole server {repeat}
- [One-time purchases](./one-time-purchases.md) — Durable upgrades and consumable items {shopping-cart}

<!-- /widget -->

## Gating a feature

The pattern is the same in both cases: read the entitlements attached to the interaction, and branch.

1. A user invokes a premium command or opens a premium part of your Activity
2. Your app checks whether an entitlement for the relevant SKU is present
3. Entitled users get the feature; everyone else gets a prompt to buy

Callback type `PREMIUM_REQUIRED` (`10`) is deprecated. Use the current premium button style rather than that callback type.

## Next steps

- [Subscriptions](./subscriptions.md) — user and guild subscriptions
- [One-time purchases](./one-time-purchases.md) — durable and consumable items
- [Receiving and responding](../interactions/receiving-and-responding.md) — where the entitlement check happens
