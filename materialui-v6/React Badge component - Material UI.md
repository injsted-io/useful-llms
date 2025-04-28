Badge generates a small badge to the top-right of its child(ren).

-   [Feedback](https://github.com/mui/material-ui/labels/component%3A%20badge)
-   [Bundle size](https://bundlephobia.com/package/@mui/material@latest "Scroll down to 'Exports Analysis' for a more detailed report.")
-   [Source](https://github.com/mui/material-ui/tree/v6.4.11/packages/mui-material/src/Badge)
-   [Figma](https://mui.com/store/items/figma-react/?utm_source=docs&utm_medium=referral&utm_campaign=component-link-header)
-   [Sketch](https://mui.com/store/items/sketch-react/?utm_source=docs&utm_medium=referral&utm_campaign=component-link-header)

## [Basic badge](https://v6.mui.com/material-ui/all-components/#basic-badge)

Examples of badges containing text, using primary and secondary colors. The badge is applied to its children.

4

Press Enter to start editing

## [Color](https://v6.mui.com/material-ui/all-components/#color)

Use `color` prop to apply theme palette to component.

Press Enter to start editing

Press Enter to start editing

## [Badge visibility](https://v6.mui.com/material-ui/all-components/#badge-visibility)

The visibility of badges can be controlled using the `invisible` prop.

The badge hides automatically when `badgeContent` is zero. You can override this with the `showZero` prop.

Press Enter to start editing

## [Maximum value](https://v6.mui.com/material-ui/all-components/#maximum-value)

You can use the `max` prop to cap the value of the badge content.

Press Enter to start editing

## [Dot badge](https://v6.mui.com/material-ui/all-components/#dot-badge)

The `dot` prop changes a badge into a small dot. This can be used as a notification that something has changed without giving a count.

Press Enter to start editing

## [Badge overlap](https://v6.mui.com/material-ui/all-components/#badge-overlap)

You can use the `overlap` prop to place the badge relative to the corner of the wrapped element.

Press Enter to start editing

## [Badge alignment](https://v6.mui.com/material-ui/all-components/#badge-alignment)

You can use the `anchorOrigin` prop to move the badge to any corner of the wrapped element.

11299+999+

```jsx
<Badge anchorOrigin={{ vertical: 'top', horizontal: 'right', }} >
```

## [Accessibility](https://v6.mui.com/material-ui/all-components/#accessibility)

You can't rely on the content of the badge to be announced correctly. You should provide a full description, for instance, with `aria-label`:

Press Enter to start editing

## [Unstyled](https://v6.mui.com/material-ui/all-components/#unstyled)

Use the [Base UI Badge](https://v6.mui.com/base-ui/react-badge/) for complete ownership of the component's design, with no Material UI or Joy UI styles to override. This unstyled version of the component is the ideal choice for heavy customization with a smaller bundle size.

## [API](https://v6.mui.com/material-ui/all-components/#api)

See the documentation below for a complete reference to all of the props and classes available to the components mentioned here.

-   [`<Badge />`](https://v6.mui.com/material-ui/api/badge/)