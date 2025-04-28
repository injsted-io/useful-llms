A Popover can be used to display some content on top of another.

Things to know when using the `Popover` component:

-   The component is built on top of the [`Modal`](https://v6.mui.com/material-ui/react-modal/) component.
-   The scroll and click away are blocked unlike with the [`Popper`](https://v6.mui.com/material-ui/react-popper/) component.

-   [Feedback](https://github.com/mui/material-ui/labels/component%3A%20Popover)
-   [Bundle size](https://bundlephobia.com/package/@mui/material@latest "Scroll down to 'Exports Analysis' for a more detailed report.")
-   [Source](https://github.com/mui/material-ui/tree/v6.4.11/packages/mui-material/src/Popover)

## [Basic Popover](https://v6.mui.com/material-ui/react-no-ssr/#basic-popover)

Press Enter to start editing

## [Anchor playground](https://v6.mui.com/material-ui/react-no-ssr/#anchor-playground)

Use the radio buttons to adjust the `anchorOrigin` and `transformOrigin` positions. You can also set the `anchorReference` to `anchorPosition` or `anchorEl`. When it is `anchorPosition`, the component will, instead of `anchorEl`, refer to the `anchorPosition` prop which you can adjust to set the position of the popover.

```jsx
<Popover anchorOrigin={{ vertical: 'top', horizontal: 'left', }} transformOrigin={{ vertical: 'top', horizontal: 'left', }} > The content of the Popover. </Popover>
```

## [Mouse hover interaction](https://v6.mui.com/material-ui/react-no-ssr/#mouse-hover-interaction)

This demo demonstrates how to use the `Popover` component with `mouseenter` and `mouseleave` events to achieve popover behavior.

## [Virtual element](https://v6.mui.com/material-ui/react-no-ssr/#virtual-element)

The value of the `anchorEl` prop can be a reference to a fake DOM element. You need to provide an object with the following interface:

```ts
interface PopoverVirtualElement { nodeType: 1; getBoundingClientRect: () => DOMRect; }
```

Highlight part of the text to see the popover:

Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nullam ipsum purus, bibendum sit amet vulputate eget, porta semper ligula. Donec bibendum vulputate erat, ac fringilla mi finibus nec. Donec ac dolor sed dolor porttitor blandit vel vel purus. Fusce vel malesuada ligula. Nam quis vehicula ante, eu finibus est. Proin ullamcorper fermentum orci, quis finibus massa. Nunc lobortis, massa ut rutrum ultrices, metus metus finibus ex, sit amet facilisis neque enim sed neque. Quisque accumsan metus vel maximus consequat. Suspendisse lacinia tellus a libero volutpat maximus.

For more information on the virtual element's properties, see the following resources:

-   [getBoundingClientRect](https://developer.mozilla.org/en-US/docs/Web/API/Element/getBoundingClientRect)
-   [DOMRect](https://drafts.fxtf.org/geometry-1/#domrectreadonly)
-   [Node types](https://developer.mozilla.org/en-US/docs/Web/API/Node/nodeType)

## [Supplementary projects](https://v6.mui.com/material-ui/react-no-ssr/#supplementary-projects)

For more advanced use cases, you might be able to take advantage of:

![stars](https://img.shields.io/github/stars/jcoreio/material-ui-popup-state?style=social&label=Star) ![npm downloads](https://img.shields.io/npm/dm/material-ui-popup-state.svg)

The package [`material-ui-popup-state`](https://github.com/jcoreio/material-ui-popup-state) that takes care of popover state for you in most cases.

## [API](https://v6.mui.com/material-ui/react-no-ssr/#api)

See the documentation below for a complete reference to all of the props and classes available to the components mentioned here.

-   [`<Grow />`](https://v6.mui.com/material-ui/api/grow/)
-   [`<Popover />`](https://v6.mui.com/material-ui/api/popover/)