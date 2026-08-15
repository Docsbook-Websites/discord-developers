---
title: Host a Discord App on Cloudflare Workers
description: Deploy an HTTP interactions app to Cloudflare Workers with no server to maintain, verify Discord signatures at the edge, and route slash commands.
---

Cloudflare Workers suits an app that only answers interactions. There is no process to keep online, nothing to pay for while idle, and the endpoint is public HTTPS by default, which is what Discord requires.

This approach works only for HTTP interactions. If your app needs messages, member joins, or voice state, it needs a [Gateway connection](../events.md) and a host that stays connected.

## Before you start

You need a Cloudflare account, Node.js 18 or later, and an application in the [Developer Portal](https://discord.com/developers/applications) with its application ID, public key, and bot token at hand.

<!-- widget:stepper -->

### Create the Worker

Scaffold a Worker project locally and confirm it deploys before adding any Discord logic. Deploying an empty Worker first separates platform problems from app problems.

### Store your credentials as secrets

Your public key verifies incoming requests; your bot token authenticates outgoing calls. Keep both out of source control.

```bash
npx wrangler secret put DISCORD_PUBLIC_KEY
npx wrangler secret put DISCORD_TOKEN
```

### Verify the signature on every request

Reject anything that fails verification with `401` before your routing logic runs. Verify against the raw request body text, not a parsed and re-serialized object. See [securing your endpoint](../interactions/securing-your-endpoint.md).

### Answer PING requests

Discord sends a `PING` (`type: 1`) when you save the endpoint URL and expects `{ "type": 1 }` back with a valid `Content-Type`.

### Route the interaction

Branch on the interaction `type`, then on the command name or `custom_id`, and return a callback payload. Type `4` posts a message; type `5` acknowledges and lets you edit later.

### Register commands and set the endpoint URL

Register your commands against the API, then paste the Worker URL into the Interactions Endpoint URL field in the portal. Discord validates it immediately, so deploy before you save.

![The Interactions Endpoint URL field in the Developer Portal](https://raw.githubusercontent.com/discord/discord-api-docs/main/images/tutorials/cloudflare-interactions-endpoint.png)

<!-- /widget -->

## Install and test

Build an install link with the OAuth2 URL generator, choosing the `applications.commands` and `bot` scopes, then add the app to a test server.

![The OAuth2 URL generator in the Developer Portal](https://raw.githubusercontent.com/discord/discord-api-docs/main/images/tutorials/cloudflare-url-generator.png)

For local iteration, tunnel your development server to a public URL and point the endpoint at the tunnel, then switch it back to the Worker URL before you ship.

![A tunneled local endpoint used during development](https://raw.githubusercontent.com/discord/discord-api-docs/main/images/tutorials/cloudflare-ngrok.png)

## Watch the three-second limit

Cold starts and outbound calls both eat into the response window. If your handler calls another API, acknowledge with type `5` first and edit the response when the call returns.

## Next steps

- [Securing your endpoint](../interactions/securing-your-endpoint.md) — the verification code in full
- [Receiving and responding](../interactions/receiving-and-responding.md) — callback types and deferring
- [Choosing a transport](../get-started/choosing-a-transport.md) — when Workers are the wrong fit
