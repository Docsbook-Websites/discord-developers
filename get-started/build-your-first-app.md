---
title: Build Your First Discord App Step by Step
description: Register an application, add a bot user, install it to a test server, and handle your first slash command with a running Discord app.
---

This tutorial takes you from an empty Developer Portal to a bot that answers a slash command in a server you control.

You need a Discord account, a server where you have the Manage Server permission, and Node.js 18 or later if you follow the JavaScript examples.

![A Discord app responding to a slash command in a channel](https://raw.githubusercontent.com/discord/discord-api-docs/main/images/getting-started-demo.gif)

<!-- widget:stepper -->

### Create an application

Open the [Developer Portal](https://discord.com/developers/applications) and create an application. The application is the container for your bot user, OAuth2 settings, and credentials.

### Copy your credentials

From the application's settings, note three values:

- **Application ID** — the public identifier of your app
- **Public key** — used to verify interaction signatures
- **Bot token** — the secret your app authenticates with

Treat the bot token like a password. Store it in an environment variable, never in source control. If it leaks, reset it in the portal.

```bash
export DISCORD_TOKEN=YOUR_BOT_TOKEN
export APP_ID=YOUR_APPLICATION_ID
```

### Install the app to a test server

Use the OAuth2 URL generator in the portal to build an install link. Select the `applications.commands` and `bot` scopes, then choose the permissions your app needs. Open the generated URL and pick your test server.

![The default install settings for a Discord application](https://raw.githubusercontent.com/discord/discord-api-docs/main/images/getting-started-default-install.png)

Request only the permissions your app uses. Server admins see this list before they approve the install, and a long list costs you installs.

### Register a slash command

Commands are registered against the API, not declared in your source. A global command is available everywhere your app is installed; a guild command appears in one server and updates instantly, which makes it the better choice while developing.

```bash
curl -X POST \
  "https://discord.com/api/v10/applications/$APP_ID/guilds/$GUILD_ID/commands" \
  -H "Authorization: Bot $DISCORD_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"name": "hello", "type": 1, "description": "Say hello"}'
```

### Respond to the command

When someone runs `/hello`, Discord sends your app an interaction. Reply within three seconds with a callback type of `4` to post a message in the channel.

```json
{
  "type": 4,
  "data": { "content": "Hello from my first app" }
}
```

Details of every callback type are in [receiving and responding](../interactions/receiving-and-responding.md).

### Run it and invoke the command

Start your app, open your test server, type `/` in the message box, and pick your command. Your reply appears in the channel.

<!-- /widget -->

## Where your app receives the interaction

By default your app receives interactions over a Gateway connection. To receive them over HTTP instead, add an Interactions Endpoint URL in your app's settings.

![The Interactions Endpoint URL field in the Developer Portal](https://raw.githubusercontent.com/discord/discord-api-docs/main/images/getting-started-interactions-endpoint.png)

Discord validates that URL before it saves it, and validation fails unless your endpoint acknowledges `PING` requests and verifies request signatures. Both steps are covered in [securing your endpoint](../interactions/securing-your-endpoint.md).

## Next steps

- [Choose how to receive events](./choosing-a-transport.md) — Gateway or HTTP
- [Application commands](../interactions/application-commands.md) — command types, options, and subcommands
- [Deploy on Cloudflare Workers](../guides/hosting-on-cloudflare-workers.md) — host the HTTP version with no server to run
