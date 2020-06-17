# component

The second argument to `window.registerPlugin` is a React Component \(or a function that receives props and returns a `React.ReactNode`\).

The props passed to the component depend on the mount point.

#### All Mount Points

* `eventStream` - An event emitter that notifies plugins about various actions that take place in the application
* `lazyLoad` - When `true`, the component is being loaded before it is displayed to the agent. TicketTaker may preload components to improve UI response times.
* `currentUser` - Data about the currently signed in `User`
* `bindShortcut(keys: string, action: () => void, options: BindShortcutOptions = {}): () => void` 

  A function that allows extensions to add keyboard shortcuts. Returns a cleanup function that **must be called** when the component is done listening for the extension \(e.g. on un-mount\).

  * `keys: string` - the keys that should trigger the action
  * `action: () => void` - the function that should be invoked when the shortcut is used
  * `options: BindShortcutOptions`
    * `options.global?: boolean` - if true, the shortcut will work even when an input element is focused
    * `options.action?: 'keydown' | 'keypress' | 'keyup'` - which event should trigger the shortcut
    * `options.description: string` - the description that will be shown to the user on the shortcut help guide

* `whitelistShortcuts(combos: string[] | null): void`- When invoked, only keyboard shortcuts passed to this function will be recognized by the application. You **must** invoke `whitelistShortcuts(null)` to re-enable all shortcuts
* `components` - Some common components that are shared across plugins
  * `Key` - A component that should be used to represent a keyboard shortcut. Works with multikey shortcuts and modifiers \(e.g. `a m`, or `alt+u`\)

#### 

#### Ticket List Items

* `ticket` - Data about the `Ticket` shown in the ticket list

