---
title: Overview of Discord Apps and How They Install
description: Compare Discord bots, Activities, and the Social SDK, learn where each app type installs, and pick the APIs your integration needs.
---

A Discord application is the entity that represents your integration with the platform. Every bot, Activity, and Social SDK integration is backed by an application registered in the [Discord Developer Portal](https://discord.com/developers/applications).

Applications hold your credentials, OAuth2 settings, bot configuration, and metadata. Whether you build a command-response bot or a full game integration with voice chat and rich presence, it starts with creating an application.

## The three types of Discord apps

### Bots

Bots are automated accounts operated by application code. They appear in servers with an `APP` tag and respond to events, slash commands, and user actions.

Use a bot when you want to:

- Add commands, moderation tools, or utilities to a server
- React to events such as messages, joins, and reactions in real time
- Build interactive experiences with buttons, menus, and modals
- Post automated updates from external systems

Bots install to a server (guild-installed) or to a person (user-installed), which makes them available everywhere that user goes without requiring server permissions.

### Activities

Activities are embedded web applications that run inside Discord channels. They are built with the Embedded App SDK and can be launched by any user in a channel, or from a bot through the `LAUNCH_ACTIVITY` interaction callback.

Use an Activity when you want to build a game, a watch party, a drawing app, or any collaborative tool that runs inside Discord and reuses its voice and social context.

### Social layer for games

The Discord Social SDK adds Discord-powered social features to a game across PC, mobile, and console: rich presence, friends lists, voice chat, and cross-platform account linking. You can adopt individual features alongside your existing social systems.

## Where apps install

| App type | Install target | What it unlocks |
|---|---|---|
| Bot (guild-installed) | A server | Access to server channels, members, events |
| Bot (user-installed) | A user | Available in DMs, group DMs, and any server |
| Activity | An application | Launchable from any voice channel |
| Social SDK | Your game | Social features embedded in your game client |

## Which API you use

Pick the APIs based on the Discord features your app touches. Most bots use the first two.

<!-- widget:accordion -->

### HTTP API — read and change Discord resources

A REST API for core resources: channels, guilds, users, and messages. Use it to retrieve information about a resource, or to create, update, and delete one. See the [API reference](../http-api.md) for the base URL, versions, and authentication.

### Gateway API — receive real-time events

A WebSocket connection between your app and Discord. Most events, including messages, member joins, reactions, and voice state changes, are available only over the Gateway. The connection is bidirectional, so your app can also send events. See [events and the Gateway](../events.md).

### Interactions — respond when a user invokes your app

Commands, message components, and modals arrive as interactions. Your app receives them over a Gateway connection by default, or over HTTP if you configure an Interactions Endpoint URL. See the [interactions overview](../interactions/overview.md).

### Embedded App SDK — build inside a channel

The SDK that Activities use to run inside Discord, subscribe to SDK events, and read the user's context.

<!-- /widget -->

## Next steps

- [Build your first app](./build-your-first-app.md) — register an app and invoke a command
- [Choose how to receive events](./choosing-a-transport.md) — Gateway or HTTP, and why it matters
- [Interactions overview](../interactions/overview.md) — the model behind commands and components
