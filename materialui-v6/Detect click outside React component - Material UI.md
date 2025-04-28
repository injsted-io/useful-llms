## Click-Away Listener

The Click-Away Listener component detects when a click event happens outside of its child element.

-   [Feedback](https://github.com/mui/material-ui/labels/component%3A%20ClickAwayListener)
-   [Bundle size](https://bundlephobia.com/package/@mui/material@latest "Scroll down to 'Exports Analysis' for a more detailed report.")

## [Introduction](https://v6.mui.com/material-ui/react-menu/#introduction)

Click-Away Listener is a utility component that listens for click events outside of its child. (Note that it only accepts _one_ child element.) This is useful for components like the [Popper](https://v6.mui.com/material-ui/react-popper/) which should close when the user clicks anywhere else in the document. Click-Away Listener also supports the [Portal](https://v6.mui.com/material-ui/react-portal/) component.

The demo below shows how to hide a menu dropdown when users click anywhere else on the page:

Press Enter to start editing

## [Basics](https://v6.mui.com/material-ui/react-menu/#basics)

### [Import](https://v6.mui.com/material-ui/react-menu/#import)

```jsx
import ClickAwayListener from '@mui/material/ClickAwayListener';
```

## [Customization](https://v6.mui.com/material-ui/react-menu/#customization)

### [Use with Portal](https://v6.mui.com/material-ui/react-menu/#use-with-portal)

The following demo uses the [Portal](https://v6.mui.com/material-ui/react-portal/) component to render the dropdown into a new subtree outside of the current DOM hierarchy:

Press Enter to start editing

### [Listening for leading events](https://v6.mui.com/material-ui/react-menu/#listening-for-leading-events)

By default, the Click-Away Listener component responds to **trailing events**—the _end_ of a click or touch.

You can set the component to listen for **leading events** (the start of a click or touch) using the `mouseEvent` and `touchEvent` props, as shown in the following demo:

Press Enter to start editing

## [Accessibility](https://v6.mui.com/material-ui/react-menu/#accessibility)

By default, Click-Away Listener adds an `onClick` handler to its child. This can result in screen readers announcing that the child is clickable, even though this `onClick` handler has no effect on the child itself.

To prevent this behavior, add `role="presentation"` to the child element:

```tsx
<ClickAwayListener> <div role="presentation"> <h1>non-interactive heading</h1> </div> </ClickAwayListener>
```

This is also required to fix a known issue in NVDA when using Firefox that prevents the announcement of alert messages—see [this GitHub issue](https://github.com/mui/material-ui/issues/29080) for details.

## [API](https://v6.mui.com/material-ui/react-menu/#api)

See the documentation below for a complete reference to all of the props and classes available to the components mentioned here.

-   [`<ClickAwayListener />`](https://v6.mui.com/base-ui/react-click-away-listener/components-api/#click-away-listener)