# Events

Plugin components are passed a prop called `eventStream`. Various parts of the application publish events to this stream. Your component may also publish events that other plugins can listen to by using the `emit` function.

### Events

* `TICKET_SELECTED` - Payload: `{ticketId: string}`
* `TICKET_DESELECTED` - Payload: `{ticketId: string}`
* `KEYBOARD_SHORTCUT_USED` - Payload: `{keys: string}`
* `COMMAND_PALETTE_OPENED`
* `COMMAND_PALETTE_CLOSED` - Payload: `{command: {name: string, command: () => void}}`
* `VIEW_OPEN_REQUST` - Payload: `{method: 'command-palette'}`
* `TICKET_OPEN_REQUST` - Payload: `{ticketId: string, method: 'g t' | 'click' | 'enter'}`
* `TICKET_CLOSE_REQUEST` - Payload: `{ticketId: string}`
* `SELECT_PROMPT_CLOSED` - Payload: `{selected: {value: string, label: string}}`



