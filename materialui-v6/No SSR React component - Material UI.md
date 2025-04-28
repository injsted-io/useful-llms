The No-SSR component defers the rendering of children components from the server to the client.

-   [Bundle size](https://bundlephobia.com/package/@mui/material@latest "Scroll down to 'Exports Analysis' for a more detailed report.")

## [Introduction](https://v6.mui.com/material-ui/react-no-ssr/#introduction)

No-SSR is a utility component that prevents its children from being rendered on the server, deferring their rendering to the client instead. This can be useful in a variety of situations, including:

-   To create an escape hatch for broken dependencies that don't support server-side rendering (SSR)
-   To improve the time to first paint by only rendering above the fold
-   To reduce the rendering time on the server
-   To turn on service degradation when the server load is too heavy
-   To improve the Time to Interactive (TTI) by only rendering what's important (using the `defer` prop)

The demo below illustrates how this component works:

Server and Client

Client only

Press Enter to start editing

## [Basics](https://v6.mui.com/material-ui/react-no-ssr/#basics)

### [Import](https://v6.mui.com/material-ui/react-no-ssr/#import)

```jsx
import NoSsr from '@mui/material/NoSsr';
```

## [Customization](https://v6.mui.com/material-ui/react-no-ssr/#customization)

### [Delay client-side rendering](https://v6.mui.com/material-ui/react-no-ssr/#delay-client-side-rendering)

You can also use No-SSR to delay the rendering of specific components on the client-side—for example, to let the rest of the application load before an especially complex or data-heavy component.

The following demo shows how to use the `defer` prop to prioritize rendering the rest of the app outside of what is nested within No-SSR:

## [API](https://v6.mui.com/material-ui/react-no-ssr/#api)

See the documentation below for a complete reference to all of the props and classes available to the components mentioned here.

-   [`<NoSsr />`](https://v6.mui.com/base-ui/react-no-ssr/components-api/#no-ssr)