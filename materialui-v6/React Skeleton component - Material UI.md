Display a placeholder preview of your content before the data gets loaded to reduce load-time frustration.

The data for your components might not be immediately available. You can improve the perceived responsiveness of the page by using skeletons. It feels like things are happening immediately, then the information is incrementally displayed on the screen (Cf. [Avoid The Spinner](https://www.lukew.com/ff/entry.asp?1797)).

-   [Feedback](https://github.com/mui/material-ui/labels/component%3A%20skeleton)
-   [Bundle size](https://bundlephobia.com/package/@mui/material@latest "Scroll down to 'Exports Analysis' for a more detailed report.")
-   [Source](https://github.com/mui/material-ui/tree/v6.4.11/packages/mui-material/src/Skeleton)
-   [Figma](https://mui.com/store/items/figma-react/?utm_source=docs&utm_medium=referral&utm_campaign=component-link-header)
-   [Sketch](https://mui.com/store/items/sketch-react/?utm_source=docs&utm_medium=referral&utm_campaign=component-link-header)

## [Usage](https://v6.mui.com/material-ui/react-progress/#usage)

The component is designed to be used **directly in your components**. For instance:

```jsx
{ item ? ( <img style={{ width: 210, height: 118, }} alt={item.title} src={item.src} /> ) : ( <Skeleton variant="rectangular" width={210} height={118} /> ); }
```

## [Variants](https://v6.mui.com/material-ui/react-progress/#variants)

The component supports 4 shape variants:

-   `text` (default): represents a single line of text (you can adjust the height via font size).
-   `circular`, `rectangular`, and `rounded`: come with different border radius to let you take control of the size.

Press Enter to start editing

## [Animations](https://v6.mui.com/material-ui/react-progress/#animations)

By default, the skeleton pulsates, but you can change the animation to a wave or disable it entirely.

Press Enter to start editing

### [Pulsate example](https://v6.mui.com/material-ui/react-progress/#pulsate-example)

![Don Diablo @ Tomorrowland Main Stage 2019 | Official…](https://i.ytimg.com/vi/pLqipJNItIo/hqdefault.jpg?sqp=-oaymwEYCNIBEHZIVfKriqkDCwgBFQAAiEIYAXAB&rs=AOn4CLBkklsyaw9FxDmMKapyBYCn9tbPNQ)

Don Diablo @ Tomorrowland Main Stage 2019 | Official…

Don Diablo396k views • a week ago

![Queen - Greatest Hits](https://i.ytimg.com/vi/_Uu12zY01ts/hqdefault.jpg?sqp=-oaymwEZCPYBEIoBSFXyq4qpAwsIARUAAIhCGAFwAQ==&rs=AOn4CLCpX6Jan2rxrCAZxJYDXppTP4MoQA)

Queen - Greatest Hits

Queen Official40M views • 3 years ago

![Calvin Harris, Sam Smith - Promises (Official Video)](https://i.ytimg.com/vi/kkLk2XWMBf8/hqdefault.jpg?sqp=-oaymwEYCNIBEHZIVfKriqkDCwgBFQAAiEIYAXAB&rs=AOn4CLB4GZTFu1Ju2EPPPXnhMZtFVvYBaw)

Calvin Harris, Sam Smith - Promises (Official Video)

Calvin Harris130M views • 10 months ago

### [Wave example](https://v6.mui.com/material-ui/react-progress/#wave-example)

![Nicola Sturgeon on a TED talk stage](https://pi.tedcdn.com/r/talkstar-photos.s3.amazonaws.com/uploads/72bda89f-9bbf-4685-910a-2f151c4f3a8a/NicolaSturgeon_2019T-embed.jpg?w=512)

Why First Minister of Scotland Nicola Sturgeon thinks GDP is the wrong measure of a country's success:

## [Inferring dimensions](https://v6.mui.com/material-ui/react-progress/#inferring-dimensions)

In addition to accepting `width` and `height` props, the component can also infer the dimensions.

It works well when it comes to typography as its height is set using `em` units.

```jsx
<Typography variant="h1">{loading ? <Skeleton /> : 'h1'}</Typography>
```

But when it comes to other components, you may not want to repeat the width and height. In these instances, you can pass `children` and it will infer its width and height from them.

```jsx
loading ? ( <Skeleton variant="circular"> <Avatar /> </Skeleton> ) : ( <Avatar src={data.avatar} /> );
```

![](https://pbs.twimg.com/profile_images/877631054525472768/Xp5FAPD5_reasonably_small.jpg)

Ted

![](https://pi.tedcdn.com/r/talkstar-photos.s3.amazonaws.com/uploads/72bda89f-9bbf-4685-910a-2f151c4f3a8a/NicolaSturgeon_2019T-embed.jpg?w=512)

## [Color](https://v6.mui.com/material-ui/react-progress/#color)

The color of the component can be customized by changing its `background-color` CSS property. This is especially useful when on a black background (as the skeleton will otherwise be invisible).

Press Enter to start editing

## [Accessibility](https://v6.mui.com/material-ui/react-progress/#accessibility)

Skeleton screens provide an alternative to the traditional spinner method. Rather than showing an abstract widget, skeleton screens create anticipation of what is to come and reduce cognitive load.

The background color of the skeleton uses the least amount of luminance to be visible in good conditions (good ambient light, good screen, no visual impairments).

### [ARIA](https://v6.mui.com/material-ui/react-progress/#aria)

None.

### [Keyboard](https://v6.mui.com/material-ui/react-progress/#keyboard)

The skeleton is not focusable.

## [API](https://v6.mui.com/material-ui/react-progress/#api)

See the documentation below for a complete reference to all of the props and classes available to the components mentioned here.

-   [`<Skeleton />`](https://v6.mui.com/material-ui/api/skeleton/)