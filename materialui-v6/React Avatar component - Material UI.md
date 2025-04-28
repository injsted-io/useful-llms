Avatars are found throughout material design with uses in everything from tables to dialog menus.

-   [Feedback](https://github.com/mui/material-ui/labels/component%3A%20avatar)
-   [Bundle size](https://bundlephobia.com/package/@mui/material@latest "Scroll down to 'Exports Analysis' for a more detailed report.")
-   [Source](https://github.com/mui/material-ui/tree/v6.4.11/packages/mui-material/src/Avatar)
-   [Figma](https://mui.com/store/items/figma-react/?utm_source=docs&utm_medium=referral&utm_campaign=component-link-header)
-   [Sketch](https://mui.com/store/items/sketch-react/?utm_source=docs&utm_medium=referral&utm_campaign=component-link-header)

## [Image avatars](https://v6.mui.com/material-ui/all-components/#image-avatars)

Image avatars can be created by passing standard `img` props `src` or `srcSet` to the component.

Press Enter to start editing

## [Letter avatars](https://v6.mui.com/material-ui/all-components/#letter-avatars)

Avatars containing simple characters can be created by passing a string as `children`.

Press Enter to start editing

You can use different background colors for the avatar. The following demo generates the color based on the name of the person.

Press Enter to start editing

## [Sizes](https://v6.mui.com/material-ui/all-components/#sizes)

You can change the size of the avatar with the `height` and `width` CSS properties.

Press Enter to start editing

## [Icon avatars](https://v6.mui.com/material-ui/all-components/#icon-avatars)

Icon avatars are created by passing an icon as `children`.

Press Enter to start editing

## [Variants](https://v6.mui.com/material-ui/all-components/#variants)

If you need square or rounded avatars, use the `variant` prop.

Press Enter to start editing

## [Fallbacks](https://v6.mui.com/material-ui/all-components/#fallbacks)

If there is an error loading the avatar image, the component falls back to an alternative in the following order:

-   the provided children
-   the first letter of the `alt` text
-   a generic avatar icon

Press Enter to start editing

## [Grouped](https://v6.mui.com/material-ui/all-components/#grouped)

`AvatarGroup` renders its children as a stack. Use the `max` prop to limit the number of avatars.

Press Enter to start editing

### [Total avatars](https://v6.mui.com/material-ui/all-components/#total-avatars)

If you need to control the total number of avatars not shown, you can use the `total` prop.

Press Enter to start editing

### [Custom surplus](https://v6.mui.com/material-ui/all-components/#custom-surplus)

Set the `renderSurplus` prop as a callback to customize the surplus avatar. The callback will receive the surplus number as an argument based on the children and the `max` prop, and should return a `React.ReactNode`.

The `renderSurplus` prop is useful when you need to render the surplus based on the data sent from the server.

Press Enter to start editing

### [Spacing](https://v6.mui.com/material-ui/all-components/#spacing)

You can change the spacing between avatars using the `spacing` prop. You can use one of the presets (`"medium"`, the default, or `"small"`) or set a custom numeric value.

Press Enter to start editing

## [With badge](https://v6.mui.com/material-ui/all-components/#with-badge)

Press Enter to start editing

## [API](https://v6.mui.com/material-ui/all-components/#api)

See the documentation below for a complete reference to all of the props and classes available to the components mentioned here.

-   [`<Avatar />`](https://v6.mui.com/material-ui/api/avatar/)
-   [`<AvatarGroup />`](https://v6.mui.com/material-ui/api/avatar-group/)
-   [`<Badge />`](https://v6.mui.com/material-ui/api/badge/)