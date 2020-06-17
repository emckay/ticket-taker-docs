# registerPlugin

Extensions invoke `window.registerPlugin(mountPoint: string, component: React.ReactNode)` with two parameters:

1. `mountPoint` - A `string` that describes where in the application the plugin should be mounted.
2. `component` - A React component that receives data about the application through `props`

