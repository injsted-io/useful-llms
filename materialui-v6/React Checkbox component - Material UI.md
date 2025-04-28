Checkboxes allow the user to select one or more items from a set.

Checkboxes can be used to turn an option on or off.

If you have multiple options appearing in a list, you can preserve space by using checkboxes instead of on/off switches. If you have a single option, avoid using a checkbox and use an on/off switch instead.

-   [Feedback](https://github.com/mui/material-ui/labels/component%3A%20checkbox)
-   [Bundle size](https://bundlephobia.com/package/@mui/material@latest "Scroll down to 'Exports Analysis' for a more detailed report.")
-   [Source](https://github.com/mui/material-ui/tree/v6.4.11/packages/mui-material/src/Checkbox)
-   [WAI-ARIA](https://www.w3.org/WAI/ARIA/apg/patterns/checkbox/)
-   [Material Design](https://m2.material.io/components/selection-controls#checkboxes)
-   [Figma](https://mui.com/store/items/figma-react/?utm_source=docs&utm_medium=referral&utm_campaign=component-link-header)
-   [Sketch](https://mui.com/store/items/sketch-react/?utm_source=docs&utm_medium=referral&utm_campaign=component-link-header)

## [Basic checkboxes](https://v6.mui.com/material-ui/all-components/#basic-checkboxes)

Press Enter to start editing

## [Label](https://v6.mui.com/material-ui/all-components/#label)

You can provide a label to the `Checkbox` thanks to the `FormControlLabel` component.

Press Enter to start editing

## [Size](https://v6.mui.com/material-ui/all-components/#size)

Use the `size` prop or customize the font size of the svg icons to change the size of the checkboxes.

Press Enter to start editing

## [Color](https://v6.mui.com/material-ui/all-components/#color)

Press Enter to start editing

## [Icon](https://v6.mui.com/material-ui/all-components/#icon)

Press Enter to start editing

## [Controlled](https://v6.mui.com/material-ui/all-components/#controlled)

You can control the checkbox with the `checked` and `onChange` props:

Press Enter to start editing

## [Indeterminate](https://v6.mui.com/material-ui/all-components/#indeterminate)

A checkbox input can only have two states in a form: checked or unchecked. It either submits its value or doesn't. Visually, there are **three** states a checkbox can be in: checked, unchecked, or indeterminate.

You can change the indeterminate icon using the `indeterminateIcon` prop.

Press Enter to start editing

## [FormGroup](https://v6.mui.com/material-ui/all-components/#formgroup)

`FormGroup` is a helpful wrapper used to group selection control components.

## [Label placement](https://v6.mui.com/material-ui/all-components/#label-placement)

You can change the placement of the label:

## [Customization](https://v6.mui.com/material-ui/all-components/#customization)

Here is an example of customizing the component. You can learn more about this in the [overrides documentation page](https://v6.mui.com/material-ui/customization/how-to-customize/).

Press Enter to start editing

🎨 If you are looking for inspiration, you can check [MUI Treasury's customization examples](https://mui-treasury.com/?path=/docs/checkbox-introduction--docs).

## [When to use](https://v6.mui.com/material-ui/all-components/#when-to-use)

-   [Checkboxes vs. Radio Buttons](https://www.nngroup.com/articles/checkboxes-vs-radio-buttons/)
-   [Checkboxes vs. Switches](https://uxplanet.org/checkbox-vs-toggle-switch-7fc6e83f10b8)

## [Accessibility](https://v6.mui.com/material-ui/all-components/#accessibility)

(WAI-ARIA: [https://www.w3.org/WAI/ARIA/apg/patterns/checkbox/](https://www.w3.org/WAI/ARIA/apg/patterns/checkbox/))

-   All form controls should have labels, and this includes radio buttons, checkboxes, and switches. In most cases, this is done by using the `<label>` element ([FormControlLabel](https://v6.mui.com/material-ui/api/form-control-label/)).
-   When a label can't be used, it's necessary to add an attribute directly to the input component. In this case, you can apply the additional attribute (for example `aria-label`, `aria-labelledby`, `title`) via the `inputProps` prop.

```jsx
<Checkbox value="checkedA" inputProps={{ 'aria-label': 'Checkbox A', }} />
```

## [API](https://v6.mui.com/material-ui/all-components/#api)

See the documentation below for a complete reference to all of the props and classes available to the components mentioned here.

-   [`<Checkbox />`](https://v6.mui.com/material-ui/api/checkbox/)
-   [`<FormControl />`](https://v6.mui.com/material-ui/api/form-control/)
-   [`<FormControlLabel />`](https://v6.mui.com/material-ui/api/form-control-label/)
-   [`<FormGroup />`](https://v6.mui.com/material-ui/api/form-group/)
-   [`<FormLabel />`](https://v6.mui.com/material-ui/api/form-label/)