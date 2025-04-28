The App Bar displays information and actions relating to the current screen.

The top App bar provides content and actions related to the current screen. It's used for branding, screen titles, navigation, and actions.

It can transform into a contextual action bar or be used as a navbar.

-   [Feedback](https://github.com/mui/material-ui/labels/component%3A%20app%20bar)
-   [Bundle size](https://bundlephobia.com/package/@mui/material@latest "Scroll down to 'Exports Analysis' for a more detailed report.")
-   [Source](https://github.com/mui/material-ui/tree/v6.4.11/packages/mui-material/src/AppBar)
-   [Material Design](https://m2.material.io/components/app-bars-top)
-   [Figma](https://mui.com/store/items/figma-react/?utm_source=docs&utm_medium=referral&utm_campaign=component-link-header)
-   [Sketch](https://mui.com/store/items/sketch-react/?utm_source=docs&utm_medium=referral&utm_campaign=component-link-header)

## [Basic App bar](https://v6.mui.com/material-ui/react-progress/#basic-app-bar)

## [App bar with menu](https://v6.mui.com/material-ui/react-progress/#app-bar-with-menu)

## [App bar with responsive menu](https://v6.mui.com/material-ui/react-progress/#app-bar-with-responsive-menu)

## [App bar with search field](https://v6.mui.com/material-ui/react-progress/#app-bar-with-search-field)

A side searchbar.

## [Responsive App bar with Drawer](https://v6.mui.com/material-ui/react-progress/#responsive-app-bar-with-drawer)

## [App bar with a primary search field](https://v6.mui.com/material-ui/react-progress/#app-bar-with-a-primary-search-field)

A primary searchbar.

## [Dense (desktop only)](https://v6.mui.com/material-ui/react-progress/#dense-desktop-only)

Press Enter to start editing

## [Prominent](https://v6.mui.com/material-ui/react-progress/#prominent)

A prominent app bar.

## [Bottom App bar](https://v6.mui.com/material-ui/react-progress/#bottom-app-bar)

## [Fixed placement](https://v6.mui.com/material-ui/react-progress/#fixed-placement)

When you render the app bar position fixed, the dimension of the element doesn't impact the rest of the page. This can cause some part of your content to be invisible, behind the app bar. Here are 3 possible solutions:

1.  You can use `position="sticky"` instead of fixed.
2.  You can render a second `<Toolbar />` component:

```jsx
function App() { return ( <React.Fragment> <AppBar position="fixed"> <Toolbar>{/* content */}</Toolbar> </AppBar> <Toolbar /> </React.Fragment> ); }
```

3.  You can use `theme.mixins.toolbar` CSS:

```jsx
const Offset = styled('div')(({ theme }) => theme.mixins.toolbar); function App() { return ( <React.Fragment> <AppBar position="fixed"> <Toolbar>{/* content */}</Toolbar> </AppBar> <Offset /> </React.Fragment> ); }
```

You can use the `useScrollTrigger()` hook to respond to user scroll actions.

### [Hide App bar](https://v6.mui.com/material-ui/react-progress/#hide-app-bar)

The app bar hides on scroll down to leave more space for reading.

### [Elevate App bar](https://v6.mui.com/material-ui/react-progress/#elevate-app-bar)

The app bar elevates on scroll to communicate that the user is not at the top of the page.

### [Back to top](https://v6.mui.com/material-ui/react-progress/#back-to-top)

A floating action button appears on scroll to make it easy to get back to the top of the page.

### [`useScrollTrigger([options]) => trigger`](https://v6.mui.com/material-ui/react-progress/#usescrolltrigger-options-trigger)

#### Arguments

1.  `options` (_object_ \[optional\]):
    
    -   `options.disableHysteresis` (_bool_ \[optional\]): Defaults to `false`. Disable the hysteresis. Ignore the scroll direction when determining the `trigger` value.
    -   `options.target` (_Node_ \[optional\]): Defaults to `window`.
    -   `options.threshold` (_number_ \[optional\]): Defaults to `100`. Change the `trigger` value when the vertical scroll strictly crosses this threshold (exclusive).

#### Returns

`trigger`: Does the scroll position match the criteria?

#### Examples

```jsx
import useScrollTrigger from '@mui/material/useScrollTrigger'; function HideOnScroll(props) { const trigger = useScrollTrigger(); return ( <Slide in={!trigger}> <div>Hello</div> </Slide> ); }
```

## [Enable color on dark](https://v6.mui.com/material-ui/react-progress/#enable-color-on-dark)

Following the [Material Design guidelines](https://m2.material.io/design/color/dark-theme.html), the `color` prop has no effect on the appearance of the app bar in dark mode. You can override this behavior by setting the `enableColorOnDark` prop to `true`.

Press Enter to start editing

### [Dashboard Layout](https://v6.mui.com/material-ui/react-progress/#dashboard-layout)

The [DashboardLayout](https://mui.com/toolpad/core/react-dashboard-layout/) component from `@toolpad/core` is the starting point for dashboarding applications. It takes care of application layout, theming, navigation, and more. An example usage of this component:

## [API](https://v6.mui.com/material-ui/react-progress/#api)

See the documentation below for a complete reference to all of the props and classes available to the components mentioned here.

-   [`<AppBar />`](https://v6.mui.com/material-ui/api/app-bar/)
-   [`<Menu />`](https://v6.mui.com/material-ui/api/menu/)
-   [`<Toolbar />`](https://v6.mui.com/material-ui/api/toolbar/)