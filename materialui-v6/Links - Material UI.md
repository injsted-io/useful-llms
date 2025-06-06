The Link component allows you to easily customize anchor elements with your theme colors and typography styles.

-   [Feedback](https://github.com/mui/material-ui/labels/component%3A%20link)
-   [Bundle size](https://bundlephobia.com/package/@mui/material@latest "Scroll down to 'Exports Analysis' for a more detailed report.")
-   [Source](https://github.com/mui/material-ui/tree/v6.4.11/packages/mui-material/src/Link)
-   [WAI-ARIA](https://www.w3.org/WAI/ARIA/apg/patterns/link/)
-   [Figma](https://mui.com/store/items/figma-react/?utm_source=docs&utm_medium=referral&utm_campaign=component-link-header)
-   [Sketch](https://mui.com/store/items/sketch-react/?utm_source=docs&utm_medium=referral&utm_campaign=component-link-header)

## [Basic links](https://v6.mui.com/material-ui/react-link/#basic-links)

The Link component is built on top of the [Typography](https://v6.mui.com/material-ui/api/typography/) component, meaning that you can use its props.

Press Enter to start editing

However, the Link component has some different default props than the Typography component:

-   `color="primary"` as the link needs to stand out.
-   `variant="inherit"` as the link will, most of the time, be used as a child of a Typography component.

## [Underline](https://v6.mui.com/material-ui/react-link/#underline)

The `underline` prop can be used to set the underline behavior. The default is `always`.

Press Enter to start editing

## [Security](https://v6.mui.com/material-ui/react-link/#security)

When you use `target="_blank"` with Links, it is [recommended](https://developers.google.com/web/tools/lighthouse/audits/noopener) to always set `rel="noopener"` or `rel="noreferrer"` when linking to third party content.

-   `rel="noopener"` prevents the new page from being able to access the `window.opener` property and ensures it runs in a separate process. Without this, the target page can potentially redirect your page to a malicious URL.
-   `rel="noreferrer"` has the same effect, but also prevents the _Referer_ header from being sent to the new page. ⚠️ Removing the referrer header will affect analytics.

## [Third-party routing library](https://v6.mui.com/material-ui/react-link/#third-party-routing-library)

One frequent use case is to perform navigation on the client only, without an HTTP round-trip to the server. The `Link` component provides the `component` prop to handle this use case. Here is a [more detailed guide](https://v6.mui.com/material-ui/integrations/routing/#link).

## [Accessibility](https://v6.mui.com/material-ui/react-link/#accessibility)

(WAI-ARIA: [https://www.w3.org/WAI/ARIA/apg/patterns/link/](https://www.w3.org/WAI/ARIA/apg/patterns/link/))

-   When providing the content for the link, avoid generic descriptions like "click here" or "go to". Instead, use [specific descriptions](https://developers.google.com/web/tools/lighthouse/audits/descriptive-link-text).
-   For the best user experience, links should stand out from the text on the page. For instance, you can keep the default `underline="always"` behavior.
-   If a link doesn't have a meaningful href, [it should be rendered using a `<button>` element](https://github.com/jsx-eslint/eslint-plugin-jsx-a11y/blob/HEAD/docs/rules/anchor-is-valid.md). The demo below illustrates how to properly link with a `<button>`:

Press Enter to start editing

### [Keyboard accessibility](https://v6.mui.com/material-ui/react-link/#keyboard-accessibility)

-   Interactive elements should receive focus in a coherent order when the user presses the Tab key.
-   Users should be able to open a link by pressing Enter.

### [Screen reader accessibility](https://v6.mui.com/material-ui/react-link/#screen-reader-accessibility)

-   When a link receives focus, screen readers should announce a descriptive link name. If the link opens in a new window or browser tab, add an [`aria-label`](https://www.w3.org/WAI/WCAG22/Techniques/aria/ARIA8) to inform screen reader users—for example, _"To learn more, visit the About page which opens in a new window."_

## [API](https://v6.mui.com/material-ui/react-link/#api)

See the documentation below for a complete reference to all of the props and classes available to the components mentioned here.

-   [`<Link />`](https://v6.mui.com/material-ui/api/link/)