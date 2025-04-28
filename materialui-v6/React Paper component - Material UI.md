The Paper component is a container for displaying content on an elevated surface.

-   [Feedback](https://github.com/mui/material-ui/labels/component%3A%20Paper)
-   [Bundle size](https://bundlephobia.com/package/@mui/material@latest "Scroll down to 'Exports Analysis' for a more detailed report.")
-   [Source](https://github.com/mui/material-ui/tree/v6.4.11/packages/mui-material/src/Paper)
-   [Material Design](https://m2.material.io/design/environment/elevation.html)
-   [Figma](https://mui.com/store/items/figma-react/?utm_source=docs&utm_medium=referral&utm_campaign=component-link-header)
-   [Sketch](https://mui.com/store/items/sketch-react/?utm_source=docs&utm_medium=referral&utm_campaign=component-link-header)

## [Introduction](https://v6.mui.com/material-ui/react-card/#introduction)

In Material Design, surface components and shadow styles are heavily influenced by their real-world physical counterparts.

Material UI implements this concept with the Paper component, a container-like surface that features the [`elevation`](https://v6.mui.com/material-ui/react-card/#elevation) prop for pulling box-shadow values from the theme.

Press Enter to start editing

## [Component](https://v6.mui.com/material-ui/react-card/#component)

```jsx
import Paper from '@mui/material/Paper';
```

## [Customization](https://v6.mui.com/material-ui/react-card/#customization)

### [Elevation](https://v6.mui.com/material-ui/react-card/#elevation)

Use the `elevation` prop to establish hierarchy through the use of shadows. The Paper component's default elevation level is `1`. The prop accepts values from `0` to `24`. The higher the number, the further away the Paper appears to be from its background.

In dark mode, increasing the elevation also makes the background color lighter. This is done by applying a semi-transparent gradient with the `background-image` CSS property.

elevation=0

elevation=1

elevation=2

elevation=3

elevation=4

elevation=6

elevation=8

elevation=12

elevation=16

elevation=24

elevation=0

elevation=1

elevation=2

elevation=3

elevation=4

elevation=6

elevation=8

elevation=12

elevation=16

elevation=24

### [Variants](https://v6.mui.com/material-ui/react-card/#variants)

Set the `variant` prop to `"outlined"` for a flat, outlined Paper with no shadows:

default variant

outlined variant

Press Enter to start editing

### [Corners](https://v6.mui.com/material-ui/react-card/#corners)

The Paper component features rounded corners by default. Add the `square` prop for square corners:

rounded corners

square corners

Press Enter to start editing

## [Anatomy](https://v6.mui.com/material-ui/react-card/#anatomy)

The Paper component is composed of a single root `<div>` that wraps around its contents:

```html
<div class="MuiPaper-root"> <!-- Paper contents --> </div>
```

## [API](https://v6.mui.com/material-ui/react-card/#api)

See the documentation below for a complete reference to all of the props and classes available to the components mentioned here.

-   [`<Paper />`](https://v6.mui.com/material-ui/api/paper/)