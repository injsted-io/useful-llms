A Toggle Button can be used to group related options.

To emphasize groups of related Toggle buttons, a group should share a common container. The `ToggleButtonGroup` controls the selected state of its child buttons when given its own `value` prop.

-   [Feedback](https://github.com/mui/material-ui/labels/component%3A%20toggle%20button)
-   [Bundle size](https://bundlephobia.com/package/@mui/material@latest "Scroll down to 'Exports Analysis' for a more detailed report.")
-   [Source](https://github.com/mui/material-ui/tree/v6.4.11/packages/mui-material/src/ToggleButton)
-   [Material Design](https://m2.material.io/components/buttons#toggle-button)
-   [Figma](https://mui.com/store/items/figma-react/?utm_source=docs&utm_medium=referral&utm_campaign=component-link-header)
-   [Sketch](https://mui.com/store/items/sketch-react/?utm_source=docs&utm_medium=referral&utm_campaign=component-link-header)

## [Exclusive selection](https://v6.mui.com/material-ui/all-components/#exclusive-selection)

With exclusive selection, selecting one option deselects any other.

In this example, text justification toggle buttons present options for left, center, right, and fully justified text (disabled), with only one item available for selection at a time.

**Note**: Exclusive selection does not enforce that a button must be active. For that effect see [enforce value set](https://v6.mui.com/material-ui/all-components/#enforce-value-set).

## [Multiple selection](https://v6.mui.com/material-ui/all-components/#multiple-selection)

Multiple selection allows for logically-grouped options, like bold, italic, and underline, to have multiple options selected.

## [Size](https://v6.mui.com/material-ui/all-components/#size)

For larger or smaller buttons, use the `size` prop.

Press Enter to start editing

## [Color](https://v6.mui.com/material-ui/all-components/#color)

Press Enter to start editing

## [Vertical buttons](https://v6.mui.com/material-ui/all-components/#vertical-buttons)

The buttons can be stacked vertically with the `orientation` prop set to "vertical".

Press Enter to start editing

## [Enforce value set](https://v6.mui.com/material-ui/all-components/#enforce-value-set)

If you want to enforce that at least one button must be active, you can adapt your handleChange function.

```jsx
const handleAlignment = (event, newAlignment) => { if (newAlignment !== null) { setAlignment(newAlignment); } }; const handleDevices = (event, newDevices) => { if (newDevices.length) { setDevices(newDevices); } };
```

## [Standalone toggle button](https://v6.mui.com/material-ui/all-components/#standalone-toggle-button)

Press Enter to start editing

## [Customization](https://v6.mui.com/material-ui/all-components/#customization)

Here is an example of customizing the component. You can learn more about this in the [overrides documentation page](https://v6.mui.com/material-ui/customization/how-to-customize/).

## [Accessibility](https://v6.mui.com/material-ui/all-components/#accessibility)

### [ARIA](https://v6.mui.com/material-ui/all-components/#aria)

-   ToggleButtonGroup has `role="group"`. You should provide an accessible label with `aria-label="label"`, `aria-labelledby="id"` or `<label>`.
-   ToggleButton sets `aria-pressed="<bool>"` according to the button state. You should label each button with `aria-label`.

### [Keyboard](https://v6.mui.com/material-ui/all-components/#keyboard)

At present, toggle buttons are in DOM order. Navigate between them with the tab key. The button behavior follows standard keyboard semantics.

## [API](https://v6.mui.com/material-ui/all-components/#api)

See the documentation below for a complete reference to all of the props and classes available to the components mentioned here.

-   [`<ToggleButton />`](https://v6.mui.com/material-ui/api/toggle-button/)
-   [`<ToggleButtonGroup />`](https://v6.mui.com/material-ui/api/toggle-button-group/)