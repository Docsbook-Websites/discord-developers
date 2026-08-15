---
title: Discord Developer Platform Documentation
description: Build bots, Activities, and game integrations on Discord. Learn interactions, message components, the HTTP and Gateway APIs, and app monetization.
---

Build apps that run where your users already are. A Discord app can answer a slash command, open a modal, launch a multiplayer Activity in a voice channel, or sell a subscription through Discord's own checkout.

Every bot, Activity, and Social SDK integration is backed by an application registered in the [Discord Developer Portal](https://discord.com/developers/applications). The application holds your credentials, OAuth2 settings, bot configuration, and metadata.

<!-- widget:cards -->

## Start here

- [What Discord apps are](./get-started/overview-of-apps.md) — The three app types and where each one installs {compass}
- [Build your first app](./get-started/build-your-first-app.md) — Register an app, run it, and invoke a command {rocket}
- [Choose how to receive events](./get-started/choosing-a-transport.md) — Gateway connection or HTTP endpoint {git-compare}

## Interactions

- [Interactions overview](./interactions/overview.md) — Commands, components, and modals in one model {mouse-pointer-click}
- [Application commands](./interactions/application-commands.md) — Slash, user, message, and Entry Point commands {terminal}
- [Receiving and responding](./interactions/receiving-and-responding.md) — The 3-second window and every callback type {reply}
- [Secure your endpoint](./interactions/securing-your-endpoint.md) — Verify Ed25519 signatures before you trust a request {shield-check}

## Components

- [Components overview](./components/overview.md) — Interactive elements inside the messages your app sends {layout-grid}
- [Message components](./components/message-components.md) — Buttons and select menus that reply to a click {square-mouse-pointer}
- [Modal components](./components/modals.md) — Collect form input from a single user {form-input}

## Monetize

- [Monetization overview](./monetization/overview.md) — SKUs, entitlements, and subscriptions {credit-card}
- [Subscriptions](./monetization/subscriptions.md) — Recurring access for a user or a whole server {repeat}
- [One-time purchases](./monetization/one-time-purchases.md) — Durable upgrades and consumable items {shopping-cart}

## Reference

- [API reference](./http-api.md) — Base URL, versions, authentication, and rate limits {book-open}
- [Events and the Gateway](./events.md) — Real-time events over WebSocket and webhooks {radio}
- [Deploy on Cloudflare Workers](./guides/hosting-on-cloudflare-workers.md) — Host an HTTP interactions app with no server {cloud}

<!-- /widget -->

## What you can build

| App type | Installs to | What it unlocks |
|---|---|---|
| Bot (guild-installed) | A server | Access to server channels, members, and events |
| Bot (user-installed) | A user | Available in DMs, group DMs, and any server |
| Activity | An application | Launchable from any voice channel |
| Social SDK | Your game | Social features embedded in your game client |

<!-- widget:cta -->

**Start building**

## Create an application in the Developer Portal

Register an app, grab its credentials, and invoke your first command in a server you control.

[Open the Developer Portal](https://discord.com/developers/applications) · [Build your first app](./get-started/build-your-first-app.md)

<!-- /widget -->
