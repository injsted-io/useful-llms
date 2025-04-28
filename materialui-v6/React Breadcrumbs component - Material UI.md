A breadcrumbs is a list of links that help visualize a page's location within a site's hierarchical structure, it allows navigation up to any of the ancestors.

-   [Feedback](https://github.com/mui/material-ui/labels/component%3A%20breadcrumbs)
-   [Bundle size](https://bundlephobia.com/package/@mui/material@latest "Scroll down to 'Exports Analysis' for a more detailed report.")
-   [Source](https://github.com/mui/material-ui/tree/v6.4.11/packages/mui-material/src/Breadcrumbs)
-   [WAI-ARIA](https://www.w3.org/WAI/ARIA/apg/patterns/breadcrumb/)
-   [Figma](https://mui.com/store/items/figma-react/?utm_source=docs&utm_medium=referral&utm_campaign=component-link-header)
-   [Sketch](https://mui.com/store/items/sketch-react/?utm_source=docs&utm_medium=referral&utm_campaign=component-link-header)

Press Enter to start editing

## [Active last breadcrumb](https://v6.mui.com/material-ui/react-card/#active-last-breadcrumb)

Keep the last breadcrumb interactive.

## [Custom separator](https://v6.mui.com/material-ui/react-card/#custom-separator)

In the following examples, we are using two string separators and an SVG icon.

Press Enter to start editing

Press Enter to start editing

As an alternative, consider adding a Menu component to display the condensed links in a dropdown list:

## [Customization](https://v6.mui.com/material-ui/react-card/#customization)

Here is an example of customizing the component. You can learn more about this in the [overrides documentation page](https://v6.mui.com/material-ui/customization/how-to-customize/).

Press Enter to start editing

## [Integration with react-router](https://v6.mui.com/material-ui/react-card/#integration-with-react-router)

-   [
    
    Inbox
    
    ](https://v6.mui.com/inbox)
-   -   [
        
        Important
        
        ](https://v6.mui.com/inbox/important)
    
-   [
    
    Trash
    
    ](https://v6.mui.com/trash)
-   [
    
    Spam
    
    ](https://v6.mui.com/spam)

## [Accessibility](https://v6.mui.com/material-ui/react-card/#accessibility)

(WAI-ARIA: [https://www.w3.org/WAI/ARIA/apg/patterns/breadcrumb/](https://www.w3.org/WAI/ARIA/apg/patterns/breadcrumb/))

Be sure to add a `aria-label` description on the `Breadcrumbs` component.

The accessibility of this component relies on:

-   The set of links is structured using an ordered list (`<ol>` element).
-   To prevent screen reader announcement of the visual separators between links, they are hidden with `aria-hidden`.
-   A nav element labeled with `aria-label` identifies the structure as a breadcrumb trail and makes it a navigation landmark so that it is easy to locate.

### [Page Container](https://v6.mui.com/material-ui/react-card/#page-container)

The [PageContainer](https://mui.com/toolpad/core/react-page-container/) component in `@toolpad/core` is the ideal wrapper for the content of your dashboard. It makes the Material UI Container navigation-aware and extends it with page title, breadcrumbs, actions, and more.

#### All

## [API](https://v6.mui.com/material-ui/react-card/#api)

See the documentation below for a complete reference to all of the props and classes available to the components mentioned here.

-   [`<Breadcrumbs />`](https://v6.mui.com/material-ui/api/breadcrumbs/)
-   [`<Link />`](https://v6.mui.com/material-ui/api/link/)
-   [`<Typography />`](https://v6.mui.com/material-ui/api/typography/)