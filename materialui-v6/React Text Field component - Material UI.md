Text Fields let users enter and edit text.

Text fields allow users to enter text into a UI. They typically appear in forms and dialogs.

-   [Feedback](https://github.com/mui/material-ui/labels/component%3A%20text%20field)
-   [Bundle size](https://bundlephobia.com/package/@mui/material@latest "Scroll down to 'Exports Analysis' for a more detailed report.")
-   [Source](https://github.com/mui/material-ui/tree/v6.4.11/packages/mui-material/src/TextField)
-   [Material Design](https://m2.material.io/components/text-fields)
-   [Figma](https://mui.com/store/items/figma-react/?utm_source=docs&utm_medium=referral&utm_campaign=component-link-header)
-   [Sketch](https://mui.com/store/items/sketch-react/?utm_source=docs&utm_medium=referral&utm_campaign=component-link-header)

## [Basic TextField](https://v6.mui.com/material-ui/all-components/#basic-textfield)

The `TextField` wrapper component is a complete form control including a label, input, and help text. It comes with three variants: outlined (default), filled, and standard.

Press Enter to start editing

## [Form props](https://v6.mui.com/material-ui/all-components/#form-props)

Standard form attributes are supported, for example `required`, `disabled`, `type`, etc. as well as a `helperText` which is used to give context about a field's input, such as how the input will be used.

## [Validation](https://v6.mui.com/material-ui/all-components/#validation)

The `error` prop toggles the error state. The `helperText` prop can then be used to provide feedback to the user about the error.

## [Multiline](https://v6.mui.com/material-ui/all-components/#multiline)

The `multiline` prop transforms the Text Field into a [MUI Base Textarea Autosize](https://v6.mui.com/base-ui/react-textarea-autosize/) element. Unless the `rows` prop is set, the height of the text field dynamically matches its content. You can use the `minRows` and `maxRows` props to bound it.

## [Select](https://v6.mui.com/material-ui/all-components/#select)

The `select` prop makes the text field use the [Select](https://v6.mui.com/material-ui/react-select/) component internally.

Select

Please select your currency

Native select

Please select your currency

Select

Please select your currency

Native select

Please select your currency

Select

Please select your currency

Native select

Please select your currency

## [Icons](https://v6.mui.com/material-ui/all-components/#icons)

There are multiple ways to display an icon with a text field.

### [Input Adornments](https://v6.mui.com/material-ui/all-components/#input-adornments)

The main way is with an `InputAdornment`. This can be used to add a prefix, a suffix, or an action to an input. For instance, you can use an icon button to hide or reveal the password.

#### Customizing adornments

You can apply custom styles to adornments, and trigger changes to one based on attributes from another. For example, the demo below uses the label's `[data-shrink=true]` attribute to make the suffix visible (via opacity) when the label is in its shrunken state.

## [Sizes](https://v6.mui.com/material-ui/all-components/#sizes)

Fancy smaller inputs? Use the `size` prop.

The `filled` variant input height can be further reduced by rendering the label outside of it.

Press Enter to start editing

## [Margin](https://v6.mui.com/material-ui/all-components/#margin)

The `margin` prop can be used to alter the vertical spacing of the text field. Using `none` (default) doesn't apply margins to the `FormControl` whereas `dense` and `normal` do.

Press Enter to start editing

## [Full width](https://v6.mui.com/material-ui/all-components/#full-width)

`fullWidth` can be used to make the input take up the full width of its container.

Press Enter to start editing

## [Uncontrolled vs. Controlled](https://v6.mui.com/material-ui/all-components/#uncontrolled-vs-controlled)

The component can be controlled or uncontrolled.

Press Enter to start editing

## [Components](https://v6.mui.com/material-ui/all-components/#components)

`TextField` is composed of smaller components ( [`FormControl`](https://v6.mui.com/material-ui/api/form-control/), [`Input`](https://v6.mui.com/material-ui/api/input/), [`FilledInput`](https://v6.mui.com/material-ui/api/filled-input/), [`InputLabel`](https://v6.mui.com/material-ui/api/input-label/), [`OutlinedInput`](https://v6.mui.com/material-ui/api/outlined-input/), and [`FormHelperText`](https://v6.mui.com/material-ui/api/form-helper-text/) ) that you can leverage directly to significantly customize your form inputs.

You might also have noticed that some native HTML input properties are missing from the `TextField` component. This is on purpose. The component takes care of the most used properties. Then, it's up to the user to use the underlying component shown in the following demo. Still, you can use `slotProps.htmlInput` (and `slotProps.input`, `slotProps.inputLabel` properties) if you want to avoid some boilerplate.

## [Inputs](https://v6.mui.com/material-ui/all-components/#inputs)

Press Enter to start editing

## [Color](https://v6.mui.com/material-ui/all-components/#color)

The `color` prop changes the highlight color of the text field when focused.

Press Enter to start editing

## [Customization](https://v6.mui.com/material-ui/all-components/#customization)

Here are some examples of customizing the component. You can learn more about this in the [overrides documentation page](https://v6.mui.com/material-ui/customization/how-to-customize/).

### [Using the styled API](https://v6.mui.com/material-ui/all-components/#using-the-styled-api)

### [Using the theme style overrides API](https://v6.mui.com/material-ui/all-components/#using-the-theme-style-overrides-api)

Use the `styleOverrides` key to change any style injected by Material UI into the DOM. See the [theme style overrides](https://v6.mui.com/material-ui/customization/theme-components/#theme-style-overrides) documentation for further details.

Press Enter to start editing

Customization does not stop at CSS. You can use composition to build custom components and give your app a unique feel. Below is an example using the [`InputBase`](https://v6.mui.com/material-ui/api/input-base/) component, inspired by Google Maps.

🎨 If you are looking for inspiration, you can check [MUI Treasury's customization examples](https://mui-treasury.com/?path=/docs/textField-introduction--docs).

## [`useFormControl`](https://v6.mui.com/material-ui/all-components/#useformcontrol)

For advanced customization use cases, a `useFormControl()` hook is exposed. This hook returns the context value of the parent `FormControl` component.

**API**

```jsx
import { useFormControl } from '@mui/material/FormControl';
```

**Returns**

`value` (_object_):

-   `value.adornedStart` (_bool_): Indicate whether the child `Input` or `Select` component has a start adornment.
-   `value.setAdornedStart` (_func_): Setter function for `adornedStart` state value.
-   `value.color` (_string_): The theme color is being used, inherited from `FormControl` `color` prop .
-   `value.disabled` (_bool_): Indicate whether the component is being displayed in a disabled state, inherited from `FormControl` `disabled` prop.
-   `value.error` (_bool_): Indicate whether the component is being displayed in an error state, inherited from `FormControl` `error` prop
-   `value.filled` (_bool_): Indicate whether input is filled
-   `value.focused` (_bool_): Indicate whether the component and its children are being displayed in a focused state
-   `value.fullWidth` (_bool_): Indicate whether the component is taking up the full width of its container, inherited from `FormControl` `fullWidth` prop
-   `value.hiddenLabel` (_bool_): Indicate whether the label is being hidden, inherited from `FormControl` `hiddenLabel` prop
-   `value.required` (_bool_): Indicate whether the label is indicating that the input is required input, inherited from the `FormControl` `required` prop
-   `value.size` (_string_): The size of the component, inherited from the `FormControl` `size` prop
-   `value.variant` (_string_): The variant is being used by the `FormControl` component and its children, inherited from `FormControl` `variant` prop
-   `value.onBlur` (_func_): Should be called when the input is blurred
-   `value.onFocus` (_func_): Should be called when the input is focused
-   `value.onEmpty` (_func_): Should be called when the input is emptied
-   `value.onFilled` (_func_): Should be called when the input is filled

**Example**

Press Enter to start editing

## [Performance](https://v6.mui.com/material-ui/all-components/#performance)

Global styles for the auto-fill keyframes are injected and removed on each mount and unmount, respectively. If you are loading a large number of Text Field components at once, it might be a good idea to change this default behavior by enabling [`disableInjectingGlobalStyles`](https://v6.mui.com/material-ui/api/input-base/#input-base-prop-disableInjectingGlobalStyles) in `MuiInputBase`. Make sure to inject `GlobalStyles` for the auto-fill keyframes at the top of your application.

```jsx
import { GlobalStyles, createTheme, ThemeProvider } from '@mui/material'; const theme = createTheme({ components: { MuiInputBase: { defaultProps: { disableInjectingGlobalStyles: true, }, }, }, }); export default function App() { return ( <ThemeProvider theme={theme}> <GlobalStyles styles={{ '@keyframes mui-auto-fill': { from: { display: 'block' } }, '@keyframes mui-auto-fill-cancel': { from: { display: 'block' } }, }} /> ... </ThemeProvider> ); }
```

## [Limitations](https://v6.mui.com/material-ui/all-components/#limitations)

### [Shrink](https://v6.mui.com/material-ui/all-components/#shrink)

The input label "shrink" state isn't always correct. The input label is supposed to shrink as soon as the input is displaying something. In some circumstances, we can't determine the "shrink" state (number input, datetime input, Stripe input). You might notice an overlap.

![shrink](https://v6.mui.com/static/images/text-fields/shrink.png)

To workaround the issue, you can force the "shrink" state of the label.

```jsx
<TextField slotProps={{ inputLabel: { shrink: true } }} />
```

or

```jsx
<InputLabel shrink>Count</InputLabel>
```

### [Floating label](https://v6.mui.com/material-ui/all-components/#floating-label)

The floating label is absolutely positioned. It won't impact the layout of the page. Make sure that the input is larger than the label to display correctly.

### [type="number"](https://v6.mui.com/material-ui/all-components/#type-quot-number-quot)

If you need a text field with number validation, you can use MUI Base's [Number Input](https://v6.mui.com/base-ui/react-number-input/) instead.

You can follow [this GitHub issue](https://github.com/mui/material-ui/issues/19154) to track the progress of introducing the Number Input component to Material UI.

### [Helper text](https://v6.mui.com/material-ui/all-components/#helper-text)

The helper text prop affects the height of the text field. If two text fields are placed side by side, one with a helper text and one without, they will have different heights. For example:

Name

Please enter your name

Press Enter to start editing

This can be fixed by passing a space character to the `helperText` prop:

Name

Please enter your name

Press Enter to start editing

## [Integration with 3rd party input libraries](https://v6.mui.com/material-ui/all-components/#integration-with-3rd-party-input-libraries)

You can use third-party libraries to format an input. You have to provide a custom implementation of the `<input>` element with the `inputComponent` property.

The following demo uses the [react-imask](https://github.com/uNmAnNeR/imaskjs) and [react-number-format](https://github.com/s-yadav/react-number-format) libraries. The same concept could be applied to, for example [react-stripe-element](https://github.com/mui/material-ui/issues/16037).

The provided input component should expose a ref with a value that implements the following interface:

```ts
interface InputElement { focus(): void; value?: string; }
```

```jsx
const MyInputComponent = React.forwardRef((props, ref) => { const { component: Component, ...other } = props; // implement `InputElement` interface React.useImperativeHandle(ref, () => ({ focus: () => { // logic to focus the rendered component from 3rd party belongs here }, // hiding the value e.g. react-stripe-elements })); // `Component` will be your `SomeThirdPartyComponent` from below return <Component {...other} />; }); // usage <TextField slotProps={{ input: { inputComponent: MyInputComponent, inputProps: { component: SomeThirdPartyComponent, }, }, }} />;
```

## [Accessibility](https://v6.mui.com/material-ui/all-components/#accessibility)

In order for the text field to be accessible, **the input should be linked to the label and the helper text**. The underlying DOM nodes should have this structure:

```jsx
<div class="form-control"> <label for="my-input">Email address</label> <input id="my-input" aria-describedby="my-helper-text" /> <span id="my-helper-text">We'll never share your email.</span> </div>
```

-   If you are using the `TextField` component, you just have to provide a unique `id` unless you're using the `TextField` only client-side. Until the UI is hydrated `TextField` without an explicit `id` will not have associated labels.
-   If you are composing the component:

```jsx
<FormControl> <InputLabel htmlFor="my-input">Email address</InputLabel> <Input id="my-input" aria-describedby="my-helper-text" /> <FormHelperText id="my-helper-text">We'll never share your email.</FormHelperText> </FormControl>
```

## [Supplementary projects](https://v6.mui.com/material-ui/all-components/#supplementary-projects)

For more advanced use cases, you might be able to take advantage of:

-   [react-hook-form-mui](https://github.com/dohomi/react-hook-form-mui): Material UI and [react-hook-form](https://react-hook-form.com/) combined.
-   [formik-material-ui](https://github.com/stackworx/formik-mui): Bindings for using Material UI with [formik](https://formik.org/).
-   [mui-rff](https://github.com/lookfirst/mui-rff): Bindings for using Material UI with [React Final Form](https://final-form.org/react).
-   [@ui-schema/ds-material](https://www.npmjs.com/package/@ui-schema/ds-material) Bindings for using Material UI with [UI Schema](https://github.com/ui-schema/ui-schema). JSON Schema compatible.

## [Unstyled](https://v6.mui.com/material-ui/all-components/#unstyled)

Use the [Base UI Text Field](https://v6.mui.com/base-ui/react-input/) for complete ownership of the component's design, with no Material UI or Joy UI styles to override. This unstyled version of the component is the ideal choice for heavy customization with a smaller bundle size.

## [API](https://v6.mui.com/material-ui/all-components/#api)

See the documentation below for a complete reference to all of the props and classes available to the components mentioned here.

-   [`<FilledInput />`](https://v6.mui.com/material-ui/api/filled-input/)
-   [`<FormControl />`](https://v6.mui.com/material-ui/api/form-control/)
-   [`<FormHelperText />`](https://v6.mui.com/material-ui/api/form-helper-text/)
-   [`<Input />`](https://v6.mui.com/material-ui/api/input/)
-   [`<InputAdornment />`](https://v6.mui.com/material-ui/api/input-adornment/)
-   [`<InputBase />`](https://v6.mui.com/material-ui/api/input-base/)
-   [`<InputLabel />`](https://v6.mui.com/material-ui/api/input-label/)
-   [`<OutlinedInput />`](https://v6.mui.com/material-ui/api/outlined-input/)
-   [`<TextField />`](https://v6.mui.com/material-ui/api/text-field/)