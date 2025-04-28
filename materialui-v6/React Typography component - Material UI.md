Use typography to present your design and content as clearly and efficiently as possible.

-   [Feedback](https://github.com/mui/material-ui/labels/component%3A%20Typography)
-   [Bundle size](https://bundlephobia.com/package/@mui/material@latest "Scroll down to 'Exports Analysis' for a more detailed report.")
-   [Source](https://github.com/mui/material-ui/tree/v6.4.11/packages/mui-material/src/Typography)
-   [Material Design](https://m2.material.io/design/typography/the-type-system.html)
-   [Figma](https://mui.com/store/items/figma-react/?utm_source=docs&utm_medium=referral&utm_campaign=component-link-header)
-   [Sketch](https://mui.com/store/items/sketch-react/?utm_source=docs&utm_medium=referral&utm_campaign=component-link-header)

## [Roboto font](https://v6.mui.com/material-ui/all-components/#roboto-font)

Material UI uses the [Roboto](https://fonts.google.com/specimen/Roboto) font by default. Add it to your project via Fontsource, or with the Google Fonts CDN.

```bash
npm install @fontsource/roboto
```

Then you can import it in your entry point like this:

```tsx
import '@fontsource/roboto/300.css'; import '@fontsource/roboto/400.css'; import '@fontsource/roboto/500.css'; import '@fontsource/roboto/700.css';
```

### [Google Web Fonts](https://v6.mui.com/material-ui/all-components/#google-web-fonts)

To install Roboto through the Google Web Fonts CDN, add the following code inside your project's `<head />` tag:

```html
<link rel="preconnect" href="https://fonts.googleapis.com" /> <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin /> <link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Roboto:wght@300;400;500;700&display=swap" />
```

## [Component](https://v6.mui.com/material-ui/all-components/#component)

### [Usage](https://v6.mui.com/material-ui/all-components/#usage)

The Typography component follows the [Material Design typographic scale](https://m2.material.io/design/typography/#type-scale) that provides a limited set of type sizes that work well together for a consistent layout.

## h1. Heading

## h2. Heading

### h3. Heading

#### h4. Heading

##### h5. Heading

###### h6. Heading

###### subtitle1. Lorem ipsum dolor sit amet, consectetur adipisicing elit. Quos blanditiis tenetur

###### subtitle2. Lorem ipsum dolor sit amet, consectetur adipisicing elit. Quos blanditiis tenetur

body1. Lorem ipsum dolor sit amet, consectetur adipisicing elit. Quos blanditiis tenetur unde suscipit, quam beatae rerum inventore consectetur, neque doloribus, cupiditate numquam dignissimos laborum fugiat deleniti? Eum quasi quidem quibusdam.

body2. Lorem ipsum dolor sit amet, consectetur adipisicing elit. Quos blanditiis tenetur unde suscipit, quam beatae rerum inventore consectetur, neque doloribus, cupiditate numquam dignissimos laborum fugiat deleniti? Eum quasi quidem quibusdam.

button textcaption textoverline text

### [Theme keys](https://v6.mui.com/material-ui/all-components/#theme-keys)

In some situations you might not be able to use the Typography component. Hopefully, you might be able to take advantage of the [`typography`](https://v6.mui.com/material-ui/customization/default-theme/?expand-path=$.typography) keys of the theme.

This div's text looks like that of a button.

Press Enter to start editing

## [Customization](https://v6.mui.com/material-ui/all-components/#customization)

### [Adding & disabling variants](https://v6.mui.com/material-ui/all-components/#adding-amp-disabling-variants)

In addition to using the default typography variants, you can add custom ones, or disable any you don't need. See the [Adding & disabling variants](https://v6.mui.com/material-ui/customization/typography/#adding-amp-disabling-variants) page for more info.

### [Changing the semantic element](https://v6.mui.com/material-ui/all-components/#changing-the-semantic-element)

The Typography component uses the `variantMapping` prop to associate a UI variant with a semantic element. It's important to realize that the style of a typography component is independent from the semantic underlying element.

To change the underlying element for a one-off situation, like avoiding two `h1` elements in your page, use the `component` prop:

```jsx
<Typography variant="h1" component="h2"> h1. Heading </Typography>
```

To change the typography element mapping globally, [use the theme](https://v6.mui.com/material-ui/customization/typography/#adding-amp-disabling-variants):

```js
const theme = createTheme({ components: { MuiTypography: { defaultProps: { variantMapping: { h1: 'h2', h2: 'h2', h3: 'h2', h4: 'h2', h5: 'h2', h6: 'h2', subtitle1: 'h2', subtitle2: 'h2', body1: 'span', body2: 'span', }, }, }, }, });
```

### [System props](https://v6.mui.com/material-ui/all-components/#system-props)

## [Accessibility](https://v6.mui.com/material-ui/all-components/#accessibility)

Key factors to follow for an accessible typography:

-   **Color**. Provide enough contrast between text and its background, check out the minimum recommended [WCAG 2.0 color contrast ratio](https://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-contrast.html) (4.5:1).
-   **Font size**. Use [relative units (rem)](https://v6.mui.com/material-ui/customization/typography/#font-size), instead of pixels, to accommodate the user's browser settings.
-   **Heading hierarchy**. Based on [the W3 guidelines](https://www.w3.org/WAI/tutorials/page-structure/headings/), don't skip heading levels. Make sure to [separate the semantics from the style](https://v6.mui.com/material-ui/all-components/#changing-the-semantic-element).

## [API](https://v6.mui.com/material-ui/all-components/#api)

See the documentation below for a complete reference to all of the props and classes available to the components mentioned here.

-   [`<Typography />`](https://v6.mui.com/material-ui/api/typography/)