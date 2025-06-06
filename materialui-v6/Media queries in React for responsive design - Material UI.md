## useMediaQuery

This React hook listens for matches to a CSS media query. It allows the rendering of components based on whether the query matches or not.

Some of the key features:

-   ⚛️ It has an idiomatic React API.
-   🚀 It's performant, it observes the document to detect when its media queries change, instead of polling the values periodically.
-   📦 [1.1 kB gzipped](https://bundlephobia.com/package/@mui/material).
-   🤖 It supports server-side rendering.

You should provide a media query to the first argument of the hook. The media query string can be any valid CSS media query, for example [`'(prefers-color-scheme: dark)'`](https://v6.mui.com/material-ui/customization/dark-mode/#system-preference).

⚠️ You can't use `'print'` per browsers limitation, for example [Firefox](https://bugzilla.mozilla.org/show_bug.cgi?id=774398).

## [Using breakpoint helpers](https://v6.mui.com/material-ui/react-no-ssr/#using-breakpoint-helpers)

You can use Material UI's [breakpoint helpers](https://v6.mui.com/material-ui/customization/breakpoints/) as follows:

```jsx
import { useTheme } from '@mui/material/styles'; import useMediaQuery from '@mui/material/useMediaQuery'; function MyComponent() { const theme = useTheme(); const matches = useMediaQuery(theme.breakpoints.up('sm')); return <span>{`theme.breakpoints.up('sm') matches: ${matches}`}</span>; }
```

Alternatively, you can use a callback function, accepting the theme as a first argument:

```jsx
import useMediaQuery from '@mui/material/useMediaQuery'; function MyComponent() { const matches = useMediaQuery((theme) => theme.breakpoints.up('sm')); return <span>{`theme.breakpoints.up('sm') matches: ${matches}`}</span>; }
```

⚠️ There is **no default** theme support, you have to inject it in a parent theme provider.

## [Using JavaScript syntax](https://v6.mui.com/material-ui/react-no-ssr/#using-javascript-syntax)

You can use [json2mq](https://github.com/akiran/json2mq) to generate media query string from a JavaScript object.

## [Testing](https://v6.mui.com/material-ui/react-no-ssr/#testing)

You need an implementation of [matchMedia](https://developer.mozilla.org/en-US/docs/Web/API/Window/matchMedia) in your test environment.

For instance, [jsdom doesn't support it yet](https://jestjs.io/docs/manual-mocks#mocking-methods-which-are-not-implemented-in-jsdom). You should polyfill it. Using [css-mediaquery](https://github.com/ericf/css-mediaquery) to emulate it is recommended.

```js
import mediaQuery from 'css-mediaquery'; function createMatchMedia(width) { return (query) => ({ matches: mediaQuery.match(query, { width, }), addEventListener: () => {}, removeEventListener: () => {}, }); } describe('MyTests', () => { beforeAll(() => { window.matchMedia = createMatchMedia(window.innerWidth); }); });
```

## [Client-side only rendering](https://v6.mui.com/material-ui/react-no-ssr/#client-side-only-rendering)

To perform the server-side hydration, the hook needs to render twice. A first time with `defaultMatches`, the value of the server, and a second time with the resolved value. This double pass rendering cycle comes with a drawback: it's slower. You can set the `noSsr` option to `true` if you use the returned value **only** client-side.

```js
const matches = useMediaQuery('(min-width:600px)', { noSsr: true });
```

or it can turn it on globally with the theme:

```js
const theme = createTheme({ components: { MuiUseMediaQuery: { defaultProps: { noSsr: true, }, }, }, });
```

## [Server-side rendering](https://v6.mui.com/material-ui/react-no-ssr/#server-side-rendering)

Try relying on client-side CSS media queries first. For instance, you could use:

-   [`<Box display>`](https://v6.mui.com/system/display/#hiding-elements)
-   [`themes.breakpoints.up(x)`](https://v6.mui.com/material-ui/customization/breakpoints/#css-media-queries)
-   or [`sx prop`](https://v6.mui.com/system/getting-started/the-sx-prop/)

If none of the above alternatives are an option, you can proceed reading this section of the documentation.

First, you need to guess the characteristics of the client request, from the server. You have the choice between using:

-   **User agent**. Parse the user agent string of the client to extract information. Using [ua-parser-js](https://github.com/faisalman/ua-parser-js) to parse the user agent is recommended.
-   **Client hints**. Read the hints the client is sending to the server. Be aware that this feature is [not supported everywhere](https://caniuse.com/#search=client%20hint).

Finally, you need to provide an implementation of [matchMedia](https://developer.mozilla.org/en-US/docs/Web/API/Window/matchMedia) to the `useMediaQuery` with the previously guessed characteristics. Using [css-mediaquery](https://github.com/ericf/css-mediaquery) to emulate matchMedia is recommended.

For instance on the server-side:

```js
import * as ReactDOMServer from 'react-dom/server'; import parser from 'ua-parser-js'; import mediaQuery from 'css-mediaquery'; import { createTheme, ThemeProvider } from '@mui/material/styles'; function handleRender(req, res) { const deviceType = parser(req.headers['user-agent']).device.type || 'desktop'; const ssrMatchMedia = (query) => ({ matches: mediaQuery.match(query, { // The estimated CSS width of the browser. width: deviceType === 'mobile' ? '0px' : '1024px', }), }); const theme = createTheme({ components: { // Change the default options of useMediaQuery MuiUseMediaQuery: { defaultProps: { ssrMatchMedia, }, }, }, }); const html = ReactDOMServer.renderToString( <ThemeProvider theme={theme}> <App /> </ThemeProvider>, ); // … }
```

Make sure you provide the same custom match media implementation to the client-side to guarantee a hydration match.

## [Migrating from `withWidth()`](https://v6.mui.com/material-ui/react-no-ssr/#migrating-from-withwidth)

The `withWidth()` higher-order component injects the screen width of the page. You can reproduce the same behavior with a `useWidth` hook:

## [API](https://v6.mui.com/material-ui/react-no-ssr/#api)

### [`useMediaQuery(query, [options]) => matches`](https://v6.mui.com/material-ui/react-no-ssr/#usemediaquery-query-options-matches)

#### Arguments

1.  `query` (_string_ | _func_): A string representing the media query to handle or a callback function accepting the theme (in the context) that returns a string.
2.  `options` (_object_ \[optional\]):

-   `options.defaultMatches` (_bool_ \[optional\]): As `window.matchMedia()` is unavailable on the server, it returns a default matches during the first mount. The default value is `false`.
-   `options.matchMedia` (_func_ \[optional\]): You can provide your own implementation of _matchMedia_. This can be used for handling an iframe content window.
-   `options.noSsr` (_bool_ \[optional\]): Defaults to `false`. To perform the server-side hydration, the hook needs to render twice. A first time with `defaultMatches`, the value of the server, and a second time with the resolved value. This double pass rendering cycle comes with a drawback: it's slower. You can set this option to `true` if you use the returned value **only** client-side.
-   `options.ssrMatchMedia` (_func_ \[optional\]): You can provide your own implementation of _matchMedia_, it's used when rendering server-side.

Note: You can change the default options using the [`default props`](https://v6.mui.com/material-ui/customization/theme-components/#theme-default-props) feature of the theme with the `MuiUseMediaQuery` key.

#### Returns

`matches`: Matches is `true` if the document currently matches the media query and `false` when it does not.

#### Examples

```jsx
import * as React from 'react'; import useMediaQuery from '@mui/material/useMediaQuery'; export default function SimpleMediaQuery() { const matches = useMediaQuery('(min-width:600px)'); return <span>{`(min-width:600px) matches: ${matches}`}</span>; }
```