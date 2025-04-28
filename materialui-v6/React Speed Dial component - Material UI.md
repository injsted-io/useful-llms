When pressed, a floating action button can display three to six related actions in the form of a Speed Dial.

If more than six actions are needed, something other than a FAB should be used to present them.

-   [Feedback](https://github.com/mui/material-ui/labels/component%3A%20speed%20dial)
-   [Bundle size](https://bundlephobia.com/package/@mui/material@latest "Scroll down to 'Exports Analysis' for a more detailed report.")
-   [Source](https://github.com/mui/material-ui/tree/v6.4.11/packages/mui-material/src/SpeedDial)
-   [WAI-ARIA](https://www.w3.org/WAI/ARIA/apg/patterns/menu-button/)
-   [Material Design](https://m2.material.io/components/buttons-floating-action-button#types-of-transitions)
-   [Figma](https://mui.com/store/items/figma-react/?utm_source=docs&utm_medium=referral&utm_campaign=component-link-header)
-   [Sketch](https://mui.com/store/items/sketch-react/?utm_source=docs&utm_medium=referral&utm_campaign=component-link-header)

## [Basic speed dial](https://v6.mui.com/material-ui/react-menu/#basic-speed-dial)

The floating action button can display related actions.

Press Enter to start editing

## [Playground](https://v6.mui.com/material-ui/react-menu/#playground)

## [Controlled speed dial](https://v6.mui.com/material-ui/react-menu/#controlled-speed-dial)

The open state of the component can be controlled with the `open`/`onOpen`/`onClose` props.

## [Custom close icon](https://v6.mui.com/material-ui/react-menu/#custom-close-icon)

You can provide an alternate icon for the closed and open states using the `icon` and `openIcon` props of the `SpeedDialIcon` component.

Press Enter to start editing

The SpeedDialActions tooltips can be displayed persistently so that users don't have to long-press to see the tooltip on touch devices.

It is enabled here across all devices for demo purposes, but in production it could use the `isTouch` logic to conditionally set the prop.

## [Accessibility](https://v6.mui.com/material-ui/react-menu/#accessibility)

### [ARIA](https://v6.mui.com/material-ui/react-menu/#aria)

#### Required

-   You should provide an `ariaLabel` for the speed dial component.
-   You should provide a `tooltipTitle` for each speed dial action.

#### Provided

-   The Fab has `aria-haspopup`, `aria-expanded` and `aria-controls` attributes.
-   The speed dial actions container has `role="menu"` and `aria-orientation` set according to the direction.
-   The speed dial actions have `role="menuitem"`, and an `aria-describedby` attribute that references the associated tooltip.

### [Keyboard](https://v6.mui.com/material-ui/react-menu/#keyboard)

-   The speed dial opens on focus.
-   The Space and Enter keys trigger the selected speed dial action, and toggle the speed dial open state.
-   The cursor keys move focus to the next or previous speed dial action. (Note that any cursor direction can be used initially to open the speed dial. This enables the expected behavior for the actual or perceived orientation of the speed dial, for example for a screen reader user who perceives the speed dial as a drop-down menu.)
-   The Escape key closes the speed dial and, if a speed dial action was focused, returns focus to the Fab.

## [API](https://v6.mui.com/material-ui/react-menu/#api)

See the documentation below for a complete reference to all of the props and classes available to the components mentioned here.

-   [`<SpeedDial />`](https://v6.mui.com/material-ui/api/speed-dial/)
-   [`<SpeedDialAction />`](https://v6.mui.com/material-ui/api/speed-dial-action/)
-   [`<SpeedDialIcon />`](https://v6.mui.com/material-ui/api/speed-dial-icon/)