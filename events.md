---
title: Receive Discord Events Over Gateway and Webhooks
description: Compare Discord's Gateway WebSocket, HTTP webhook events, and Embedded App SDK events, and learn which transport carries which kind of event.
---

Apps listen to events to stay current with changes in servers, users, and the app itself. Three transports deliver events, and they are not interchangeable.

## The three transports

| Transport | Carries | Requires |
|---|---|---|
| Gateway | Most events, including messages, joins, reactions, and voice state | A persistent WebSocket connection |
| Webhook events | A small set unavailable elsewhere, such as Application Authorized | A public HTTPS endpoint |
| Embedded App SDK | Activity-scoped events such as voice status and screen orientation | An Activity using the SDK |

## Gateway events

The Gateway is the primary way apps receive events. Most events related to channels, guilds, roles, and messages are available **only** over a Gateway connection.

Gateway events travel over a WebSocket connection your app opens and maintains. That connection has a lifecycle: identify, heartbeat, resume after a disconnect, and reconnect when Discord asks.

![The lifecycle of a Discord Gateway connection](https://raw.githubusercontent.com/discord/discord-api-docs/main/images/events/gateway-lifecycle.svg)

Use a community library rather than implementing that loop yourself. Libraries handle heartbeats, resumes, and Gateway rate limits, which are the parts that fail quietly in production.

## Webhook events

Webhook events arrive at your app's Webhook Event URL over HTTP. Few events support this transport, but some exist nowhere else, including Application Authorized, which fires when your app is installed to a user or a server.

This suits serverless apps that otherwise have no reason to hold a connection open.

## Embedded App SDK events

Activities subscribe to SDK events with `subscribe()` and the event name. These cover the Activity's own context, such as a user's voice status or screen orientation.

## Intents

Gateway events are gated by intents, and some are privileged. Request only the intents your app uses: privileged intents require review once an app reaches verification, and asking for what you do not need turns into a rejection or a delay.

## Next steps

- [Choosing a transport](./get-started/choosing-a-transport.md) — Gateway or HTTP for interactions
- [API reference](./api-reference.md) — versions, authentication, and rate limits
- [Interactions overview](./interactions/overview.md) — the user-initiated half of the platform
