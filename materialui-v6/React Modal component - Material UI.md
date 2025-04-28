The modal component provides a solid foundation for creating dialogs, popovers, lightboxes, or whatever else.

The component renders its `children` node in front of a backdrop component. The `Modal` offers important features:

-   💄 Manages modal stacking when one-at-a-time just isn't enough.
-   🔐 Creates a backdrop, for disabling interaction below the modal.
-   🔐 It disables scrolling of the page content while open.
-   ♿️ It properly manages focus; moving to the modal content, and keeping it there until the modal is closed.
-   ♿️ Adds the appropriate ARIA roles automatically.

-   [Feedback](https://github.com/mui/material-ui/labels/component%3A%20modal)
-   [Bundle size](https://bundlephobia.com/package/@mui/material@latest "Scroll down to 'Exports Analysis' for a more detailed report.")
-   [Source](https://github.com/mui/material-ui/tree/v6.4.11/packages/mui-material/src/Modal)
-   [WAI-ARIA](https://www.w3.org/WAI/ARIA/apg/patterns/dialog-modal/)

If you are creating a modal dialog, you probably want to use the [Dialog](https://v6.mui.com/material-ui/react-dialog/) component rather than directly using Modal. Modal is a lower-level construct that is leveraged by the following components:

-   [Dialog](https://v6.mui.com/material-ui/react-dialog/)
-   [Drawer](https://v6.mui.com/material-ui/react-drawer/)
-   [Menu](https://v6.mui.com/material-ui/react-menu/)
-   [Popover](https://v6.mui.com/material-ui/react-popover/)

## [Basic modal](https://v6.mui.com/material-ui/react-menu/#basic-modal)

Press Enter to start editing

Notice that you can disable the outline (often blue or gold) with the `outline: 0` CSS property.

## [Nested modal](https://v6.mui.com/material-ui/react-menu/#nested-modal)

Modals can be nested, for example a select within a dialog, but stacking of more than two modals, or any two modals with a backdrop is discouraged.

Press Enter to start editing

## [Transitions](https://v6.mui.com/material-ui/react-menu/#transitions)

The open/close state of the modal can be animated with a transition component. This component should respect the following conditions:

-   Be a direct child descendent of the modal.
-   Have an `in` prop. This corresponds to the open/close state.
-   Call the `onEnter` callback prop when the enter transition starts.
-   Call the `onExited` callback prop when the exit transition is completed. These two callbacks allow the modal to unmount the child content when closed and fully transitioned.

Modal has built-in support for [react-transition-group](https://github.com/reactjs/react-transition-group).

Alternatively, you can use [react-spring](https://github.com/pmndrs/react-spring).

## [Performance](https://v6.mui.com/material-ui/react-menu/#performance)

The content of modal is unmounted when closed. If you need to make the content available to search engines or render expensive component trees inside your modal while optimizing for interaction responsiveness it might be a good idea to change this default behavior by enabling the `keepMounted` prop:

As with any performance optimization, this is not a silver bullet. Be sure to identify bottlenecks first, and then try out these optimization strategies.

## [Server-side modal](https://v6.mui.com/material-ui/react-menu/#server-side-modal)

React [doesn't support](https://github.com/facebook/react/issues/13097) the [`createPortal()`](https://react.dev/reference/react-dom/createPortal) API on the server. In order to display the modal, you need to disable the portal feature with the `disablePortal` prop:

## Server-side modal

If you disable JavaScript, you will still see me.

## [Limitations](https://v6.mui.com/material-ui/react-menu/#limitations)

### [Focus trap](https://v6.mui.com/material-ui/react-menu/#focus-trap)

The modal moves the focus back to the body of the component if the focus tries to escape it.

This is done for accessibility purposes. However, it might create issues. In the event the users need to interact with another part of the page, for example with a chatbot window, you can disable the behavior:

```jsx
<Modal disableEnforceFocus />
```

## [Accessibility](https://v6.mui.com/material-ui/react-menu/#accessibility)

(WAI-ARIA: [https://www.w3.org/WAI/ARIA/apg/patterns/dialog-modal/](https://www.w3.org/WAI/ARIA/apg/patterns/dialog-modal/))

-   Be sure to add `aria-labelledby="id..."`, referencing the modal title, to the `Modal`. Additionally, you may give a description of your modal with the `aria-describedby="id..."` prop on the `Modal`.
    
    ```jsx
    <Modal aria-labelledby="modal-title" aria-describedby="modal-description"> <h2 id="modal-title">My Title</h2> <p id="modal-description">My Description</p> </Modal>
    ```
    
-   The [WAI-ARIA Authoring Practices](https://www.w3.org/WAI/ARIA/apg/patterns/dialog-modal/examples/dialog/) can help you set the initial focus on the most relevant element, based on your modal content.
    
-   Keep in mind that a "modal window" overlays on either the primary window or another modal window. Windows under a modal are **inert**. That is, users cannot interact with content outside an active modal window. This might create [conflicting behaviors](https://v6.mui.com/material-ui/react-menu/#focus-trap).
    

## [Unstyled](https://v6.mui.com/material-ui/react-menu/#unstyled)

Use the [Base UI Modal](https://v6.mui.com/base-ui/react-modal/) for complete ownership of the component's design, with no Material UI or Joy UI styles to override. This unstyled version of the component is the ideal choice for heavy customization with a smaller bundle size.

## [API](https://v6.mui.com/material-ui/react-menu/#api)

See the documentation below for a complete reference to all of the props and classes available to the components mentioned here.

-   [`<Modal />`](https://v6.mui.com/material-ui/api/modal/)