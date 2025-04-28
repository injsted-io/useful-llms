The Accordion component lets users show and hide sections of related content on a page.

-   [Feedback](https://github.com/mui/material-ui/labels/component%3A%20accordion)
-   [Bundle size](https://bundlephobia.com/package/@mui/material@latest "Scroll down to 'Exports Analysis' for a more detailed report.")
-   [Source](https://github.com/mui/material-ui/tree/v6.4.11/packages/mui-material/src/Accordion)
-   [WAI-ARIA](https://www.w3.org/WAI/ARIA/apg/patterns/accordion/)
-   [Material Design](https://m1.material.io/components/expansion-panels.html)
-   [Figma](https://mui.com/store/items/figma-react/?utm_source=docs&utm_medium=referral&utm_campaign=component-link-header)
-   [Sketch](https://mui.com/store/items/sketch-react/?utm_source=docs&utm_medium=referral&utm_campaign=component-link-header)

## [Introduction](https://v6.mui.com/material-ui/react-progress/#introduction)

The Material UI Accordion component includes several complementary utility components to handle various use cases:

-   Accordion: the wrapper for grouping related components.
-   Accordion Summary: the wrapper for the Accordion header, which expands or collapses the content when clicked.
-   Accordion Details: the wrapper for the Accordion content.
-   Accordion Actions: an optional wrapper that groups a set of buttons.

Lorem ipsum dolor sit amet, consectetur adipiscing elit. Suspendisse malesuada lacus ex, sit amet blandit leo lobortis eget.

## [Basics](https://v6.mui.com/material-ui/react-progress/#basics)

```jsx
import Accordion from '@mui/material/Accordion'; import AccordionDetails from '@mui/material/AccordionDetails'; import AccordionSummary from '@mui/material/AccordionSummary';
```

### [Expand icon](https://v6.mui.com/material-ui/react-progress/#expand-icon)

Use the `expandIcon` prop on the Accordion Summary component to change the expand indicator icon. The component handles the turning upside-down transition automatically.

### [Expanded by default](https://v6.mui.com/material-ui/react-progress/#expanded-by-default)

Use the `defaultExpanded` prop on the Accordion component to have it opened by default.

Lorem ipsum dolor sit amet, consectetur adipiscing elit. Suspendisse malesuada lacus ex, sit amet blandit leo lobortis eget.

### [Transition](https://v6.mui.com/material-ui/react-progress/#transition)

Use the `slots.transition` and `slotProps.transition` props to change the Accordion's default transition.

### [Disabled item](https://v6.mui.com/material-ui/react-progress/#disabled-item)

Use the `disabled` prop on the Accordion component to disable interaction and focus.

### [Controlled Accordion](https://v6.mui.com/material-ui/react-progress/#controlled-accordion)

The Accordion component can be controlled or uncontrolled.

## [Customization](https://v6.mui.com/material-ui/react-progress/#customization)

### [Only one expanded at a time](https://v6.mui.com/material-ui/react-progress/#only-one-expanded-at-a-time)

Use the `expanded` prop with React's `useState` hook to allow only one Accordion item to be expanded at a time. The demo below also shows a bit of visual customization.

Lorem ipsum dolor sit amet, consectetur adipiscing elit. Suspendisse malesuada lacus ex, sit amet blandit leo lobortis eget. Lorem ipsum dolor sit amet, consectetur adipiscing elit. Suspendisse malesuada lacus ex, sit amet blandit leo lobortis eget.

### [Changing heading level](https://v6.mui.com/material-ui/react-progress/#changing-heading-level)

By default, the Accordion uses an `h3` element for the heading. You can change the heading element using the `slotProps.heading.component` prop to ensure the correct heading hierarchy in your document.

```jsx
<Accordion slotProps={{ heading: { component: 'h4' } }}> <AccordionSummary expandIcon={<ExpandMoreIcon />} aria-controls="panel1-content" id="panel1-header" > Accordion </AccordionSummary> <AccordionDetails> Lorem ipsum dolor sit amet, consectetur adipiscing elit. Suspendisse malesuada lacus ex, sit amet blandit leo lobortis eget. </AccordionDetails> </Accordion>
```

## [Performance](https://v6.mui.com/material-ui/react-progress/#performance)

The Accordion content is mounted by default even if it's not expanded. This default behavior has server-side rendering and SEO in mind.

If you render the Accordion Details with a big component tree nested inside, or if you have many Accordions, you may want to change this behavior by setting `unmountOnExit` to `true` inside the `slotProps.transition` prop to improve performance:

```jsx
<Accordion slotProps={{ transition: { unmountOnExit: true } }} />
```

## [Accessibility](https://v6.mui.com/material-ui/react-progress/#accessibility)

The [WAI-ARIA guidelines for accordions](https://www.w3.org/WAI/ARIA/apg/patterns/accordion/) recommend setting an `id` and `aria-controls`, which in this case would apply to the Accordion Summary component. The Accordion component then derives the necessary `aria-labelledby` and `id` from its content.

```jsx
<Accordion> <AccordionSummary id="panel-header" aria-controls="panel-content"> Header </AccordionSummary> <AccordionDetails> Lorem ipsum dolor sit amet, consectetur adipiscing elit. </AccordionDetails> </Accordion>
```

## [Anatomy](https://v6.mui.com/material-ui/react-progress/#anatomy)

The Accordion component consists of a root `<div>` that contains the Accordion Summary, Accordion Details, and optional Accordion Actions for action buttons.

```jsx
<div class="MuiAccordion-root"> <h3 class="MuiAccordion-heading"> <button class="MuiButtonBase-root MuiAccordionSummary-root" aria-expanded=""> <!-- Accordion summary goes here --> </button> </h3> <div class="MuiAccordion-region" role="region"> <div class="MuiAccordionDetails-root"> <!-- Accordion content goes here --> </div> </div> </div>
```

## [API](https://v6.mui.com/material-ui/react-progress/#api)

See the documentation below for a complete reference to all of the props and classes available to the components mentioned here.

-   [`<Accordion />`](https://v6.mui.com/material-ui/api/accordion/)
-   [`<AccordionActions />`](https://v6.mui.com/material-ui/api/accordion-actions/)
-   [`<AccordionDetails />`](https://v6.mui.com/material-ui/api/accordion-details/)
-   [`<AccordionSummary />`](https://v6.mui.com/material-ui/api/accordion-summary/)