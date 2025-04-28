Alerts display brief messages for the user without interrupting their use of the app.

-   [Feedback](https://github.com/mui/material-ui/labels/component%3A%20alert)
-   [Bundle size](https://bundlephobia.com/package/@mui/material@latest "Scroll down to 'Exports Analysis' for a more detailed report.")
-   [Source](https://github.com/mui/material-ui/tree/v6.4.11/packages/mui-material/src/Alert)
-   [WAI-ARIA](https://www.w3.org/WAI/ARIA/apg/patterns/alert/)
-   [Figma](https://mui.com/store/items/figma-react/?utm_source=docs&utm_medium=referral&utm_campaign=component-link-header)
-   [Sketch](https://mui.com/store/items/sketch-react/?utm_source=docs&utm_medium=referral&utm_campaign=component-link-header)

## [Introduction](https://v6.mui.com/material-ui/all-components/#introduction)

Alerts give users brief and potentially time-sensitive information in an unobtrusive manner.

The Material UI Alert component includes several props for quickly customizing its styles to provide immediate visual cues about its contents.

Press Enter to start editing

### [Usage](https://v6.mui.com/material-ui/all-components/#usage)

A key trait of the alert pattern is that [it should not interrupt the user's experience](https://www.w3.org/WAI/ARIA/apg/patterns/alert/) of the app. Alerts should not be confused with alert _dialogs_ ([ARIA](https://www.w3.org/WAI/ARIA/apg/patterns/alertdialog/)), which _are_ intended to interrupt the user to obtain a response. Use the Material UI [Dialog](https://v6.mui.com/material-ui/react-dialog/) component if you need this behavior.

## [Basics](https://v6.mui.com/material-ui/all-components/#basics)

```jsx
import Alert from '@mui/material/Alert';
```

The Alert component wraps around its content, and stretches to fill its enclosing container.

### [Severity](https://v6.mui.com/material-ui/all-components/#severity)

The `severity` prop accepts four values representing different states—`success` (the default), `info`, `warning`, and `error`–with corresponding icon and color combinations for each:

Press Enter to start editing

### [Variants](https://v6.mui.com/material-ui/all-components/#variants)

The Alert component comes with two alternative style options—`filled` and `outlined`—which you can set using the `variant` prop.

#### Filled

Press Enter to start editing

#### Outlined

Press Enter to start editing

### [Color](https://v6.mui.com/material-ui/all-components/#color)

Use the `color` prop to override the default color for the specified [`severity`](https://v6.mui.com/material-ui/all-components/#severity)—for instance, to apply `warning` colors to a `success` Alert:

Press Enter to start editing

### [Actions](https://v6.mui.com/material-ui/all-components/#actions)

Add an action to your Alert with the `action` prop. This lets you insert any element—an HTML tag, an SVG icon, or a React component such as a Material UI Button—after the Alert's message, justified to the right.

If you provide an `onClose` callback to the Alert without setting the `action` prop, the component will display a close icon (✕) by default.

Press Enter to start editing

### [Icons](https://v6.mui.com/material-ui/all-components/#icons)

Use the `icon` prop to override an Alert's icon. As with the [`action`](https://v6.mui.com/material-ui/all-components/#actions) prop, your `icon` can be an HTML element, an SVG icon, or a React component. Set this prop to `false` to remove the icon altogether.

If you need to override all instances of an icon for a given [`severity`](https://v6.mui.com/material-ui/all-components/#severity), you can use the `iconMapping` prop instead. You can define this prop globally by customizing your app's theme. See [Theme components—Default props](https://v6.mui.com/material-ui/customization/theme-components/#theme-default-props) for details.

Press Enter to start editing

## [Customization](https://v6.mui.com/material-ui/all-components/#customization)

### [Titles](https://v6.mui.com/material-ui/all-components/#titles)

To add a title to an Alert, import the Alert Title component:

```jsx
import AlertTitle from '@mui/material/AlertTitle';
```

You can nest this component above the message in your Alert for a neatly styled and properly aligned title, as shown below:

Press Enter to start editing

### [Transitions](https://v6.mui.com/material-ui/all-components/#transitions)

You can use [Transition components](https://v6.mui.com/material-ui/transitions/) like [Collapse](https://v6.mui.com/material-ui/transitions/#collapse) to add motion to an Alert's entrance and exit.

## [Accessibility](https://v6.mui.com/material-ui/all-components/#accessibility)

Here are some factors to consider to ensure that your Alert is accessible:

-   Because alerts are not intended to interfere with the use of the app, your Alert component should _never_ affect the keyboard focus.
-   If an alert contains an action, that action must have a `tabindex` of `0` so it can be reached by keyboard-only users.
-   Essential alerts should not disappear automatically—[timed interactions](https://www.w3.org/TR/UNDERSTANDING-WCAG20/time-limits-no-exceptions.html) can make your app inaccessible to users who need extra time to understand or locate the alert.
-   Alerts that occur too frequently can [inhibit the usability](https://www.w3.org/TR/UNDERSTANDING-WCAG20/time-limits-postponed.html) of your app.
-   Dynamically rendered alerts are announced by screen readers; alerts that are already present on the page when it loads are _not_ announced.
-   Color does not add meaning to the UI for users who require assistive technology. You must ensure that any information conveyed through color is also denoted in other ways, such as within the text of the alert itself, or with additional hidden text that's read by screen readers.

## [Anatomy](https://v6.mui.com/material-ui/all-components/#anatomy)

The Alert component is composed of a root [Paper](https://v6.mui.com/material-ui/react-paper/) component (which renders as a `<div>`) that houses an icon, a message, and an optional [action](https://v6.mui.com/material-ui/all-components/#actions):

```html
<div class="MuiPaper-root MuiAlert-root" role="alert"> <div class="MuiAlert-icon"> <!-- svg icon here --> </div> <div class="MuiAlert-message">This is how an Alert renders in the DOM.</div> <div class="MuiAlert-action"> <!-- optional action element here --> </div> </div>
```

## [API](https://v6.mui.com/material-ui/all-components/#api)

See the documentation below for a complete reference to all of the props and classes available to the components mentioned here.

-   [`<Alert />`](https://v6.mui.com/material-ui/api/alert/)
-   [`<AlertTitle />`](https://v6.mui.com/material-ui/api/alert-title/)