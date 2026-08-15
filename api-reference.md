---
title: Discord API Reference for Versions and Auth
description: Look up the Discord HTTP API base URL, supported versions, authentication header formats, snowflake IDs, and how rate limiting applies to your app.
---

The HTTP API is a REST API for core Discord resources: channels, guilds, users, and messages. Use it to read a resource, or to create, update, and delete one.

## Base URL and versioning

Specify the version in the request path:

```
https://discord.com/api/v{version_number}
```

Omitting the version routes the request to the current default version. Some versions are discontinued and return `400 Bad Request`.

| Version | Status |
|---|---|
| 10 | Available |
| 9 | Available |
| 8 | Deprecated |
| 7 | Deprecated |
| 6 | Deprecated (current default) |
| 5 and below | Discontinued |

Pin `v10` in new apps. Relying on the default routes you to a deprecated version.

## Authentication

Authentication uses the `Authorization` header in the format `TOKEN_TYPE TOKEN`.

```
Authorization: Bot YOUR_BOT_TOKEN
```

```
Authorization: Bearer YOUR_ACCESS_TOKEN
```

Bot tokens authenticate your app itself. Bearer tokens come from OAuth2 and act for a user who granted your app access.

## Try a request

<!-- widget:api -->

## GET /users/@me

Return the account of the authenticated app or user. With a bot token this returns your app's bot user.

| Field | Type | Required | Description |
|---|---|---|---|
| `Authorization` | string | yes | `Bot YOUR_BOT_TOKEN` or `Bearer YOUR_ACCESS_TOKEN` |

### Example

```bash
curl -X GET "https://discord.com/api/v10/users/@me" \
  -H "Authorization: Bot YOUR_BOT_TOKEN"
```

### Errors

| Status | Meaning |
|---|---|
| `401` | Missing or invalid token |
| `429` | Rate limited; retry after the interval in the response |

<!-- /widget -->

## Snowflake IDs

Discord IDs are snowflakes: 64-bit integers that encode a timestamp, which makes them sortable by creation time. They are serialized as strings in JSON because they exceed what some languages represent safely as numbers. Store and compare them as strings.

## Rate limiting

The HTTP API limits excessive requests in accordance with RFC 6585. Apps that regularly hit and ignore rate limits have their keys revoked and are blocked from the platform. Respect the retry interval the API returns rather than retrying immediately.

## Request requirements

- Send a descriptive `User-Agent` identifying your app
- Send a valid `Content-Type` on requests with a body, including `PING` responses
- Handle nullable and optional fields separately: an absent field and a `null` field mean different things

## Next steps

- [Events and the Gateway](./events.md) — the WebSocket half of the platform
- [Interactions overview](./interactions/overview.md) — the interaction model
- [Build your first app](./get-started/build-your-first-app.md) — a working app that uses these endpoints
