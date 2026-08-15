---
title: Choose How Your Discord App Receives Interactions
description: Compare Discord's WebSocket Gateway with HTTP interaction endpoints, see what each transport delivers, and pick the one that fits your app.
---

Your app receives interactions in one of two mutually exclusive ways: over a WebSocket Gateway connection, or over HTTP through outgoing webhooks. By default an app receives interactions over the Gateway. Adding an Interactions Endpoint URL to your app's settings switches it to HTTP.

The choice affects hosting, not features, for interactions. It does affect which other events you can receive at all.

## What each transport gives you

| | Gateway (WebSocket) | HTTP endpoint |
|---|---|---|
| Interactions | Delivered over the connection | Delivered as POST requests |
| Other events (messages, joins, voice state) | Available | Not available |
| Hosting | A process that stays connected | Any public HTTPS endpoint |
| Serverless-friendly | No, the connection is persistent | Yes |
| Signature verification | Handled by the connection | Required on every request |

## Choose the Gateway when

Your app reacts to things that happen in Discord without a user invoking it: moderating messages, welcoming members, tracking voice state, or syncing roles. Most events related to channels, guilds, roles, and messages are only available over the Gateway.

The Gateway needs a process that stays online and maintains the connection, including heartbeats, resumes, and reconnects. Use a community library rather than writing that loop yourself.

![The lifecycle of a Discord Gateway connection](https://raw.githubusercontent.com/discord/discord-api-docs/main/images/events/gateway-lifecycle.svg)

## Choose HTTP when

Your app only ever answers user-initiated interactions: slash commands, button clicks, select menus, and modal submissions. Nothing needs to stay connected, so the app can run on serverless infrastructure and cost nothing while idle.

Two requirements come with HTTP, and Discord enforces both before it accepts your endpoint:

1. Acknowledge `PING` requests with a `PONG` response
2. Verify the `X-Signature-Ed25519` and `X-Signature-Timestamp` headers on every request

Both are covered in [securing your endpoint](../interactions/securing-your-endpoint.md).

## You can use both APIs

The transport question is about receiving. Regardless of which one you pick, your app calls the HTTP API to create messages, edit responses, register commands, and read resources. See the [API reference](../http-api.md).

## Next steps

- [Securing your endpoint](../interactions/securing-your-endpoint.md) — the two checks Discord requires
- [Events and the Gateway](../events.md) — event transports and what each one carries
- [Deploy on Cloudflare Workers](../guides/hosting-on-cloudflare-workers.md) — a working HTTP setup
