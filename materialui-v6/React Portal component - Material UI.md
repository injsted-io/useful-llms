The Portal component lets you render its children into a DOM node that exists outside of the Portal's own DOM hierarchy.

-   [Feedback](https://github.com/mui/material-ui/labels/component%3A%20Portal)
-   [Bundle size](https://bundlephobia.com/package/@mui/material@latest "Scroll down to 'Exports Analysis' for a more detailed report.")

## [Introduction](https://v6.mui.com/material-ui/react-no-ssr/#introduction)

Portal is a utility component built around [React's `createPortal()` API](https://react.dev/reference/react-dom/createPortal). It gives you the functionality of `createPortal()` in a convenient component form. It's used internally by the [Modal](https://v6.mui.com/base-ui/react-modal/) and [Popper](https://v6.mui.com/base-ui/react-popper/) components.

Normally, children of a component are rendered within that component's DOM tree. But sometimes it's necessary to mount a child at a different location in the DOM. The Portal component accepts a `container` prop that passes a `ref` to the DOM node where its children will be mounted.

The following demo shows how a `<span>` nested within a Portal can be appended to a node outside of the Portal's DOM hierarchy—click **Mount children** to see how it behaves:

It looks like I will render here.

Press Enter to start editing

## [Basics](https://v6.mui.com/material-ui/react-no-ssr/#basics)

### [Import](https://v6.mui.com/material-ui/react-no-ssr/#import)

```jsx
import Portal from '@mui/material/Portal';
```

## [Customization](https://v6.mui.com/material-ui/react-no-ssr/#customization)

### [Server-side Portals](https://v6.mui.com/material-ui/react-no-ssr/#server-side-portals)

The DOM API isn't available on the server, so you need to use the `container` prop callback. This callback is called during a React layout effect:

```jsx
<Portal container={() => document.getElementById('filter-panel')!}> <Child /> </Portal>
```

## [API](https://v6.mui.com/material-ui/react-no-ssr/#api)

See the documentation below for a complete reference to all of the props and classes available to the components mentioned here.

-   [`<Portal />`](https://v6.mui.com/base-ui/react-portal/components-api/#portal)