The navigation drawers (or "sidebars") provide ergonomic access to destinations in a site or app functionality such as switching accounts.

A navigation drawer can either be permanently on-screen or controlled by a navigation menu icon.

[Side sheets](https://m2.material.io/components/sheets-side) are supplementary surfaces primarily used on tablet and desktop.

-   [Feedback](https://github.com/mui/material-ui/labels/component%3A%20drawer)
-   [Bundle size](https://bundlephobia.com/package/@mui/material@latest "Scroll down to 'Exports Analysis' for a more detailed report.")
-   [Source](https://github.com/mui/material-ui/tree/v6.4.11/packages/mui-material/src/Drawer)
-   [Material Design](https://m2.material.io/components/navigation-drawer)
-   [Figma](https://mui.com/store/items/figma-react/?utm_source=docs&utm_medium=referral&utm_campaign=component-link-header)
-   [Sketch](https://mui.com/store/items/sketch-react/?utm_source=docs&utm_medium=referral&utm_campaign=component-link-header)

## [Temporary drawer](https://v6.mui.com/material-ui/react-card/#temporary-drawer)

Temporary navigation drawers can toggle open or closed. Closed by default, the drawer opens temporarily above all other content until a section is selected.

The Drawer can be cancelled by clicking the overlay or pressing the Esc key. It closes when an item is selected, handled by controlling the `open` prop.

Press Enter to start editing

### [Anchor](https://v6.mui.com/material-ui/react-card/#anchor)

Use the `anchor` prop to specify which side of the screen the Drawer should originate from.

The default value is `left`.

Press Enter to start editing

### [Swipeable](https://v6.mui.com/material-ui/react-card/#swipeable)

You can make the drawer swipeable with the `SwipeableDrawer` component.

This component comes with a 2 kB gzipped payload overhead. Some low-end mobile devices won't be able to follow the fingers at 60 FPS. You can use the `disableBackdropTransition` prop to help.

Press Enter to start editing

The following properties are used in this documentation website for optimal usability of the component:

-   iOS is hosted on high-end devices. The backdrop transition can be enabled without dropping frames. The performance will be good enough.
-   iOS has a "swipe to go back" feature that interferes with the discovery feature, so discovery has to be disabled.

```jsx
const iOS = typeof navigator !== 'undefined' && /iPad|iPhone|iPod/.test(navigator.userAgent); <SwipeableDrawer disableBackdropTransition={!iOS} disableDiscovery={iOS} />;
```

### [Swipeable edge](https://v6.mui.com/material-ui/react-card/#swipeable-edge)

You can configure the `SwipeableDrawer` to have a visible edge when closed.

If you are on a desktop, you can toggle the drawer with the "OPEN" button. If you are on mobile, you can open the demo in CodeSandbox ("edit" icon) and swipe.

### [Keep mounted](https://v6.mui.com/material-ui/react-card/#keep-mounted)

The Modal used internally by the Swipeable Drawer has the `keepMounted` prop set by default. This means that the contents of the drawer are always present in the DOM.

You can change this default behavior with the `ModalProps` prop, but you may encounter issues with `keepMounted: false` in React 18.

```jsx
<Drawer variant="temporary" ModalProps={{ keepMounted: false, }} />
```

## [Responsive drawer](https://v6.mui.com/material-ui/react-card/#responsive-drawer)

You can use the `temporary` variant to display a drawer for small screens and `permanent` for a drawer for wider screens.

## [Persistent drawer](https://v6.mui.com/material-ui/react-card/#persistent-drawer)

Persistent navigation drawers can toggle open or closed. The drawer sits on the same surface elevation as the content. It is closed by default and opens by selecting the menu icon, and stays open until closed by the user. The state of the drawer is remembered from action to action and session to session.

When the drawer is outside of the page grid and opens, the drawer forces other content to change size and adapt to the smaller viewport.

Persistent navigation drawers are acceptable for all sizes larger than mobile. They are not recommended for apps with multiple levels of hierarchy that require using an up arrow for navigation.

## [Mini variant drawer](https://v6.mui.com/material-ui/react-card/#mini-variant-drawer)

In this variation, the persistent navigation drawer changes its width. Its resting state is as a mini-drawer at the same elevation as the content, clipped by the app bar. When expanded, it appears as the standard persistent navigation drawer.

The mini variant is recommended for apps sections that need quick selection access alongside content.

## [Permanent drawer](https://v6.mui.com/material-ui/react-card/#permanent-drawer)

Permanent navigation drawers are always visible and pinned to the left edge, at the same elevation as the content or background. They cannot be closed.

Permanent navigation drawers are the **recommended default for desktop**.

### [Full-height navigation](https://v6.mui.com/material-ui/react-card/#full-height-navigation)

Apps focused on information consumption that use a left-to-right hierarchy.

### [Clipped under the app bar](https://v6.mui.com/material-ui/react-card/#clipped-under-the-app-bar)

Apps focused on productivity that require balance across the screen.

### [Dashboard Layout](https://v6.mui.com/material-ui/react-card/#dashboard-layout)

The [DashboardLayout](https://mui.com/toolpad/core/react-dashboard-layout/) component from `@toolpad/core` is the starting point for dashboarding applications. It takes care of application layout, theming, navigation, and more. An example usage of this component:

## [API](https://v6.mui.com/material-ui/react-card/#api)

See the documentation below for a complete reference to all of the props and classes available to the components mentioned here.

-   [`<Drawer />`](https://v6.mui.com/material-ui/api/drawer/)
-   [`<SwipeableDrawer />`](https://v6.mui.com/material-ui/api/swipeable-drawer/)