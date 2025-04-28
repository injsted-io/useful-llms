Select components are used for collecting user provided information from a list of options.

-   [Feedback](https://github.com/mui/material-ui/labels/component%3A%20select)
-   [Bundle size](https://bundlephobia.com/package/@mui/material@latest "Scroll down to 'Exports Analysis' for a more detailed report.")
-   [Source](https://github.com/mui/material-ui/tree/v6.4.11/packages/mui-material/src/Select)
-   [WAI-ARIA](https://www.w3.org/WAI/ARIA/apg/patterns/combobox/examples/combobox-select-only/)
-   [Material Design](https://m2.material.io/components/menus#exposed-dropdown-menu)
-   [Figma](https://mui.com/store/items/figma-react/?utm_source=docs&utm_medium=referral&utm_campaign=component-link-header)
-   [Sketch](https://mui.com/store/items/sketch-react/?utm_source=docs&utm_medium=referral&utm_campaign=component-link-header)

## [Basic select](https://v6.mui.com/material-ui/all-components/#basic-select)

Menus are positioned under their emitting elements, unless they are close to the bottom of the viewport.

Press Enter to start editing

## [Advanced features](https://v6.mui.com/material-ui/all-components/#advanced-features)

The Select component is meant to be interchangeable with a native `<select>` element.

If you are looking for more advanced features, like combobox, multiselect, autocomplete, async or creatable support, head to the [`Autocomplete` component](https://v6.mui.com/material-ui/react-autocomplete/). It's meant to be an improved version of the "react-select" and "downshift" packages.

## [Props](https://v6.mui.com/material-ui/all-components/#props)

The Select component is implemented as a custom `<input>` element of the [InputBase](https://v6.mui.com/material-ui/api/input-base/). It extends the [text field components](https://v6.mui.com/material-ui/react-text-field/) subcomponents, either the [OutlinedInput](https://v6.mui.com/material-ui/api/outlined-input/), [Input](https://v6.mui.com/material-ui/api/input/), or [FilledInput](https://v6.mui.com/material-ui/api/filled-input/), depending on the variant selected. It shares the same styles and many of the same props. Refer to the respective component's API page for details.

### [Filled and standard variants](https://v6.mui.com/material-ui/all-components/#filled-and-standard-variants)

### [Labels and helper text](https://v6.mui.com/material-ui/all-components/#labels-and-helper-text)

Age

With label + helper text

### [Auto width](https://v6.mui.com/material-ui/all-components/#auto-width)

### [Small Size](https://v6.mui.com/material-ui/all-components/#small-size)

### [Other props](https://v6.mui.com/material-ui/all-components/#other-props)

## [Native select](https://v6.mui.com/material-ui/all-components/#native-select)

As the user experience can be improved on mobile using the native select of the platform, we allow such pattern.

Press Enter to start editing

## [TextField](https://v6.mui.com/material-ui/all-components/#textfield)

The `TextField` wrapper component is a complete form control including a label, input and help text. You can find an example with the select mode [in this section](https://v6.mui.com/material-ui/react-text-field/#select).

## [Customization](https://v6.mui.com/material-ui/all-components/#customization)

Here are some examples of customizing the component. You can learn more about this in the [overrides documentation page](https://v6.mui.com/material-ui/customization/how-to-customize/).

The first step is to style the `InputBase` component. Once it's styled, you can either use it directly as a text field or provide it to the select `input` prop to have a `select` field. Notice that the `"standard"` variant is easier to customize, since it does not wrap the contents in a `fieldset`/`legend` markup.

🎨 If you are looking for inspiration, you can check [MUI Treasury's customization examples](https://mui-treasury.com/?path=/docs/select-introduction--docs).

## [Multiple select](https://v6.mui.com/material-ui/all-components/#multiple-select)

The `Select` component can handle multiple selections. It's enabled with the `multiple` prop.

Like with the single selection, you can pull out the new value by accessing `event.target.value` in the `onChange` callback. It's always an array.

### [Default](https://v6.mui.com/material-ui/all-components/#default)

### [Checkmarks](https://v6.mui.com/material-ui/all-components/#checkmarks)

### [Chip](https://v6.mui.com/material-ui/all-components/#chip)

### [Placeholder](https://v6.mui.com/material-ui/all-components/#placeholder)

### [Native](https://v6.mui.com/material-ui/all-components/#native)

## [Controlling the open state](https://v6.mui.com/material-ui/all-components/#controlling-the-open-state)

You can control the open state of the select with the `open` prop. Alternatively, it is also possible to set the initial (uncontrolled) open state of the component with the `defaultOpen` prop.

## [With a dialog](https://v6.mui.com/material-ui/all-components/#with-a-dialog)

While it's discouraged by the Material Design guidelines, you can use a select inside a dialog.

## [Grouping](https://v6.mui.com/material-ui/all-components/#grouping)

Display categories with the `ListSubheader` component or the native `<optgroup>` element.

## [Accessibility](https://v6.mui.com/material-ui/all-components/#accessibility)

To properly label your `Select` input you need an extra element with an `id` that contains a label. That `id` needs to match the `labelId` of the `Select`, for example:

```jsx
<InputLabel id="label">Age</InputLabel> <Select labelId="label" id="select" value="20"> <MenuItem value="10">Ten</MenuItem> <MenuItem value="20">Twenty</MenuItem> </Select>
```

Alternatively a `TextField` with an `id` and `label` creates the proper markup and ids for you:

```jsx
<TextField id="select" label="Age" value="20" select> <MenuItem value="10">Ten</MenuItem> <MenuItem value="20">Twenty</MenuItem> </TextField>
```

For a [native select](https://v6.mui.com/material-ui/all-components/#native-select), you should mention a label by giving the value of the `id` attribute of the select element to the `InputLabel`'s `htmlFor` attribute:

```jsx
<InputLabel htmlFor="select">Age</InputLabel> <NativeSelect id="select"> <option value="10">Ten</option> <option value="20">Twenty</option> </NativeSelect>
```

## [Unstyled](https://v6.mui.com/material-ui/all-components/#unstyled)

Use the [Base UI Select](https://v6.mui.com/base-ui/react-select/) for complete ownership of the component's design, with no Material UI or Joy UI styles to override. This unstyled version of the component is the ideal choice for heavy customization with a smaller bundle size.

## [API](https://v6.mui.com/material-ui/all-components/#api)

See the documentation below for a complete reference to all of the props and classes available to the components mentioned here.

-   [`<NativeSelect />`](https://v6.mui.com/material-ui/api/native-select/)
-   [`<Select />`](https://v6.mui.com/material-ui/api/select/)