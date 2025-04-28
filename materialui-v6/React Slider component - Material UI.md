Sliders allow users to make selections from a range of values.

Sliders reflect a range of values along a bar, from which users may select a single value. They are ideal for adjusting settings such as volume, brightness, or applying image filters.

-   [Feedback](https://github.com/mui/material-ui/labels/component%3A%20slider)
-   [Bundle size](https://bundlephobia.com/package/@mui/material@latest "Scroll down to 'Exports Analysis' for a more detailed report.")
-   [Source](https://github.com/mui/material-ui/tree/v6.4.11/packages/mui-material/src/Slider)
-   [WAI-ARIA](https://www.w3.org/WAI/ARIA/apg/patterns/slider-multithumb/)
-   [Material Design](https://m2.material.io/components/sliders)
-   [Figma](https://mui.com/store/items/figma-react/?utm_source=docs&utm_medium=referral&utm_campaign=component-link-header)
-   [Sketch](https://mui.com/store/items/sketch-react/?utm_source=docs&utm_medium=referral&utm_campaign=component-link-header)

## [Continuous sliders](https://v6.mui.com/material-ui/all-components/#continuous-sliders)

Continuous sliders allow users to select a value along a subjective range.

Press Enter to start editing

## [Sizes](https://v6.mui.com/material-ui/all-components/#sizes)

For smaller slider, use the prop `size="small"`.

Press Enter to start editing

## [Discrete sliders](https://v6.mui.com/material-ui/all-components/#discrete-sliders)

Discrete sliders can be adjusted to a specific value by referencing its value indicator. You can generate a mark for each step with `marks={true}`.

Press Enter to start editing

### [Small steps](https://v6.mui.com/material-ui/all-components/#small-steps)

You can change the default step increment. Make sure to adjust the `shiftStep` prop (the granularity with which the slider can step when using Page Up/Down or Shift + Arrow Up/Down) to a value divisible by the `step`.

Press Enter to start editing

### [Custom marks](https://v6.mui.com/material-ui/all-components/#custom-marks)

You can have custom marks by providing a rich array to the `marks` prop.

Press Enter to start editing

### [Restricted values](https://v6.mui.com/material-ui/all-components/#restricted-values)

You can restrict the selectable values to those provided with the `marks` prop with `step={null}`.

Press Enter to start editing

### [Label always visible](https://v6.mui.com/material-ui/all-components/#label-always-visible)

You can force the thumb label to be always visible with `valueLabelDisplay="on"`.

Press Enter to start editing

## [Range slider](https://v6.mui.com/material-ui/all-components/#range-slider)

The slider can be used to set the start and end of a range by supplying an array of values to the `value` prop.

Press Enter to start editing

### [Minimum distance](https://v6.mui.com/material-ui/all-components/#minimum-distance)

You can enforce a minimum distance between values in the `onChange` event handler. By default, when you move the pointer over a thumb while dragging another thumb, the active thumb will swap to the hovered thumb. You can disable this behavior with the `disableSwap` prop. If you want the range to shift when reaching minimum distance, you can utilize the `activeThumb` parameter in `onChange`.

Press Enter to start editing

## [Slider with input field](https://v6.mui.com/material-ui/all-components/#slider-with-input-field)

In this example, an input allows a discrete value to be set.

## [Color](https://v6.mui.com/material-ui/all-components/#color)

Press Enter to start editing

## [Customization](https://v6.mui.com/material-ui/all-components/#customization)

Here are some examples of customizing the component. You can learn more about this in the [overrides documentation page](https://v6.mui.com/material-ui/customization/how-to-customize/).

iOS

pretto.fr

Tooltip value label

Airbnb

### [Music player](https://v6.mui.com/material-ui/all-components/#music-player)

![can't win - Chilling Sunday](https://v6.mui.com/static/images/sliders/chilling-sunday.jpg)

Jun Pulse

**คนเก่าเขาทำไว้ดี (Can't win)**

Chilling Sunday — คนเก่าเขาทำไว้ดี

## [Vertical sliders](https://v6.mui.com/material-ui/all-components/#vertical-sliders)

Set the `orientation` prop to `"vertical"` to create vertical sliders. The thumb will track vertical movement instead of horizontal movement.

## [Marks placement](https://v6.mui.com/material-ui/all-components/#marks-placement)

You can customize your slider by adding and repositioning marks for minimum and maximum values.

## [Track](https://v6.mui.com/material-ui/all-components/#track)

The track shows the range available for user selection.

### [Removed track](https://v6.mui.com/material-ui/all-components/#removed-track)

The track can be turned off with `track={false}`.

Removed track

Removed track range slider

### [Inverted track](https://v6.mui.com/material-ui/all-components/#inverted-track)

The track can be inverted with `track="inverted"`.

Inverted track

Inverted track range

## [Non-linear scale](https://v6.mui.com/material-ui/all-components/#non-linear-scale)

You can use the `scale` prop to represent the `value` on a different scale.

In the following demo, the value _x_ represents the value _2^x_. Increasing _x_ by one increases the represented value by factor _2_.

Press Enter to start editing

## [Accessibility](https://v6.mui.com/material-ui/all-components/#accessibility)

(WAI-ARIA: [https://www.w3.org/WAI/ARIA/apg/patterns/slider-multithumb/](https://www.w3.org/WAI/ARIA/apg/patterns/slider-multithumb/))

The component handles most of the work necessary to make it accessible. However, you need to make sure that:

-   Each thumb has a user-friendly label (`aria-label`, `aria-labelledby` or `getAriaLabel` prop).
-   Each thumb has a user-friendly text for its current value. This is not required if the value matches the semantics of the label. You can change the name with the `getAriaValueText` or `aria-valuetext` prop.

## [Unstyled](https://v6.mui.com/material-ui/all-components/#unstyled)

Use the [Base UI Slider](https://v6.mui.com/base-ui/react-slider/) for complete ownership of the component's design, with no Material UI or Joy UI styles to override. This unstyled version of the component is the ideal choice for heavy customization with a smaller bundle size.

## [API](https://v6.mui.com/material-ui/all-components/#api)

See the documentation below for a complete reference to all of the props and classes available to the components mentioned here.

-   [`<Slider />`](https://v6.mui.com/material-ui/api/slider/)