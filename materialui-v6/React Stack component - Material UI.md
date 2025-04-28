Stack is a container component for arranging elements vertically or horizontally.

## [Introduction](https://v6.mui.com/material-ui/react-menu/#introduction)

The Stack component manages the layout of its immediate children along the vertical or horizontal axis, with optional spacing and dividers between each child.

-   [Feedback](https://github.com/mui/material-ui/labels/component%3A%20Stack)
-   [Bundle size](https://bundlephobia.com/package/@mui/material@latest "Scroll down to 'Exports Analysis' for a more detailed report.")
-   [Source](https://github.com/mui/material-ui/tree/v6.4.11/packages/mui-material/src/Stack)
-   [Figma](https://mui.com/store/items/figma-react/?utm_source=docs&utm_medium=referral&utm_campaign=component-link-header)
-   [Sketch](https://mui.com/store/items/sketch-react/?utm_source=docs&utm_medium=referral&utm_campaign=component-link-header)

## [Basics](https://v6.mui.com/material-ui/react-menu/#basics)

```jsx
import Stack from '@mui/material/Stack';
```

The Stack component acts as a generic container, wrapping around the elements to be arranged.

Use the `spacing` prop to control the space between children. The spacing value can be any number, including decimals, or a string. (The prop is converted into a CSS property using the [`theme.spacing()`](https://v6.mui.com/material-ui/customization/spacing/) helper.)

Press Enter to start editing

### [Stack vs. Grid](https://v6.mui.com/material-ui/react-menu/#stack-vs-grid)

`Stack` is concerned with one-dimensional layouts, while [Grid](https://v6.mui.com/material-ui/react-grid/) handles two-dimensional layouts. The default direction is `column` which stacks children vertically.

## [Direction](https://v6.mui.com/material-ui/react-menu/#direction)

By default, Stack arranges items vertically in a column. Use the `direction` prop to position items horizontally in a row:

Press Enter to start editing

## [Dividers](https://v6.mui.com/material-ui/react-menu/#dividers)

Use the `divider` prop to insert an element between each child. This works particularly well with the [Divider](https://v6.mui.com/material-ui/react-divider/) component, as shown below:

Press Enter to start editing

## [Responsive values](https://v6.mui.com/material-ui/react-menu/#responsive-values)

You can switch the `direction` or `spacing` values based on the active breakpoint.

Press Enter to start editing

## [Flexbox gap](https://v6.mui.com/material-ui/react-menu/#flexbox-gap)

To use [flexbox `gap`](https://developer.mozilla.org/en-US/docs/Web/CSS/gap) for the spacing implementation, set the `useFlexGap` prop to true.

It removes the [known limitations](https://v6.mui.com/material-ui/react-menu/#limitations) of the default implementation that uses CSS nested selector. However, CSS flexbox gap is not fully supported in some browsers.

We recommend checking the [support percentage](https://caniuse.com/?search=flex%20gap) before using it.

Press Enter to start editing

To set the prop to all stack instances, create a theme with default props:

```js
import { ThemeProvider, createTheme } from '@mui/material/styles'; import Stack from '@mui/material/Stack'; const theme = createTheme({ components: { MuiStack: { defaultProps: { useFlexGap: true, }, }, }, }); function App() { return ( <ThemeProvider theme={theme}> <Stack>…</Stack> {/* uses flexbox gap by default */} </ThemeProvider> ); }
```

## [Interactive demo](https://v6.mui.com/material-ui/react-menu/#interactive-demo)

Below is an interactive demo that lets you explore the visual results of the different settings:

```jsx
<Stack direction="row" spacing={2} sx={{ justifyContent: "center", alignItems: "center", }} >
```

## [System props](https://v6.mui.com/material-ui/react-menu/#system-props)

## [Limitations](https://v6.mui.com/material-ui/react-menu/#limitations)

### [Margin on the children](https://v6.mui.com/material-ui/react-menu/#margin-on-the-children)

Customizing the margin on the children is not supported by default.

For instance, the top-margin on the `Button` component below will be ignored.

```jsx
<Stack> <Button sx={{ marginTop: '30px' }}>...</Button> </Stack>
```

### [white-space: nowrap](https://v6.mui.com/material-ui/react-menu/#white-space-nowrap)

The initial setting on flex items is `min-width: auto`. This causes a positioning conflict when children use `white-space: nowrap;`. You can reproduce the issue with:

```jsx
<Stack direction="row"> <Typography noWrap>
```

In order for the item to stay within the container you need to set `min-width: 0`.

```jsx
<Stack direction="row" sx={{ minWidth: 0 }}> <Typography noWrap>
```

W

Truncation should be conditionally applicable on this long line of text as this is a much longer line than what the container can support.

Truncation should be conditionally applicable on this long line of text as this is a much longer line than what the container can support.

Press Enter to start editing

## [Anatomy](https://v6.mui.com/material-ui/react-menu/#anatomy)

The Stack component is composed of a single root `<div>` element:

```html
<div class="MuiStack-root"> <!-- Stack contents --> </div>
```

## [API](https://v6.mui.com/material-ui/react-menu/#api)

See the documentation below for a complete reference to all of the props and classes available to the components mentioned here.

-   [`<PigmentStack />`](https://v6.mui.com/material-ui/api/pigment-stack/)
-   [`<Stack />`](https://v6.mui.com/material-ui/api/stack/)