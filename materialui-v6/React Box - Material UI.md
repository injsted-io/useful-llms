The Box component is a generic, theme-aware container with access to CSS utilities from MUI System.

-   [Feedback](https://github.com/mui/material-ui/labels/component%3A%20Box)
-   [Bundle size](https://bundlephobia.com/package/@mui/material@latest "Scroll down to 'Exports Analysis' for a more detailed report.")
-   [Source](https://github.com/mui/material-ui/tree/v6.4.11/packages/mui-material/src/Box)

## [Introduction](https://v6.mui.com/material-ui/react-menu/#introduction)

The Box component is a generic container for grouping other components. It's a fundamental building block when working with Material UI—you can think of it as a `<div>` with extra built-in features, like access to your app's theme and the [`sx` prop](https://v6.mui.com/system/getting-started/the-sx-prop/).

### [Usage](https://v6.mui.com/material-ui/react-menu/#usage)

The Box component differs from other containers available in Material UI in that its usage is intended to be multipurpose and open-ended, just like a `<div>`. Components like [Container](https://v6.mui.com/material-ui/react-container/), [Stack](https://v6.mui.com/material-ui/react-stack/) and [Paper](https://v6.mui.com/material-ui/react-paper/), by contrast, feature usage-specific props that make them ideal for certain use cases: Container for main layout orientation, Stack for one-dimensional layouts, and Paper for elevated surfaces.

## [Basics](https://v6.mui.com/material-ui/react-menu/#basics)

```jsx
import Box from '@mui/material/Box';
```

The Box component renders as a `<div>` by default, but you can swap in any other valid HTML tag or React component using the `component` prop. The demo below replaces the `<div>` with a `<section>` element:

This Box renders as an HTML section element.

Press Enter to start editing

## [Customization](https://v6.mui.com/material-ui/react-menu/#customization)

### [With the sx prop](https://v6.mui.com/material-ui/react-menu/#with-the-sx-prop)

Use the [`sx` prop](https://v6.mui.com/system/getting-started/the-sx-prop/) to quickly customize any Box instance using a superset of CSS that has access to all the style functions and theme-aware properties exposed in the MUI System package. The demo below shows how to apply colors from the theme using this prop:

Press Enter to start editing

### [With MUI System props](https://v6.mui.com/material-ui/react-menu/#with-mui-system-props)

## [Anatomy](https://v6.mui.com/material-ui/react-menu/#anatomy)

The Box component is composed of a single root `<div>` element:

```html
<div className="MuiBox-root"> <!-- contents of the Box --> </div>
```

## [API](https://v6.mui.com/material-ui/react-menu/#api)

See the documentation below for a complete reference to all of the props and classes available to the components mentioned here.

-   [`<Box />`](https://v6.mui.com/material-ui/api/box/)