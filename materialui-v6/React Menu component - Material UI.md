Menus display a list of choices on temporary surfaces.

A menu displays a list of choices on a temporary surface. It appears when the user interacts with a button, or other control.

-   [Feedback](https://github.com/mui/material-ui/labels/component%3A%20menu)
-   [Bundle size](https://bundlephobia.com/package/@mui/material@latest "Scroll down to 'Exports Analysis' for a more detailed report.")
-   [Source](https://github.com/mui/material-ui/tree/v6.4.11/packages/mui-material/src/Menu)
-   [WAI-ARIA](https://www.w3.org/WAI/ARIA/apg/patterns/menu-button/)
-   [Material Design](https://m2.material.io/components/menus)
-   [Figma](https://mui.com/store/items/figma-react/?utm_source=docs&utm_medium=referral&utm_campaign=component-link-header)
-   [Sketch](https://mui.com/store/items/sketch-react/?utm_source=docs&utm_medium=referral&utm_campaign=component-link-header)

## [Introduction](https://v6.mui.com/material-ui/react-menu/#introduction)

Menus are implemented using a collection of related components:

-   Menu: The container/surface of the menu.
-   Menu Item: An option for users to select from the menu.
-   Menu List (optional): Alternative composable container for Menu Items—see [Composition with Menu List](https://v6.mui.com/material-ui/react-menu/#composition-with-menu-list) for details.

A basic menu opens over the anchor element by default (this option can be [changed](https://v6.mui.com/material-ui/react-menu/#menu-positioning) via props). When close to a screen edge, a basic menu vertically realigns to make sure that all menu items are completely visible.

You should configure the component so that selecting an option immediately confirms it and closes the menu, as shown in the demo below.

In desktop viewport, padding is increased to give more space to the menu.

For the menu that has long list and long text, you can use the `dense` prop to reduce the padding and text size.

If used for item selection, when opened, simple menus places the initial focus on the selected menu item. The currently selected menu item is set using the `selected` prop (from [ListItem](https://v6.mui.com/material-ui/api/list-item/)). To use a selected menu item without impacting the initial focus, set the `variant` prop to "menu".

When device is locked

Show all notification content

Because the `Menu` component uses the `Popover` component to position itself, you can use the same [positioning props](https://v6.mui.com/material-ui/react-popover/#anchor-playground) to position it. For instance, you can display the menu on top of the anchor:

The Menu component uses the Popover component internally. But you might want to use a different positioning strategy, or prefer not to block scrolling, for example.

The Menu List component lets you compose your own menu for these kinds of use cases—its primary purpose is to handle focus. See the demo below for an example of composition that uses Menu List and replaces the Menu's default Popover with a Popper component instead:

`Menu` content can be mixed with other components like `Avatar`.

## [Customization](https://v6.mui.com/material-ui/react-menu/#customization)

Here is an example of customizing the component. You can learn more about this in the [overrides documentation page](https://v6.mui.com/material-ui/customization/how-to-customize/).

The `MenuItem` is a wrapper around `ListItem` with some additional styles. You can use the same list composition features with the `MenuItem` component:

🎨 If you are looking for inspiration, you can check [MUI Treasury's customization examples](https://mui-treasury.com/?path=/docs/menu-introduction--docs).

If the height of a menu prevents all menu items from being displayed, the menu can scroll internally.

## [Limitations](https://v6.mui.com/material-ui/react-menu/#limitations)

There is [a flexbox bug](https://issues.chromium.org/issues/40344463) that prevents `text-overflow: ellipsis` from working in a flexbox layout. You can use the `Typography` component with `noWrap` to workaround this issue:

## [Change transition](https://v6.mui.com/material-ui/react-menu/#change-transition)

Use a different transition.

Here is an example of a context menu. (Right click to open.)

Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nullam ipsum purus, bibendum sit amet vulputate eget, porta semper ligula. Donec bibendum vulputate erat, ac fringilla mi finibus nec. Donec ac dolor sed dolor porttitor blandit vel vel purus. Fusce vel malesuada ligula. Nam quis vehicula ante, eu finibus est. Proin ullamcorper fermentum orci, quis finibus massa. Nunc lobortis, massa ut rutrum ultrices, metus metus finibus ex, sit amet facilisis neque enim sed neque. Quisque accumsan metus vel maximus consequat. Suspendisse lacinia tellus a libero volutpat maximus.

Display categories with the `ListSubheader` component.

## [Supplementary projects](https://v6.mui.com/material-ui/react-menu/#supplementary-projects)

For more advanced use cases you might be able to take advantage of:

![stars](https://img.shields.io/github/stars/jcoreio/material-ui-popup-state?style=social&label=Star) ![npm downloads](https://img.shields.io/npm/dm/material-ui-popup-state.svg)

The package [`material-ui-popup-state`](https://github.com/jcoreio/material-ui-popup-state) that takes care of menu state for you in most cases.

Press Enter to start editing

## [Unstyled](https://v6.mui.com/material-ui/react-menu/#unstyled)

Use the [Base UI Menu](https://v6.mui.com/base-ui/react-menu/) for complete ownership of the component's design, with no Material UI or Joy UI styles to override. This unstyled version of the component is the ideal choice for heavy customization with a smaller bundle size.

## [API](https://v6.mui.com/material-ui/react-menu/#api)

See the documentation below for a complete reference to all of the props and classes available to the components mentioned here.

-   [`<ClickAwayListener />`](https://v6.mui.com/base-ui/react-click-away-listener/components-api/#click-away-listener)
-   [`<Menu />`](https://v6.mui.com/material-ui/api/menu/)
-   [`<MenuItem />`](https://v6.mui.com/material-ui/api/menu-item/)
-   [`<MenuList />`](https://v6.mui.com/material-ui/api/menu-list/)
-   [`<Popover />`](https://v6.mui.com/material-ui/api/popover/)
-   [`<Popper />`](https://v6.mui.com/material-ui/api/popper/)