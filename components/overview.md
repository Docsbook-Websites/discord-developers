---
title: Discord Message Components Overview
description: Add buttons, select menus, and text inputs to the messages and modals your app sends, and learn how the components flag changes message content.
---

Components add interactive elements to the messages your app sends and to modals it opens. They are accessible, customizable, and reusable across both surfaces.

![Examples of Discord component layouts in messages](https://raw.githubusercontent.com/discord/discord-api-docs/main/images/components/hero.png)

## The components flag

To use components, send messages with the `IS_COMPONENTS_V2` flag (`1<<15`). This flag disables traditional content and embeds, so every part of the message must be expressed as components instead.

Legacy message component behavior is not being deprecated and remains available on a message-by-message basis. New projects and features should use the current components.

## What you can send

<!-- widget:cards -->

- [Message components](./message-components.md) — Buttons and select menus that answer a click {square-mouse-pointer}
- [Modal components](./modals.md) — Text inputs that collect form data from one user {form-input}
- [Interactions overview](../interactions/overview.md) — How component clicks reach your app {mouse-pointer-click}

<!-- /widget -->

## How a component reaches your app

A user clicking a button or choosing from a select menu produces a `MESSAGE_COMPONENT` interaction, type `3`. Your app answers it like any other interaction, with the same three-second window. Two callback types exist for components specifically: `UPDATE_MESSAGE` (`7`) edits the message the component is attached to, and `DEFERRED_UPDATE_MESSAGE` (`6`) acknowledges without showing a loading state.

## Next steps

- [Message components](./message-components.md) — buttons and the select menu types
- [Modals](./modals.md) — collect input rather than a click
- [Receiving and responding](../interactions/receiving-and-responding.md) — callback types for component interactions
