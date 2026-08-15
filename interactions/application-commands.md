---
title: Discord Application Command Types and Structure
description: Create slash, user, message, and Entry Point commands, scope them globally or per server, and organize options with subcommands and groups.
---

Application commands give users a native way to invoke your app. Each command has a type that decides where it appears in the client and what data your app receives when it runs.

![The four application command types shown in the Discord client](https://raw.githubusercontent.com/discord/discord-api-docs/main/images/command-types.png)

## The four command types

<!-- widget:accordion -->

### Slash commands — typed in the chat input

The most common type. Users reach them by typing `/` or opening the command picker. A slash command carries a name, a description, and optional typed parameters.

![A slash command with its parameters in the chat input](https://raw.githubusercontent.com/discord/discord-api-docs/main/images/command.png)

### Message commands — act on a message

Reached through the context menu at the top-right of a message, or by right-clicking it, under Apps. Your app receives the target message with the interaction, so the command needs no parameters.

![A message command in the Apps context menu](https://raw.githubusercontent.com/discord/discord-api-docs/main/images/message-command.webp)

### User commands — act on a person

Reached by right-clicking a user profile, under Apps. Your app receives the target user with the interaction.

![A user command in the Apps context menu](https://raw.githubusercontent.com/discord/discord-api-docs/main/images/user-command.webp)

### Entry Point commands — launch an Activity

The primary way users launch an Activity from the App Launcher. Available to apps that have Activities enabled.

<!-- /widget -->

## Global and guild commands

A command is registered either globally or against a single server.

| Scope | Where it appears | Best for |
|---|---|---|
| Global | Everywhere your app is installed | Production commands |
| Guild | One server | Development and testing, because updates apply immediately |

Register a guild command while you iterate, then promote it to a global command when the shape settles.

```bash
curl -X POST \
  "https://discord.com/api/v10/applications/$APP_ID/guilds/$GUILD_ID/commands" \
  -H "Authorization: Bot $DISCORD_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"name": "hello", "type": 1, "description": "Say hello"}'
```

## Options, subcommands, and groups

Slash commands accept typed options. Discord validates the type in the client before the interaction reaches your app, so a user cannot submit a string where you asked for an integer.

When a command grows past a handful of options, split it with subcommands, and group subcommands when even that gets long.

![A command with groups, subcommands, and parameters](https://raw.githubusercontent.com/discord/discord-api-docs/main/images/command-with-groups-subcommands-parameters.png)

Autocomplete is a separate interaction type. When a user is still typing an option value, your app receives an `APPLICATION_COMMAND_AUTOCOMPLETE` interaction and answers with suggested choices rather than a message. See [receiving and responding](./receiving-and-responding.md).

## Next steps

- [Receiving and responding](./receiving-and-responding.md) — handle the interaction your command produces
- [Message components](../components/message-components.md) — add buttons and menus to the reply
- [API reference](../api-reference.md) — authentication and versioning for the registration call
