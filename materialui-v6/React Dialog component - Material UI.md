Dialogs inform users about a task and can contain critical information, require decisions, or involve multiple tasks.

A Dialog is a type of [modal](https://v6.mui.com/material-ui/react-modal/) window that appears in front of app content to provide critical information or ask for a decision. Dialogs disable all app functionality when they appear, and remain on screen until confirmed, dismissed, or a required action has been taken.

Dialogs are purposefully interruptive, so they should be used sparingly.

-   [Feedback](https://github.com/mui/material-ui/labels/component%3A%20dialog)
-   [Bundle size](https://bundlephobia.com/package/@mui/material@latest "Scroll down to 'Exports Analysis' for a more detailed report.")
-   [Source](https://github.com/mui/material-ui/tree/v6.4.11/packages/mui-material/src/Dialog)
-   [WAI-ARIA](https://www.w3.org/WAI/ARIA/apg/patterns/dialog-modal/)
-   [Material Design](https://m2.material.io/components/dialogs)
-   [Figma](https://mui.com/store/items/figma-react/?utm_source=docs&utm_medium=referral&utm_campaign=component-link-header)
-   [Sketch](https://mui.com/store/items/sketch-react/?utm_source=docs&utm_medium=referral&utm_campaign=component-link-header)

## [Introduction](https://v6.mui.com/material-ui/all-components/#introduction)

Dialogs are implemented using a collection of related components:

-   Dialog: the parent component that renders the modal.
-   Dialog Title: a wrapper used for the title of a Dialog.
-   Dialog Actions: an optional container for a Dialog's Buttons.
-   Dialog Content: an optional container for displaying the Dialog's content.
-   Dialog Content Text: a wrapper for text inside of `<DialogContent />`.
-   Slide: optional [Transition](https://v6.mui.com/material-ui/transitions/#slide) used to slide the Dialog in from the edge of the screen.

Selected: user02@gmail.com

  

Press Enter to start editing

## [Basics](https://v6.mui.com/material-ui/all-components/#basics)

```jsx
import Dialog from '@mui/material/Dialog'; import DialogTitle from '@mui/material/DialogTitle';
```

## [Alerts](https://v6.mui.com/material-ui/all-components/#alerts)

Alerts are urgent interruptions, requiring acknowledgement, that inform the user about a situation.

Most alerts don't need titles. They summarize a decision in a sentence or two by either:

-   Asking a question (for example "Delete this conversation?")
-   Making a statement related to the action buttons

Use title bar alerts only for high-risk situations, such as the potential loss of connectivity. Users should be able to understand the choices based on the title and button text alone.

If a title is required:

-   Use a clear question or statement with an explanation in the content area, such as "Erase USB storage?".
-   Avoid apologies, ambiguity, or questions, such as "Warning!" or "Are you sure?"

## [Transitions](https://v6.mui.com/material-ui/all-components/#transitions)

You can also swap out the transition, the next example uses `Slide`.

## [Form dialogs](https://v6.mui.com/material-ui/all-components/#form-dialogs)

Form dialogs allow users to fill out form fields within a dialog. For example, if your site prompts for potential subscribers to fill in their email address, they can fill out the email field and touch 'Submit'.

## [Customization](https://v6.mui.com/material-ui/all-components/#customization)

Here is an example of customizing the component. You can learn more about this in the [overrides documentation page](https://v6.mui.com/material-ui/customization/how-to-customize/).

The dialog has a close button added to aid usability.

## [Full-screen dialogs](https://v6.mui.com/material-ui/all-components/#full-screen-dialogs)

## [Optional sizes](https://v6.mui.com/material-ui/all-components/#optional-sizes)

You can set a dialog maximum width by using the `maxWidth` enumerable in combination with the `fullWidth` boolean. When the `fullWidth` prop is true, the dialog will adapt based on the `maxWidth` value.

## [Responsive full-screen](https://v6.mui.com/material-ui/all-components/#responsive-full-screen)

You may make a dialog responsively full screen using [`useMediaQuery`](https://v6.mui.com/material-ui/react-use-media-query/).

```jsx
import useMediaQuery from '@mui/material/useMediaQuery'; function MyComponent() { const theme = useTheme(); const fullScreen = useMediaQuery(theme.breakpoints.down('md')); return <Dialog fullScreen={fullScreen} />; }
```

## [Confirmation dialogs](https://v6.mui.com/material-ui/all-components/#confirmation-dialogs)

Confirmation dialogs require users to explicitly confirm their choice before an option is committed. For example, users can listen to multiple ringtones but only make a final selection upon touching "OK".

Touching "Cancel" in a confirmation dialog, cancels the action, discards any changes, and closes the dialog.

Default notification ringtone

Tethys

## [Non-modal dialog](https://v6.mui.com/material-ui/all-components/#non-modal-dialog)

Dialogs can also be non-modal, meaning they don't interrupt user interaction behind it. Visit [the Nielsen Norman Group article](https://www.nngroup.com/articles/modal-nonmodal-dialog/) for more in-depth guidance about modal vs. non-modal dialog usage.

The demo below shows a persistent cookie banner, a common non-modal dialog use case.

## [Draggable dialog](https://v6.mui.com/material-ui/all-components/#draggable-dialog)

You can create a draggable dialog by using [react-draggable](https://github.com/react-grid-layout/react-draggable). To do so, you can pass the imported `Draggable` component as the `PaperComponent` of the `Dialog` component. This will make the entire dialog draggable.

## [Scrolling long content](https://v6.mui.com/material-ui/all-components/#scrolling-long-content)

When dialogs become too long for the user's viewport or device, they scroll.

-   `scroll=paper` the content of the dialog scrolls within the paper element.
-   `scroll=body` the content of the dialog scrolls within the body element.

Try the demo below to see what we mean:

## [Performance](https://v6.mui.com/material-ui/all-components/#performance)

Follow the [Modal performance section](https://v6.mui.com/material-ui/react-modal/#performance).

## [Limitations](https://v6.mui.com/material-ui/all-components/#limitations)

Follow the [Modal limitations section](https://v6.mui.com/material-ui/react-modal/#limitations).

## [Supplementary projects](https://v6.mui.com/material-ui/all-components/#supplementary-projects)

For more advanced use cases you might be able to take advantage of:

### [material-ui-confirm](https://v6.mui.com/material-ui/all-components/#material-ui-confirm)

![stars](https://img.shields.io/github/stars/jonatanklosko/material-ui-confirm?style=social&label=Star) ![npm downloads](https://img.shields.io/npm/dm/material-ui-confirm.svg)

The package [`material-ui-confirm`](https://github.com/jonatanklosko/material-ui-confirm/) provides dialogs for confirming user actions without writing boilerplate code.

## [Accessibility](https://v6.mui.com/material-ui/all-components/#accessibility)

Follow the [Modal accessibility section](https://v6.mui.com/material-ui/react-modal/#accessibility).

### [useDialogs](https://v6.mui.com/material-ui/all-components/#usedialogs)

You can create and manipulate dialogs imperatively with the [`useDialogs()`](https://mui.com/toolpad/core/react-use-dialogs/) API in `@toolpad/core`. This hook handles

-   state management for opening and closing dialogs
-   passing data to dialogs and receiving results back from them
-   stacking multiple dialogs
-   themed, asynchronous versions of `window.alert()`, `window.confirm()` and `window.prompt()`

The following example demonstrates some of these features:

```tsx
const handleDelete = async () => { const id = await dialogs.prompt('Enter the ID to delete', { okText: 'Delete', cancelText: 'Cancel', }); if (id) { const deleteConfirmed = await dialogs.confirm( `Are you sure you want to delete "${id}"?`, ); if (deleteConfirmed) { try { setIsDeleting(true); await mockApiDelete(id); dialogs.alert('Deleted!'); } catch (error) { const message = error instanceof Error ? error.message : 'Unknown error'; await dialogs.open(MyCustomDialog, { id, error: message }); } finally { setIsDeleting(false); } } } };
```

## [API](https://v6.mui.com/material-ui/all-components/#api)

See the documentation below for a complete reference to all of the props and classes available to the components mentioned here.

-   [`<Dialog />`](https://v6.mui.com/material-ui/api/dialog/)
-   [`<DialogActions />`](https://v6.mui.com/material-ui/api/dialog-actions/)
-   [`<DialogContent />`](https://v6.mui.com/material-ui/api/dialog-content/)
-   [`<DialogContentText />`](https://v6.mui.com/material-ui/api/dialog-content-text/)
-   [`<DialogTitle />`](https://v6.mui.com/material-ui/api/dialog-title/)
-   [`<Slide />`](https://v6.mui.com/material-ui/api/slide/)