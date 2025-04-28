The Pagination component enables the user to select a specific page from a range of pages.

-   [Feedback](https://github.com/mui/material-ui/labels/component%3A%20pagination)
-   [Bundle size](https://bundlephobia.com/package/@mui/material@latest "Scroll down to 'Exports Analysis' for a more detailed report.")
-   [Source](https://github.com/mui/material-ui/tree/v6.4.11/packages/mui-material/src/Pagination)
-   [Figma](https://mui.com/store/items/figma-react/?utm_source=docs&utm_medium=referral&utm_campaign=component-link-header)
-   [Sketch](https://mui.com/store/items/sketch-react/?utm_source=docs&utm_medium=referral&utm_campaign=component-link-header)

Press Enter to start editing

Press Enter to start editing

Press Enter to start editing

Press Enter to start editing

## [Buttons](https://v6.mui.com/material-ui/react-menu/#buttons)

You can optionally enable first-page and last-page buttons, or disable the previous-page and next-page buttons.

Press Enter to start editing

## [Custom icons](https://v6.mui.com/material-ui/react-menu/#custom-icons)

It's possible to customize the control icons.

Press Enter to start editing

You can specify how many digits to display either side of current page with the `siblingCount` prop, and adjacent to the start and end page number with the `boundaryCount` prop.

Press Enter to start editing

Press Enter to start editing

## [Router integration](https://v6.mui.com/material-ui/react-menu/#router-integration)

Press Enter to start editing

For advanced customization use cases, a headless `usePagination()` hook is exposed. It accepts almost the same options as the Pagination component minus all the props related to the rendering of JSX. The Pagination component is built on this hook.

```jsx
import usePagination from '@mui/material/usePagination';
```

-   …

The `Pagination` component was designed to paginate a list of arbitrary items when infinite loading isn't used. It's preferred in contexts where SEO is important, for instance, a blog.

For the pagination of a large set of tabular data, you should use the `TablePagination` component.

Press Enter to start editing

You can learn more about this use case in the [table section](https://v6.mui.com/material-ui/react-table/#custom-pagination-options) of the documentation.

## [Accessibility](https://v6.mui.com/material-ui/react-menu/#accessibility)

### [ARIA](https://v6.mui.com/material-ui/react-menu/#aria)

The root node has a role of "navigation" and aria-label "pagination navigation" by default. The page items have an aria-label that identifies the purpose of the item ("go to first page", "go to previous page", "go to page 1" etc.). You can override these using the `getItemAriaLabel` prop.

### [Keyboard](https://v6.mui.com/material-ui/react-menu/#keyboard)

The pagination items are in tab order, with a tabindex of "0".

## [API](https://v6.mui.com/material-ui/react-menu/#api)

See the documentation below for a complete reference to all of the props and classes available to the components mentioned here.

-   [`<Pagination />`](https://v6.mui.com/material-ui/api/pagination/)
-   [`<PaginationItem />`](https://v6.mui.com/material-ui/api/pagination-item/)
-   [`<TablePagination />`](https://v6.mui.com/material-ui/api/table-pagination/)