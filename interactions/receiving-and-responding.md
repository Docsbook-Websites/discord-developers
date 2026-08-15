---
title: Receiving and Responding to Discord Interactions
description: Handle every Discord interaction type, answer inside the three-second window, defer long work, and pick the right interaction callback type.
---

Every interactive feature produces an interaction: a command run, a button click, a select menu choice, an autocomplete keystroke, or a modal submission. Your app reads the interaction's `type` field to know which one arrived.

## Interaction types

| Name | Value | Sent when |
|---|---|---|
| `PING` | 1 | Discord verifies your Interactions Endpoint URL |
| `APPLICATION_COMMAND` | 2 | A user runs one of your commands |
| `MESSAGE_COMPONENT` | 3 | A user clicks a button or uses a select menu |
| `APPLICATION_COMMAND_AUTOCOMPLETE` | 4 | A user is typing a command option value |
| `MODAL_SUBMIT` | 5 | A user submits a modal |

The `data` field's shape follows the type: command data for types `2` and `4`, message component data for type `3`, and modal submit data for type `5`. A `PING` carries no data.

## Answer within three seconds

An interaction token is valid for 15 minutes, but the initial response has a hard limit: your app must respond within **three seconds** or Discord marks the interaction as failed and the user sees an error.

When the work takes longer, acknowledge first and edit the response later:

- Reply with callback type `5` to show the user a loading state, then edit the response when the work finishes
- For component interactions, reply with type `6` to acknowledge without any loading state, then edit the original message

## Interaction callback types

| Name | Value | Description |
|---|---|---|
| `PONG` | 1 | Acknowledge a `PING` |
| `CHANNEL_MESSAGE_WITH_SOURCE` | 4 | Respond with a message |
| `DEFERRED_CHANNEL_MESSAGE_WITH_SOURCE` | 5 | Acknowledge and edit the response later; the user sees a loading state |
| `DEFERRED_UPDATE_MESSAGE` | 6 | For components, acknowledge and edit the original message later, with no loading state |
| `UPDATE_MESSAGE` | 7 | For components, edit the message the component was attached to |
| `APPLICATION_COMMAND_AUTOCOMPLETE_RESULT` | 8 | Respond to an autocomplete interaction with suggested choices |
| `MODAL` | 9 | Respond with a pop-up modal |
| `LAUNCH_ACTIVITY` | 12 | Launch the Activity associated with the app, for apps with Activities enabled |

Types `6` and `7` are valid only for component-based interactions. Type `9` is not available for `MODAL_SUBMIT` and `PING` interactions. Callback type `10`, `PREMIUM_REQUIRED`, is deprecated; see [monetization](../monetization/overview.md) for the current premium button style.

## A minimal response

Answer a command with a visible message:

```json
{
  "type": 4,
  "data": { "content": "Hello from my app" }
}
```

Acknowledge now and fill in the answer later:

```json
{ "type": 5 }
```

Respond to a `PING` during endpoint validation:

```json
{ "type": 1 }
```

Provide a valid `Content-Type` when you respond to a `PING`, or validation fails even though the payload is correct.

## Next steps

- [Securing your endpoint](./securing-your-endpoint.md) — verify signatures before you trust a request
- [Message components](../components/message-components.md) — components that produce type `3` interactions
- [Modals](../components/modals.md) — components that produce type `5` interactions
