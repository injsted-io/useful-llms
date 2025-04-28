Progress indicators commonly known as spinners, express an unspecified wait time or display the length of a process.

Progress indicators inform users about the status of ongoing processes, such as loading an app, submitting a form, or saving updates.

-   **Determinate** indicators display how long an operation will take.
-   **Indeterminate** indicators visualize an unspecified wait time.

The animations of the components rely on CSS as much as possible to work even before the JavaScript is loaded.

-   [Feedback](https://github.com/mui/material-ui/labels/component%3A%20progress)
-   [Bundle size](https://bundlephobia.com/package/@mui/material@latest "Scroll down to 'Exports Analysis' for a more detailed report.")
-   [Source](https://github.com/mui/material-ui/tree/v6.4.11/packages/mui-material/src/LinearProgress)
-   [Material Design](https://m2.material.io/components/progress-indicators)
-   [Figma](https://mui.com/store/items/figma-react/?utm_source=docs&utm_medium=referral&utm_campaign=component-link-header)
-   [Sketch](https://mui.com/store/items/sketch-react/?utm_source=docs&utm_medium=referral&utm_campaign=component-link-header)

## [Circular](https://v6.mui.com/material-ui/react-progress/#circular)

### [Circular indeterminate](https://v6.mui.com/material-ui/react-progress/#circular-indeterminate)

Press Enter to start editing

### [Circular color](https://v6.mui.com/material-ui/react-progress/#circular-color)

Press Enter to start editing

### [Circular size](https://v6.mui.com/material-ui/react-progress/#circular-size)

Press Enter to start editing

### [Circular determinate](https://v6.mui.com/material-ui/react-progress/#circular-determinate)

Press Enter to start editing

### [Interactive integration](https://v6.mui.com/material-ui/react-progress/#interactive-integration)

### [Circular with label](https://v6.mui.com/material-ui/react-progress/#circular-with-label)

Press Enter to start editing

## [Linear](https://v6.mui.com/material-ui/react-progress/#linear)

### [Linear indeterminate](https://v6.mui.com/material-ui/react-progress/#linear-indeterminate)

Press Enter to start editing

### [Linear color](https://v6.mui.com/material-ui/react-progress/#linear-color)

Press Enter to start editing

### [Linear determinate](https://v6.mui.com/material-ui/react-progress/#linear-determinate)

Press Enter to start editing

### [Linear buffer](https://v6.mui.com/material-ui/react-progress/#linear-buffer)

Press Enter to start editing

### [Linear with label](https://v6.mui.com/material-ui/react-progress/#linear-with-label)

Press Enter to start editing

## [Non-standard ranges](https://v6.mui.com/material-ui/react-progress/#non-standard-ranges)

The progress components accept a value in the range 0 - 100. This simplifies things for screen-reader users, where these are the default min / max values. Sometimes, however, you might be working with a data source where the values fall outside this range. Here's how you can easily transform a value in any range to a scale of 0 - 100:

```jsx
// MIN = Minimum expected value // MAX = Maximum expected value // Function to normalise the values (MIN / MAX could be integrated) const normalise = (value) => ((value - MIN) * 100) / (MAX - MIN); // Example component that utilizes the `normalise` function at the point of render. function Progress(props) { return ( <React.Fragment> <CircularProgress variant="determinate" value={normalise(props.value)} /> <LinearProgress variant="determinate" value={normalise(props.value)} /> </React.Fragment> ); }
```

## [Customization](https://v6.mui.com/material-ui/react-progress/#customization)

Here are some examples of customizing the component. You can learn more about this in the [overrides documentation page](https://v6.mui.com/material-ui/customization/how-to-customize/).

## [Delaying appearance](https://v6.mui.com/material-ui/react-progress/#delaying-appearance)

There are [3 important limits](https://www.nngroup.com/articles/response-times-3-important-limits/) to know around response time. The ripple effect of the `ButtonBase` component ensures that the user feels that the UI is reacting instantaneously. Normally, no special feedback is necessary during delays of more than 0.1 but less than 1.0 second. After 1.0 second, you can display a loader to keep user's flow of thought uninterrupted.

## [Limitations](https://v6.mui.com/material-ui/react-progress/#limitations)

### [High CPU load](https://v6.mui.com/material-ui/react-progress/#high-cpu-load)

Under heavy load, you might lose the stroke dash animation or see random `CircularProgress` ring widths. You should run processor intensive operations in a web worker or by batch in order not to block the main rendering thread.

When it's not possible, you can leverage the `disableShrink` prop to mitigate the issue. See [this issue](https://github.com/mui/material-ui/issues/10327).

Press Enter to start editing

### [High frequency updates](https://v6.mui.com/material-ui/react-progress/#high-frequency-updates)

The `LinearProgress` uses a transition on the CSS transform property to provide a smooth update between different values. The default transition duration is 200ms. In the event a parent component updates the `value` prop too quickly, you will at least experience a 200ms delay between the re-render and the progress bar fully updated.

If you need to perform 30 re-renders per second or more, we recommend disabling the transition:

```css
.MuiLinearProgress-bar { transition: none; }
```

## [API](https://v6.mui.com/material-ui/react-progress/#api)

See the documentation below for a complete reference to all of the props and classes available to the components mentioned here.

-   [`<CircularProgress />`](https://v6.mui.com/material-ui/api/circular-progress/)
-   [`<LinearProgress />`](https://v6.mui.com/material-ui/api/linear-progress/)