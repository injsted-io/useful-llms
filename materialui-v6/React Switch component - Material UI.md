Switches toggle the state of a single setting on or off.

Switches are the preferred way to adjust settings on mobile. The option that the switch controls, as well as the state it's in, should be made clear from the corresponding inline label.

-   [Feedback](https://github.com/mui/material-ui/labels/component%3A%20switch)
-   [Bundle size](https://bundlephobia.com/package/@mui/material@latest "Scroll down to 'Exports Analysis' for a more detailed report.")
-   [Source](https://github.com/mui/material-ui/tree/v6.4.11/packages/mui-material/src/Switch)
-   [Material Design](https://m2.material.io/components/selection-controls#switches)
-   [Figma](https://mui.com/store/items/figma-react/?utm_source=docs&utm_medium=referral&utm_campaign=component-link-header)
-   [Sketch](https://mui.com/store/items/sketch-react/?utm_source=docs&utm_medium=referral&utm_campaign=component-link-header)

## [Basic switches](https://v6.mui.com/material-ui/all-components/#basic-switches)

Press Enter to start editing

## [Label](https://v6.mui.com/material-ui/all-components/#label)

You can provide a label to the `Switch` thanks to the `FormControlLabel` component.

Press Enter to start editing

## [Size](https://v6.mui.com/material-ui/all-components/#size)

Use the `size` prop to change the size of the switch.

Press Enter to start editing

## [Color](https://v6.mui.com/material-ui/all-components/#color)

Press Enter to start editing

## [Controlled](https://v6.mui.com/material-ui/all-components/#controlled)

You can control the switch with the `checked` and `onChange` props:

Press Enter to start editing

## [Switches with FormGroup](https://v6.mui.com/material-ui/all-components/#switches-with-formgroup)

`FormGroup` is a helpful wrapper used to group selection controls components that provides an easier API. However, you are encouraged to use [Checkboxes](https://v6.mui.com/material-ui/react-checkbox/) instead if multiple related controls are required. (See: [When to use](https://v6.mui.com/material-ui/all-components/#when-to-use)).

## [Customization](https://v6.mui.com/material-ui/all-components/#customization)

Here are some examples of customizing the component. You can learn more about this in the [overrides documentation page](https://v6.mui.com/material-ui/customization/how-to-customize/).

MUI switchAndroid 12iOS style

🎨 If you are looking for inspiration, you can check [MUI Treasury's customization examples](https://mui-treasury.com/?path=/docs/switch-introduction--docs).

## [Label placement](https://v6.mui.com/material-ui/all-components/#label-placement)

You can change the placement of the label:

## [When to use](https://v6.mui.com/material-ui/all-components/#when-to-use)

-   [Checkboxes vs. Switches](https://uxplanet.org/checkbox-vs-toggle-switch-7fc6e83f10b8)

## [Accessibility](https://v6.mui.com/material-ui/all-components/#accessibility)

-   It will render an element with the `checkbox` role not `switch` role since this role isn't widely supported yet. Please test first if assistive technology of your target audience supports this role properly. Then you can change the role with `<Switch inputProps={{ role: 'switch' }}>`
-   All form controls should have labels, and this includes radio buttons, checkboxes, and switches. In most cases, this is done by using the `<label>` element ([FormControlLabel](https://v6.mui.com/material-ui/api/form-control-label/)).
-   When a label can't be used, it's necessary to add an attribute directly to the input component. In this case, you can apply the additional attribute (for example `aria-label`, `aria-labelledby`, `title`) via the `inputProps` prop.

```jsx
<Switch value="checkedA" inputProps={{ 'aria-label': 'Switch A' }} />
```

## [Unstyled](https://v6.mui.com/material-ui/all-components/#unstyled)

Use the [Base UI Switch](https://v6.mui.com/base-ui/react-switch/) for complete ownership of the component's design, with no Material UI or Joy UI styles to override. This unstyled version of the component is the ideal choice for heavy customization with a smaller bundle size.

## [API](https://v6.mui.com/material-ui/all-components/#api)

See the documentation below for a complete reference to all of the props and classes available to the components mentioned here.

-   [`<FormControl />`](https://v6.mui.com/material-ui/api/form-control/)
-   [`<FormControlLabel />`](https://v6.mui.com/material-ui/api/form-control-label/)
-   [`<FormGroup />`](https://v6.mui.com/material-ui/api/form-group/)
-   [`<FormLabel />`](https://v6.mui.com/material-ui/api/form-label/)
-   [`<Switch />`](https://v6.mui.com/material-ui/api/switch/)