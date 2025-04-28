Tabs make it easy to explore and switch between different views.

Tabs organize and allow navigation between groups of content that are related and at the same level of hierarchy.

-   [Feedback](https://github.com/mui/material-ui/labels/component%3A%20tabs)
-   [Bundle size](https://bundlephobia.com/package/@mui/material@latest "Scroll down to 'Exports Analysis' for a more detailed report.")
-   [Source](https://github.com/mui/material-ui/tree/v6.4.11/packages/mui-material/src/Tabs)
-   [WAI-ARIA](https://www.w3.org/WAI/ARIA/apg/patterns/tabs/)
-   [Material Design](https://m2.material.io/components/tabs)
-   [Figma](https://mui.com/store/items/figma-react/?utm_source=docs&utm_medium=referral&utm_campaign=component-link-header)
-   [Sketch](https://mui.com/store/items/sketch-react/?utm_source=docs&utm_medium=referral&utm_campaign=component-link-header)

## [Introduction](https://v6.mui.com/material-ui/react-menu/#introduction)

Tabs are implemented using a collection of related components:

-   `<Tab />` - the tab element itself. Clicking on a tab displays its corresponding panel.
-   `<Tabs />` - the container that houses the tabs. Responsible for handling focus and keyboard navigation between tabs.

Press Enter to start editing

## [Basics](https://v6.mui.com/material-ui/react-menu/#basics)

```jsx
import Tabs from '@mui/material/Tabs'; import Tab from '@mui/material/Tab';
```

## [Experimental API](https://v6.mui.com/material-ui/react-menu/#experimental-api)

`@mui/lab` offers utility components that inject props to implement accessible tabs following [WAI-ARIA Authoring Practices](https://www.w3.org/WAI/ARIA/apg/patterns/tabs/):

-   `<TabList />` - the container that houses the tabs. Responsible for handling focus and keyboard navigation between tabs.
-   `<TabPanel />` - the card that hosts the content associated with a tab.
-   `<TabContext />` - the top-level component that wraps the Tab List and Tab Panel components.

Press Enter to start editing

## [Wrapped labels](https://v6.mui.com/material-ui/react-menu/#wrapped-labels)

Long labels will automatically wrap on tabs. If the label is too long for the tab, it will overflow, and the text will not be visible.

Press Enter to start editing

## [Colored tab](https://v6.mui.com/material-ui/react-menu/#colored-tab)

Press Enter to start editing

## [Disabled tab](https://v6.mui.com/material-ui/react-menu/#disabled-tab)

A tab can be disabled by setting the `disabled` prop.

Press Enter to start editing

## [Fixed tabs](https://v6.mui.com/material-ui/react-menu/#fixed-tabs)

Fixed tabs should be used with a limited number of tabs, and when a consistent placement will aid muscle memory.

### [Full width](https://v6.mui.com/material-ui/react-menu/#full-width)

The `variant="fullWidth"` prop should be used for smaller views.

### [Centered](https://v6.mui.com/material-ui/react-menu/#centered)

The `centered` prop should be used for larger views.

Press Enter to start editing

### [Automatic scroll buttons](https://v6.mui.com/material-ui/react-menu/#automatic-scroll-buttons)

Use the `variant="scrollable"` and `scrollButtons="auto"` props to display left and right scroll buttons on desktop that are hidden on mobile:

Press Enter to start editing

### [Forced scroll buttons](https://v6.mui.com/material-ui/react-menu/#forced-scroll-buttons)

Apply `scrollButtons={true}` and the `allowScrollButtonsMobile` prop to display the left and right scroll buttons on all viewports:

Press Enter to start editing

If you want to make sure the buttons are always visible, you should customize the opacity.

```css
.MuiTabs-scrollButtons.Mui-disabled { opacity: 0.3; }
```

### [Prevent scroll buttons](https://v6.mui.com/material-ui/react-menu/#prevent-scroll-buttons)

Left and right scroll buttons are never be presented with `scrollButtons={false}`. All scrolling must be initiated through user agent scrolling mechanisms (for example left/right swipe, shift mouse wheel, etc.)

Press Enter to start editing

## [Customization](https://v6.mui.com/material-ui/react-menu/#customization)

Here is an example of customizing the component. You can learn more about this in the [overrides documentation page](https://v6.mui.com/material-ui/customization/how-to-customize/).

🎨 If you are looking for inspiration, you can check [MUI Treasury's customization examples](https://mui-treasury.com/?path=/docs/tabs-introduction--docs).

## [Vertical tabs](https://v6.mui.com/material-ui/react-menu/#vertical-tabs)

To make vertical tabs instead of default horizontal ones, there is `orientation="vertical"`:

Note that you can restore the scrollbar with `visibleScrollbar`.

## [Nav tabs](https://v6.mui.com/material-ui/react-menu/#nav-tabs)

By default, tabs use a `button` element, but you can provide your custom tag or component. Here's an example of implementing tabbed navigation:

Press Enter to start editing

### [Third-party routing library](https://v6.mui.com/material-ui/react-menu/#third-party-routing-library)

One frequent use case is to perform navigation on the client only, without an HTTP round-trip to the server. The `Tab` component provides the `component` prop to handle this use case. Here is a [more detailed guide](https://v6.mui.com/material-ui/integrations/routing/#tabs).

## [Icon tabs](https://v6.mui.com/material-ui/react-menu/#icon-tabs)

Tab labels may be either all icons or all text.

Press Enter to start editing

Press Enter to start editing

## [Icon position](https://v6.mui.com/material-ui/react-menu/#icon-position)

By default, the icon is positioned at the `top` of a tab. Other supported positions are `start`, `end`, `bottom`.

Press Enter to start editing

## [Accessibility](https://v6.mui.com/material-ui/react-menu/#accessibility)

(WAI-ARIA: [https://www.w3.org/WAI/ARIA/apg/patterns/tabs/](https://www.w3.org/WAI/ARIA/apg/patterns/tabs/))

The following steps are needed in order to provide necessary information for assistive technologies:

1.  Label `Tabs` via `aria-label` or `aria-labelledby`.
2.  `Tab`s need to be connected to their corresponding `[role="tabpanel"]` by setting the correct `id`, `aria-controls` and `aria-labelledby`.

An example for the current implementation can be found in the demos on this page. We've also published [an experimental API](https://v6.mui.com/material-ui/react-menu/#experimental-api) in `@mui/lab` that does not require extra work.

### [Keyboard navigation](https://v6.mui.com/material-ui/react-menu/#keyboard-navigation)

The components implement keyboard navigation using the "manual activation" behavior. If you want to switch to the "selection automatically follows focus" behavior you have to pass `selectionFollowsFocus` to the `Tabs` component. The WAI-ARIA authoring practices have a detailed guide on [how to decide when to make selection automatically follow focus](https://www.w3.org/WAI/ARIA/apg/practices/keyboard-interface/#x6-4-deciding-when-to-make-selection-automatically-follow-focus).

#### Demo

The following two demos only differ in their keyboard navigation behavior. Focus a tab and navigate with arrow keys to notice the difference, for example Arrow Left.

```jsx
/* Tabs where selection follows focus */ <Tabs selectionFollowsFocus />
```

```jsx
/* Tabs where each tab needs to be selected manually */ <Tabs />
```

## [Unstyled](https://v6.mui.com/material-ui/react-menu/#unstyled)

Use the [Base UI Tabs](https://v6.mui.com/base-ui/react-tabs/) for complete ownership of the component's design, with no Material UI or Joy UI styles to override. This unstyled version of the component is the ideal choice for heavy customization with a smaller bundle size.

## [API](https://v6.mui.com/material-ui/react-menu/#api)

See the documentation below for a complete reference to all of the props and classes available to the components mentioned here.

-   [`<Tab />`](https://v6.mui.com/material-ui/api/tab/)
-   [`<TabContext />`](https://v6.mui.com/material-ui/api/tab-context/)
-   [`<TabList />`](https://v6.mui.com/material-ui/api/tab-list/)
-   [`<TabPanel />`](https://v6.mui.com/material-ui/api/tab-panel/)
-   [`<TabScrollButton />`](https://v6.mui.com/material-ui/api/tab-scroll-button/)
-   [`<Tabs />`](https://v6.mui.com/material-ui/api/tabs/)