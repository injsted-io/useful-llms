The Divider component provides a thin, unobtrusive line for grouping elements to reinforce visual hierarchy.

-   [Feedback](https://github.com/mui/material-ui/labels/component%3A%20divider)
-   [Bundle size](https://bundlephobia.com/package/@mui/material@latest "Scroll down to 'Exports Analysis' for a more detailed report.")
-   [Source](https://github.com/mui/material-ui/tree/v6.4.11/packages/mui-material/src/Divider)
-   [Material Design](https://m2.material.io/components/dividers)
-   [Figma](https://mui.com/store/items/figma-react/?utm_source=docs&utm_medium=referral&utm_campaign=component-link-header)
-   [Sketch](https://mui.com/store/items/sketch-react/?utm_source=docs&utm_medium=referral&utm_campaign=component-link-header)

## [Introduction](https://v6.mui.com/material-ui/all-components/#introduction)

The Material UI Divider component renders as a dark gray `<hr>` by default, and features several useful props for quick style adjustments.

Pinstriped cornflower blue cotton blouse takes you on a walk to the park or just down the hall.

___

## [Basics](https://v6.mui.com/material-ui/all-components/#basics)

```jsx
import Divider from '@mui/material/Divider';
```

### [Variants](https://v6.mui.com/material-ui/all-components/#variants)

The Divider component supports three variants: `fullWidth` (default), `inset`, and `middle`.

-   Full width variant below
    

-   Inset variant below
    

-   Middle variant below
    

-   List item
    

### [Orientation](https://v6.mui.com/material-ui/all-components/#orientation)

Use the `orientation` prop to change the Divider from horizontal to vertical. When using vertical orientation, the Divider renders a `<div>` with the corresponding accessibility attributes instead of `<hr>` to adhere to the WAI-ARIA [spec](https://www.w3.org/TR/wai-aria-1.2/#separator).

Press Enter to start editing

### [Flex item](https://v6.mui.com/material-ui/all-components/#flex-item)

Use the `flexItem` prop to display the Divider when it's being used in a flex container.

Press Enter to start editing

### [With children](https://v6.mui.com/material-ui/all-components/#with-children)

Use the `textAlign` prop to align elements that are wrapped by the Divider.

Lorem ipsum dolor sit amet, consectetur adipiscing elit.

CENTER

Lorem ipsum dolor sit amet, consectetur adipiscing elit.

LEFT

Lorem ipsum dolor sit amet, consectetur adipiscing elit.

RIGHT

Lorem ipsum dolor sit amet, consectetur adipiscing elit.

Chip

Lorem ipsum dolor sit amet, consectetur adipiscing elit.

Press Enter to start editing

## [Customization](https://v6.mui.com/material-ui/all-components/#customization)

### [Use with a List](https://v6.mui.com/material-ui/all-components/#use-with-a-list)

When using the Divider to separate items in a List, use the `component` prop to render it as an `<li>`—otherwise it won't be a valid HTML element.

-   Inbox
    

-   Drafts
    

-   Trash
    

-   Spam
    

### [Icon grouping](https://v6.mui.com/material-ui/all-components/#icon-grouping)

The demo below shows how to combine the props `variant="middle"` and `orientation="vertical"`.

## [Accessibility](https://v6.mui.com/material-ui/all-components/#accessibility)

Due to its implicit role of `separator`, the Divider, which is a `<hr>` element, will be announced by screen readers as a "Horziontal Splitter" (or vertical, if you're using the `orientation` prop).

If you're using it as a purely stylistic element, we recommend setting `aria-hidden="true"` which will make screen readers bypass it.

```js
<Divider aria-hidden="true" />
```

If you're using the Divider to wrap other elements, such as text or chips, we recommend changing its rendered element to a plain `<div>` using the `component` prop, and setting `role="presentation"`. This ensures that it's not announced by screen readers while still preserving the semantics of the elements inside it.

```js
<Divider component="div" role="presentation"> <Typography>Text element</Typography> </Divider>
```

## [Anatomy](https://v6.mui.com/material-ui/all-components/#anatomy)

The Divider component is composed of a root `<hr>`.

```html
<hr class="MuiDivider-root"> <!-- Divider children goes here --> </hr>
```

## [API](https://v6.mui.com/material-ui/all-components/#api)

See the documentation below for a complete reference to all of the props and classes available to the components mentioned here.

-   [`<Divider />`](https://v6.mui.com/material-ui/api/divider/)