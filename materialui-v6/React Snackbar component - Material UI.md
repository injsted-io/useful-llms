Snackbars (also known as toasts) are used for brief notifications of processes that have been or will be performed.

-   [Feedback](https://github.com/mui/material-ui/labels/component%3A%20snackbar)
-   [Bundle size](https://bundlephobia.com/package/@mui/material@latest "Scroll down to 'Exports Analysis' for a more detailed report.")
-   [Source](https://github.com/mui/material-ui/tree/v6.4.11/packages/mui-material/src/Snackbar)
-   [WAI-ARIA](https://www.w3.org/TR/wai-aria-1.1/#alert)
-   [Material Design](https://m2.material.io/components/snackbars)
-   [Figma](https://mui.com/store/items/figma-react/?utm_source=docs&utm_medium=referral&utm_campaign=component-link-header)
-   [Sketch](https://mui.com/store/items/sketch-react/?utm_source=docs&utm_medium=referral&utm_campaign=component-link-header)

## [Introduction](https://v6.mui.com/material-ui/react-progress/#introduction)

The Snackbar component appears temporarily and floats above the UI to provide users with (non-critical) updates on an app's processes. The demo below, inspired by Google Keep, shows a basic Snackbar with a text element and two actions:

Press Enter to start editing

### [Usage](https://v6.mui.com/material-ui/react-progress/#usage)

Snackbars differ from [Alerts](https://v6.mui.com/material-ui/react-alert/) in that Snackbars have a fixed position and a high z-index, so they're intended to break out of the document flow; Alerts, on the other hand, are usually part of the flow—except when they're [used as children of a Snackbar](https://v6.mui.com/material-ui/react-progress/#use-with-alerts).

Snackbars also from differ from [Dialogs](https://v6.mui.com/material-ui/react-dialog/) in that Snackbars are not intended to convey _critical_ information or block the user from interacting with the rest of the app; Dialogs, by contrast, require input from the user in order to be dismissed.

## [Basics](https://v6.mui.com/material-ui/react-progress/#basics)

### [Import](https://v6.mui.com/material-ui/react-progress/#import)

```jsx
import Snackbar from '@mui/material/Snackbar';
```

### [Position](https://v6.mui.com/material-ui/react-progress/#position)

Use the `anchorOrigin` prop to control the Snackbar's position on the screen.

Press Enter to start editing

### [Content](https://v6.mui.com/material-ui/react-progress/#content)

```jsx
import SnackbarContent from '@mui/material/SnackbarContent';
```

Use the Snackbar Content component to add text and actions to the Snackbar.

### [Automatic dismiss](https://v6.mui.com/material-ui/react-progress/#automatic-dismiss)

Use the `autoHideDuration` prop to automatically trigger the Snackbar's `onClose` function after a set period of time (in milliseconds).

Make sure to [provide sufficient time](https://www.w3.org/TR/UNDERSTANDING-WCAG20/time-limits.html) for the user to process the information displayed on it.

Press Enter to start editing

### [Transitions](https://v6.mui.com/material-ui/react-progress/#transitions)

You can use the `TransitionComponent` prop to change the transition of the Snackbar from [Grow](https://v6.mui.com/material-ui/transitions/#grow) (the default) to others such as [Slide](https://v6.mui.com/material-ui/transitions/#slide).

Press Enter to start editing

## [Customization](https://v6.mui.com/material-ui/react-progress/#customization)

### [Use with Alerts](https://v6.mui.com/material-ui/react-progress/#use-with-alerts)

Use an Alert inside a Snackbar for messages that communicate a certain severity.

Press Enter to start editing

### [Use with Floating Action Buttons](https://v6.mui.com/material-ui/react-progress/#use-with-floating-action-buttons)

If you're using a [Floating Action Button](https://v6.mui.com/material-ui/react-floating-action-button/) on mobile, Material Design recommends positioning snackbars directly above it, as shown in the demo below:

## [Common examples](https://v6.mui.com/material-ui/react-progress/#common-examples)

### [Consecutive Snackbars](https://v6.mui.com/material-ui/react-progress/#consecutive-snackbars)

This demo shows how to display multiple Snackbars without stacking them by using a consecutive animation.

## [Supplementary components](https://v6.mui.com/material-ui/react-progress/#supplementary-components)

### [notistack](https://v6.mui.com/material-ui/react-progress/#notistack)

![stars](https://img.shields.io/github/stars/iamhosseindhv/notistack.svg?style=social&label=Star) ![npm downloads](https://img.shields.io/npm/dm/notistack.svg)

With an imperative API, [notistack](https://github.com/iamhosseindhv/notistack) lets you vertically stack multiple Snackbars without having to handle their open and close states. Even though this is discouraged in the Material Design guidelines, it is still a common pattern.

## [Accessibility](https://v6.mui.com/material-ui/react-progress/#accessibility)

The user should be able to dismiss Snackbars by pressing Escape. If there are multiple instances appearing at the same time and you want Escape to dismiss only the oldest one that's currently open, call `event.preventDefault` in the `onClose` prop.

```jsx
export default function MyComponent() { const [open, setOpen] = React.useState(true); return ( <React.Fragment> <Snackbar open={open} onClose={(event, reason) => { // `reason === 'escapeKeyDown'` if `Escape` was pressed setOpen(false); // call `event.preventDefault` to only close one Snackbar at a time. }} /> <Snackbar open={open} onClose={() => setOpen(false)} /> </React.Fragment> ); }
```

## [Anatomy](https://v6.mui.com/material-ui/react-progress/#anatomy)

The Snackbar component is composed of a root `<div>` that houses interior elements like the Snackbar Content and other optional components (such as buttons or decorators).

```html
<div role="presentation" class="MuiSnackbar-root"> <div class="MuiPaper-root MuiSnackbarContent-root" role="alert"> <div class="MuiSnackbarContent-message"> <!-- Snackbar content goes here --> </div> </div> </div>
```

### [useNotifications](https://v6.mui.com/material-ui/react-progress/#usenotifications)

You can create and manipulate notifications imperatively with the [`useNotifications()`](https://mui.com/toolpad/core/react-use-notifications/) API in `@toolpad/core`. This API provides state management for opening and closing snackbars. It also allows for queueing multiple notifications at once.

## [API](https://v6.mui.com/material-ui/react-progress/#api)

See the documentation below for a complete reference to all of the props and classes available to the components mentioned here.

-   [`<Snackbar />`](https://v6.mui.com/material-ui/api/snackbar/)
-   [`<SnackbarContent />`](https://v6.mui.com/material-ui/api/snackbar-content/)

Contents

[MUI stands in solidarity with Ukraine.](https://war.ukraine.ua/support-ukraine/)