# TicketTaker Integration Framework

**NOTE**: This is an early draft of our plugin API. Everything is subject to change as the product matures.

The TicketTaker Integration Framework allows developers to extend TicketTaker functionality.

## Overview

Developers publish Javascript files that are executed on the end-user's browser via `<script>` tags.

These files invoke `window.registerPlugin(mountPoint: string, component: React.ReactNode)` with two parameters:

1. `mountPoint` - A `string` that describes where in the application the plugin should be mounted.
2. `component` - A React component that receives data about the application through `props`

## Mount Points

The following is a list of possible values for the `mountPoint` argument of `window.registerPlugin`. These values describe where in the application the `component` returned by the plugin will be mounted.

Note: Multiple plugins can be mounted at the same locations. In this case, they will be rendered according to the order in which they invoked `window.registerPlugin`

- `root` - At the root of the application. Modals should use this mount point.

### Ticket List View

- `ticket-list-header` - At the top right of the Ticket List View. Useful for icons or notifications.
- `ticket-list-item-icons` - At the end of the list of icons shown when a ticket in the Ticket List view is focused or selected.
- `ticket-list-sidebar-top` - Under the header of the sidebar shown on the Ticket List view
- `ticket-list-sidebar-bottom` - Under all other content in the sidebar shown on the Ticket List view
- `ticket-list-sidebar-icons` - At the end of the list of icons in the sidebar shown on the Ticket List view

### Ticket View

- `ticket-icons` - At the end of the icons in the top right of the Ticket View
- `ticket-top` - Between the header and the new comment input field of the Ticket View
- `ticket-bottom` - Below all comments shown on Ticket View. (likely off screen unless scrolled to)
- `ticket-left-col` - Adds a column to the left of the comments on the Ticket View
- `ticket-right-col` - Adds a column to the right of the comments on the Ticket View

## Component

The second argument to `window.registerPlugin` is a React Component (or a function that receives props and returns a `React.ReactNode`).

The props passed to the component depend on the mount point.

### All Mount Points

- `eventStream` - An event emitter that notifies plugins about various actions that take place in the application
- `lazyLoad` - When `true`, the component is being loaded before it is displayed to the agent. TicketTaker may preloads components to improve UI response times.
- `currentUser` - Data about the currently signed in `User`

### Ticket List Items

- `ticket` - Data about the `Ticket` shown in the ticket list

## Event Stream

The `eventStream` passed to plugin components allows plugins to listen and respond to actions that occur.

Here are the events that are published to the `eventStream`:

### `TICKET_CHANGED`

A new ticket has been published or an existing ticket has been updated. Note: this event does not only fire when tickets are published/updated in the current dashboard. Any ticket creations or updates by any agent or end-user on TT or Zendesk will fire this event.

Payload:

- `ticket`: The full data for the created/updated `Ticket`

### `COMMENT_CHANGED`

A new comment has been published or an existing comment has been updated. Note: this event does not only fire when comments are published/updated in the current dashboard. Any comment creations or updates by any agent or end-user on TT or Zendesk will fire this event.

Payload:

- `comment`: The full data for the created/updated `Comment`

### `KEYBOARD_SHORTCUT_USED`

Fires when the user uses a keyboard shortcut on the current TT interface.

Payload:

- `keys`: A `string` describing the sequence of keys that was used

### `MACRO_USED`

Fires when the user uses a macro on the current TT interface.

Payload:

- `macro`: The `Macro` that was used

### `TICKET_OPEN_REQUEST`

Fires when the user opens the individual ticket view.

Payload:

- `method`: The shortcut or mouse method used to open the ticket `"click" | "g t" | "enter"`

Please contact us if there is an event you would like to use that we do not currently publish.
