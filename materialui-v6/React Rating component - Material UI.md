Ratings provide insight regarding others' opinions and experiences, and can allow the user to submit a rating of their own.

-   [Feedback](https://github.com/mui/material-ui/labels/component%3A%20rating)
-   [Bundle size](https://bundlephobia.com/package/@mui/material@latest "Scroll down to 'Exports Analysis' for a more detailed report.")
-   [Source](https://github.com/mui/material-ui/tree/v6.4.11/packages/mui-material/src/Rating)
-   [WAI-ARIA](https://www.w3.org/WAI/tutorials/forms/custom-controls/#a-star-rating)
-   [Figma](https://mui.com/store/items/figma-react/?utm_source=docs&utm_medium=referral&utm_campaign=component-link-header)
-   [Sketch](https://mui.com/store/items/sketch-react/?utm_source=docs&utm_medium=referral&utm_campaign=component-link-header)

## [Basic rating](https://v6.mui.com/material-ui/all-components/#basic-rating)

Controlled

1 Star2 Stars3 Stars4 Stars5 StarsEmpty

Uncontrolled

1 Star2 Stars3 Stars4 Stars5 StarsEmpty

Read onlyDisabled

1 Star2 Stars3 Stars4 Stars5 Stars

No rating given

1 Star2 Stars3 Stars4 Stars5 StarsEmpty

## [Rating precision](https://v6.mui.com/material-ui/all-components/#rating-precision)

The rating can display any float number with the `value` prop. Use the `precision` prop to define the minimum increment value change allowed.

0.5 Stars1 Star1.5 Stars2 Stars2.5 Stars3 Stars3.5 Stars4 Stars4.5 Stars5 StarsEmpty

Press Enter to start editing

## [Hover feedback](https://v6.mui.com/material-ui/all-components/#hover-feedback)

You can display a label on hover to help the user pick the correct rating value. The demo uses the `onChangeActive` prop.

0.5 Stars, Useless1 Star, Useless+1.5 Stars, Poor2 Stars, Poor+2.5 Stars, Ok3 Stars, Ok+3.5 Stars, Good4 Stars, Good+4.5 Stars, Excellent5 Stars, Excellent+Empty

Poor+

Press Enter to start editing

## [Sizes](https://v6.mui.com/material-ui/all-components/#sizes)

For larger or smaller ratings use the `size` prop.

1 Star2 Stars3 Stars4 Stars5 StarsEmpty1 Star2 Stars3 Stars4 Stars5 StarsEmpty1 Star2 Stars3 Stars4 Stars5 StarsEmpty

Press Enter to start editing

## [Customization](https://v6.mui.com/material-ui/all-components/#customization)

Here are some examples of customizing the component. You can learn more about this in the [overrides documentation page](https://v6.mui.com/material-ui/customization/how-to-customize/).

Custom icon and color

0.5 Hearts1 Heart1.5 Hearts2 Hearts2.5 Hearts3 Hearts3.5 Hearts4 Hearts4.5 Hearts5 HeartsEmpty

10 stars

1 Star2 Stars3 Stars4 Stars5 Stars6 Stars7 Stars8 Stars9 Stars10 StarsEmpty

Press Enter to start editing

## [Radio group](https://v6.mui.com/material-ui/all-components/#radio-group)

The rating is implemented with a radio group, set `highlightSelectedOnly` to restore the natural behavior.

Very DissatisfiedDissatisfiedNeutralSatisfiedVery SatisfiedEmpty

Press Enter to start editing

## [Accessibility](https://v6.mui.com/material-ui/all-components/#accessibility)

([WAI tutorial](https://www.w3.org/WAI/tutorials/forms/custom-controls/#a-star-rating))

The accessibility of this component relies on:

-   A radio group with its fields visually hidden. It contains six radio buttons, one for each star, and another for 0 stars that is checked by default. Be sure to provide a value for the `name` prop that is unique to the parent form.
-   Labels for the radio buttons containing actual text ("1 Star", "2 Stars", …). Be sure to provide a suitable function to the `getLabelText` prop when the page is in a language other than English. You can use the [included locales](https://v6.mui.com/material-ui/guides/localization/), or provide your own.
-   A visually distinct appearance for the rating icons. By default, the rating component uses both a difference of color and shape (filled and empty icons) to indicate the value. In the event that you are using color as the only means to indicate the value, the information should also be also displayed as text, as in this demo. This is important to match [success Criterion 1.4.1](https://www.w3.org/TR/WCAG21/#use-of-color) of WCAG2.1.

Press Enter to start editing

### [ARIA](https://v6.mui.com/material-ui/all-components/#aria)

The read only rating has a role of "img", and an aria-label that describes the displayed rating.

### [Keyboard](https://v6.mui.com/material-ui/all-components/#keyboard)

Because the rating component uses radio buttons, keyboard interaction follows the native browser behavior. Tab will focus the current rating, and cursor keys control the selected rating.

The read only rating is not focusable.

## [API](https://v6.mui.com/material-ui/all-components/#api)

See the documentation below for a complete reference to all of the props and classes available to the components mentioned here.

-   [`<Rating />`](https://v6.mui.com/material-ui/api/rating/)