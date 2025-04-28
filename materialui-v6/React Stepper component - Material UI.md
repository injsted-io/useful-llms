Steppers convey progress through numbered steps. It provides a wizard-like workflow.

Steppers display progress through a sequence of logical and numbered steps. They may also be used for navigation. Steppers may display a transient feedback message after a step is saved.

-   **Types of Steps**: Editable, Non-editable, Mobile, Optional
-   **Types of Steppers**: Horizontal, Vertical, Linear, Non-linear

-   [Feedback](https://github.com/mui/material-ui/labels/component%3A%20stepper)
-   [Bundle size](https://bundlephobia.com/package/@mui/material@latest "Scroll down to 'Exports Analysis' for a more detailed report.")
-   [Source](https://github.com/mui/material-ui/tree/v6.4.11/packages/mui-material/src/Stepper)
-   [Material Design](https://m1.material.io/components/steppers.html)
-   [Figma](https://mui.com/store/items/figma-react/?utm_source=docs&utm_medium=referral&utm_campaign=component-link-header)
-   [Sketch](https://mui.com/store/items/sketch-react/?utm_source=docs&utm_medium=referral&utm_campaign=component-link-header)

## [Introduction](https://v6.mui.com/material-ui/react-menu/#introduction)

The Stepper component displays progress through a sequence of logical and numbered steps. It supports horizontal and vertical orientation for desktop and mobile viewports.

Steppers are implemented using a collection of related components:

-   Stepper: the container for the steps.
-   Step: an individual step in the sequence.
-   Step Label: a label for a Step.
-   Step Content: optional content for a Step.
-   Step Button: optional button for a Step.
-   Step Icon: optional icon for a Step.
-   Step Connector: optional customized connector between Steps.

## [Basics](https://v6.mui.com/material-ui/react-menu/#basics)

```jsx
import Stepper from '@mui/material/Stepper'; import Step from '@mui/material/Step'; import StepLabel from '@mui/material/StepLabel';
```

## [Horizontal stepper](https://v6.mui.com/material-ui/react-menu/#horizontal-stepper)

Horizontal steppers are ideal when the contents of one step depend on an earlier step.

Avoid using long step names in horizontal steppers.

### [Linear](https://v6.mui.com/material-ui/react-menu/#linear)

A linear stepper allows the user to complete the steps in sequence.

The `Stepper` can be controlled by passing the current step index (zero-based) as the `activeStep` prop. `Stepper` orientation is set using the `orientation` prop.

This example also shows the use of an optional step by placing the `optional` prop on the second `Step` component. Note that it's up to you to manage when an optional step is skipped. Once you've determined this for a particular step you must set `completed={false}` to signify that even though the active step index has gone beyond the optional step, it's not actually complete.

Select campaign settings

Create an ad groupOptional

Create an ad

Step 1

### [Non-linear](https://v6.mui.com/material-ui/react-menu/#non-linear)

Non-linear steppers allow the user to enter a multi-step flow at any point.

This example is similar to the regular horizontal stepper, except steps are no longer automatically set to `disabled={true}` based on the `activeStep` prop.

The use of the `StepButton` here demonstrates clickable step labels, as well as setting the `completed` flag. However because steps can be accessed in a non-linear fashion, it's up to your own implementation to determine when all steps are completed (or even if they need to be completed).

### [Alternative label](https://v6.mui.com/material-ui/react-menu/#alternative-label)

Labels can be placed below the step icon by setting the `alternativeLabel` prop on the `Stepper` component.

Select master blaster campaign settings

Press Enter to start editing

### [Error step](https://v6.mui.com/material-ui/react-menu/#error-step)

Select campaign settings

Create an ad groupAlert message

Create an ad

### [Customized horizontal stepper](https://v6.mui.com/material-ui/react-menu/#customized-horizontal-stepper)

Here is an example of customizing the component. You can learn more about this in the [overrides documentation page](https://v6.mui.com/material-ui/customization/how-to-customize/).

Press Enter to start editing

## [Vertical stepper](https://v6.mui.com/material-ui/react-menu/#vertical-stepper)

Vertical steppers are designed for narrow screen sizes. They are ideal for mobile. All the features of the horizontal stepper can be implemented.

Select campaign settings

For each ad campaign that you create, you can control how much you're willing to spend on clicks and conversions, which networks and geographical locations you want your ads to show on, and more.

### [Performance](https://v6.mui.com/material-ui/react-menu/#performance)

The content of a step is unmounted when closed. If you need to make the content available to search engines or render expensive component trees inside your modal while optimizing for interaction responsiveness it might be a good idea to keep the step mounted with:

```jsx
<StepContent TransitionProps={{ unmountOnExit: false }} />
```

## [Mobile stepper](https://v6.mui.com/material-ui/react-menu/#mobile-stepper)

This component implements a compact stepper suitable for a mobile device. It has more limited functionality than the vertical stepper. See [mobile steps](https://m1.material.io/components/steppers.html#steppers-types-of-steps) for its inspiration.

The mobile stepper supports three variants to display progress through the available steps: text, dots, and progress.

### [Text](https://v6.mui.com/material-ui/react-menu/#text)

The current step and total number of steps are displayed as text.

Select campaign settings

For each ad campaign that you create, you can control how much you're willing to spend on clicks and conversions, which networks and geographical locations you want your ads to show on, and more.

1 / 3

### [Dots](https://v6.mui.com/material-ui/react-menu/#dots)

Use dots when the number of steps is small.

### [Progress](https://v6.mui.com/material-ui/react-menu/#progress)

Use a progress bar when there are many steps, or if there are steps that need to be inserted during the process (based on responses to earlier steps).

## [API](https://v6.mui.com/material-ui/react-menu/#api)

See the documentation below for a complete reference to all of the props and classes available to the components mentioned here.

-   [`<MobileStepper />`](https://v6.mui.com/material-ui/api/mobile-stepper/)
-   [`<Step />`](https://v6.mui.com/material-ui/api/step/)
-   [`<StepButton />`](https://v6.mui.com/material-ui/api/step-button/)
-   [`<StepConnector />`](https://v6.mui.com/material-ui/api/step-connector/)
-   [`<StepContent />`](https://v6.mui.com/material-ui/api/step-content/)
-   [`<StepIcon />`](https://v6.mui.com/material-ui/api/step-icon/)
-   [`<StepLabel />`](https://v6.mui.com/material-ui/api/step-label/)
-   [`<Stepper />`](https://v6.mui.com/material-ui/api/stepper/)