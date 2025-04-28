Buttons allow users to take actions, and make choices, with a single tap.

Buttons communicate actions that users can take. They are typically placed throughout your UI, in places like:

-   Modal windows
-   Forms
-   Cards
-   Toolbars

-   [Feedback](https://github.com/mui/material-ui/labels/component%3A%20button)
-   [Bundle size](https://bundlephobia.com/package/@mui/material@latest "Scroll down to 'Exports Analysis' for a more detailed report.")
-   [Source](https://github.com/mui/material-ui/tree/v6.4.11/packages/mui-material/src/Button)
-   [WAI-ARIA](https://www.w3.org/WAI/ARIA/apg/patterns/button/)
-   [Material Design](https://m2.material.io/components/buttons)
-   [Figma](https://mui.com/store/items/figma-react/?utm_source=docs&utm_medium=referral&utm_campaign=component-link-header)
-   [Sketch](https://mui.com/store/items/sketch-react/?utm_source=docs&utm_medium=referral&utm_campaign=component-link-header)

## [Basic button](https://v6.mui.com/material-ui/all-components/#basic-button)

The `Button` comes with three variants: text (default), contained, and outlined.

Press Enter to start editing

### [Text button](https://v6.mui.com/material-ui/all-components/#text-button)

[Text buttons](https://m2.material.io/components/buttons#text-button) are typically used for less-pronounced actions, including those located: in dialogs, in cards. In cards, text buttons help maintain an emphasis on card content.

Press Enter to start editing

### [Contained button](https://v6.mui.com/material-ui/all-components/#contained-button)

[Contained buttons](https://m2.material.io/components/buttons#contained-button) are high-emphasis, distinguished by their use of elevation and fill. They contain actions that are primary to your app.

Press Enter to start editing

You can remove the elevation with the `disableElevation` prop.

Press Enter to start editing

### [Outlined button](https://v6.mui.com/material-ui/all-components/#outlined-button)

[Outlined buttons](https://m2.material.io/components/buttons#outlined-button) are medium-emphasis buttons. They contain actions that are important but aren't the primary action in an app.

Outlined buttons are also a lower emphasis alternative to contained buttons, or a higher emphasis alternative to text buttons.

Press Enter to start editing

## [Handling clicks](https://v6.mui.com/material-ui/all-components/#handling-clicks)

All components accept an `onClick` handler that is applied to the root DOM element.

```jsx
<Button onClick={() => { alert('clicked'); }} > Click me </Button>
```

Note that the documentation [avoids](https://v6.mui.com/material-ui/guides/api/#native-properties) mentioning native props (there are a lot) in the API section of the components.

## [Color](https://v6.mui.com/material-ui/all-components/#color)

Press Enter to start editing

In addition to using the default button colors, you can add custom ones, or disable any you don't need. See the [Adding new colors](https://v6.mui.com/material-ui/customization/palette/#custom-colors) examples for more info.

## [Sizes](https://v6.mui.com/material-ui/all-components/#sizes)

For larger or smaller buttons, use the `size` prop.

## [Buttons with icons and label](https://v6.mui.com/material-ui/all-components/#buttons-with-icons-and-label)

Sometimes you might want to have icons for certain buttons to enhance the UX of the application as we recognize logos more easily than plain text. For example, if you have a delete button you can label it with a dustbin icon.

Press Enter to start editing

## [Icon button](https://v6.mui.com/material-ui/all-components/#icon-button)

Icon buttons are commonly found in app bars and toolbars.

Icons are also appropriate for toggle buttons that allow a single choice to be selected or deselected, such as adding or removing a star to an item.

Press Enter to start editing

### [Sizes](https://v6.mui.com/material-ui/all-components/#sizes-2)

For larger or smaller icon buttons, use the `size` prop.

Press Enter to start editing

### [Colors](https://v6.mui.com/material-ui/all-components/#colors)

Use `color` prop to apply theme color palette to component.

Press Enter to start editing

### [Loading](https://v6.mui.com/material-ui/all-components/#loading)

Starting from v6.4.0, use `loading` prop to set icon buttons in a loading state and disable interactions.

Press Enter to start editing

### [Badge](https://v6.mui.com/material-ui/all-components/#badge)

You can use the [`Badge`](https://v6.mui.com/material-ui/react-badge/) component to add a badge to an `IconButton`.

Press Enter to start editing

## [File upload](https://v6.mui.com/material-ui/all-components/#file-upload)

To create a file upload button, turn the button into a label using `component="label"` and then create a visually-hidden input with type `file`.

Upload files

Press Enter to start editing

## [Loading](https://v6.mui.com/material-ui/all-components/#loading-2)

Starting from v6.4.0, use the `loading` prop to set buttons in a loading state and disable interactions.

Toggle the loading switch to see the transition between the different states.

## [Customization](https://v6.mui.com/material-ui/all-components/#customization)

Here are some examples of customizing the component. You can learn more about this in the [overrides documentation page](https://v6.mui.com/material-ui/customization/how-to-customize/).

🎨 If you are looking for inspiration, you can check [MUI Treasury's customization examples](https://mui-treasury.com/?path=/docs/button-introduction--docs).

## [Complex button](https://v6.mui.com/material-ui/all-components/#complex-button)

The Text Buttons, Contained Buttons, Floating Action Buttons and Icon Buttons are built on top of the same component: the `ButtonBase`. You can take advantage of this lower-level component to build custom interactions.

## [Third-party routing library](https://v6.mui.com/material-ui/all-components/#third-party-routing-library)

One frequent use case is to perform navigation on the client only, without an HTTP round-trip to the server. The `ButtonBase` component provides the `component` prop to handle this use case. Here is a [more detailed guide](https://v6.mui.com/material-ui/integrations/routing/#button).

## [Limitations](https://v6.mui.com/material-ui/all-components/#limitations)

### [Cursor not-allowed](https://v6.mui.com/material-ui/all-components/#cursor-not-allowed)

The ButtonBase component sets `pointer-events: none;` on disabled buttons, which prevents the appearance of a disabled cursor.

If you wish to use `not-allowed`, you have two options:

1.  **CSS only**. You can remove the pointer-events style on the disabled state of the `<button>` element:

```css
.MuiButtonBase-root:disabled { cursor: not-allowed; pointer-events: auto; }
```

However:

-   You should add `pointer-events: none;` back when you need to display [tooltips on disabled elements](https://v6.mui.com/material-ui/react-tooltip/#disabled-elements).
-   The cursor won't change if you render something other than a button element, for instance, a link `<a>` element.

2.  **DOM change**. You can wrap the button:

```jsx
<span style={{ cursor: 'not-allowed' }}> <Button component={Link} disabled> disabled </Button> </span>
```

This has the advantage of supporting any element, for instance, a link `<a>` element.

## [Unstyled](https://v6.mui.com/material-ui/all-components/#unstyled)

Use the [Base UI Button](https://v6.mui.com/base-ui/react-button/) for complete ownership of the component's design, with no Material UI or Joy UI styles to override. This unstyled version of the component is the ideal choice for heavy customization with a smaller bundle size.

## [API](https://v6.mui.com/material-ui/all-components/#api)

See the documentation below for a complete reference to all of the props and classes available to the components mentioned here.

-   [`<Button />`](https://v6.mui.com/material-ui/api/button/)
-   [`<ButtonBase />`](https://v6.mui.com/material-ui/api/button-base/)
-   [`<IconButton />`](https://v6.mui.com/material-ui/api/icon-button/)