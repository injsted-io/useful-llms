Tooltips display informative text when users hover over, focus on, or tap an element.

When activated, Tooltips display a text label identifying an element, such as a description of its function.

-   [Feedback](https://github.com/mui/material-ui/labels/component%3A%20tooltip)
-   [Bundle size](https://bundlephobia.com/package/@mui/material@latest "Scroll down to 'Exports Analysis' for a more detailed report.")
-   [Source](https://github.com/mui/material-ui/tree/v6.4.11/packages/mui-material/src/Tooltip)
-   [WAI-ARIA](https://www.w3.org/WAI/ARIA/apg/patterns/tooltip/)
-   [Material Design](https://m2.material.io/components/tooltips)
-   [Figma](https://mui.com/store/items/figma-react/?utm_source=docs&utm_medium=referral&utm_campaign=component-link-header)
-   [Sketch](https://mui.com/store/items/sketch-react/?utm_source=docs&utm_medium=referral&utm_campaign=component-link-header)

Press Enter to start editing

The `Tooltip` has 12 **placement** choices. They don't have directional arrows; instead, they rely on motion emanating from the source to convey direction.

## [Customization](https://v6.mui.com/material-ui/all-components/#customization)

Here are some examples of customizing the component. You can learn more about this in the [overrides documentation page](https://v6.mui.com/material-ui/customization/how-to-customize/).

You can use the `arrow` prop to give your tooltip an arrow indicating which element it refers to.

Press Enter to start editing

## [Distance from anchor](https://v6.mui.com/material-ui/all-components/#distance-from-anchor)

To adjust the distance between the tooltip and its anchor, you can use the `slotProps` prop to modify the [offset](https://popper.js.org/docs/v2/modifiers/offset/) of the popper.

Alternatively, you can use the `slotProps` prop to customize the margin of the popper.

## [Custom child element](https://v6.mui.com/material-ui/all-components/#custom-child-element)

The tooltip needs to apply DOM event listeners to its child element. If the child is a custom React element, you need to make sure that it spreads its props to the underlying DOM element.

```jsx
const MyComponent = React.forwardRef(function MyComponent(props, ref) { // Spread the props to the underlying DOM element. return ( <div {...props} ref={ref}> Bin </div> ); }); // ... <Tooltip title="Delete"> <MyComponent /> </Tooltip>;
```

If using a class component as a child, you'll also need to ensure that the ref is forwarded to the underlying DOM element. (A ref to the class component itself will not work.)

```jsx
class MyComponent extends React.Component { render() { const { innerRef, ...props } = this.props; // Spread the props to the underlying DOM element. return ( <div {...props} ref={innerRef}> Bin </div> ); } } // Wrap MyComponent to forward the ref as expected by Tooltip const WrappedMyComponent = React.forwardRef(function WrappedMyComponent(props, ref) { return <MyComponent {...props} innerRef={ref} />; }); // ... <Tooltip title="Delete"> <WrappedMyComponent /> </Tooltip>;
```

## [Triggers](https://v6.mui.com/material-ui/all-components/#triggers)

You can define the types of events that cause a tooltip to show.

The touch action requires a long press due to the `enterTouchDelay` prop being set to `700`ms by default.

You can use the `open`, `onOpen` and `onClose` props to control the behavior of the tooltip.

Press Enter to start editing

## [Variable width](https://v6.mui.com/material-ui/all-components/#variable-width)

The `Tooltip` wraps long text by default to make it readable.

Press Enter to start editing

## [Interactive](https://v6.mui.com/material-ui/all-components/#interactive)

Tooltips are interactive by default (to pass [WCAG 2.1 success criterion 1.4.13](https://www.w3.org/TR/WCAG21/#content-on-hover-or-focus)). It won't close when the user hovers over the tooltip before the `leaveDelay` is expired. You can disable this behavior (thus failing the success criterion which is required to reach level AA) by passing `disableInteractive`.

Press Enter to start editing

## [Disabled elements](https://v6.mui.com/material-ui/all-components/#disabled-elements)

By default disabled elements like `<button>` do not trigger user interactions so a `Tooltip` will not activate on normal events like hover. To accommodate disabled elements, add a simple wrapper element, such as a `span`.

Press Enter to start editing

```jsx
<Tooltip title="You don't have permission to do this"> <span> <button disabled={disabled} style={disabled ? { pointerEvents: 'none' } : {}}> A disabled button </button> </span> </Tooltip>
```

## [Transitions](https://v6.mui.com/material-ui/all-components/#transitions)

Use a different transition.

## [Follow cursor](https://v6.mui.com/material-ui/all-components/#follow-cursor)

You can enable the tooltip to follow the cursor by setting `followCursor={true}`.

Press Enter to start editing

## [Virtual element](https://v6.mui.com/material-ui/all-components/#virtual-element)

In the event you need to implement a custom placement, you can use the `anchorEl` prop: The value of the `anchorEl` prop can be a reference to a fake DOM element. You need to create an object shaped like the [`VirtualElement`](https://popper.js.org/docs/v2/virtual-elements/).

## [Showing and hiding](https://v6.mui.com/material-ui/all-components/#showing-and-hiding)

The tooltip is normally shown immediately when the user's mouse hovers over the element, and hides immediately when the user's mouse leaves. A delay in showing or hiding the tooltip can be added through the `enterDelay` and `leaveDelay` props.

On mobile, the tooltip is displayed when the user longpresses the element and hides after a delay of 1500ms. You can disable this feature with the `disableTouchListener` prop.

Press Enter to start editing

## [Accessibility](https://v6.mui.com/material-ui/all-components/#accessibility)

(WAI-ARIA: [https://www.w3.org/WAI/ARIA/apg/patterns/tooltip/](https://www.w3.org/WAI/ARIA/apg/patterns/tooltip/))

By default, the tooltip only labels its child element. This is notably different from `title` which can either label **or** describe its child depending on whether the child already has a label. For example, in:

```html
<button title="some more information">A button</button>
```

the `title` acts as an accessible description. If you want the tooltip to act as an accessible description you can pass `describeChild`. Note that you shouldn't use `describeChild` if the tooltip provides the only visual label. Otherwise, the child would have no accessible name and the tooltip would violate [success criterion 2.5.3 in WCAG 2.1](https://www.w3.org/WAI/WCAG21/Understanding/label-in-name.html).

Press Enter to start editing

## [API](https://v6.mui.com/material-ui/all-components/#api)

See the documentation below for a complete reference to all of the props and classes available to the components mentioned here.

-   [`<Tooltip />`](https://v6.mui.com/material-ui/api/tooltip/)