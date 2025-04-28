The `layout` file is used to define a layout in your Next.js application.

```
<span><span>export</span><span> </span><span>default</span><span> </span><span>function</span><span> </span><span>DashboardLayout</span><span>({</span></span>
<span><span>  children</span><span>,</span></span>
<span><span>}</span><span>:</span><span> {</span></span>
<span><span>  children</span><span>:</span><span> </span><span>React</span><span>.</span><span>ReactNode</span></span>
<span><span>}) {</span></span>
<span><span>  </span><span>return</span><span> &lt;</span><span>section</span><span>&gt;{children}&lt;/</span><span>section</span><span>&gt;</span></span>
<span><span>}</span></span>
```

A **root layout** is the top-most layout in the root `app` directory. It is used to define the `<html>` and `<body>` tags and other globally shared UI.

```
<span><span>export</span><span> </span><span>default</span><span> </span><span>function</span><span> </span><span>RootLayout</span><span>({</span></span>
<span><span>  children</span><span>,</span></span>
<span><span>}</span><span>:</span><span> {</span></span>
<span><span>  children</span><span>:</span><span> </span><span>React</span><span>.</span><span>ReactNode</span></span>
<span><span>}) {</span></span>
<span><span>  </span><span>return</span><span> (</span></span>
<span><span>    &lt;</span><span>html</span><span> </span><span>lang</span><span>=</span><span>"en"</span><span>&gt;</span></span>
<span><span>      &lt;</span><span>body</span><span>&gt;{children}&lt;/</span><span>body</span><span>&gt;</span></span>
<span><span>    &lt;/</span><span>html</span><span>&gt;</span></span>
<span><span>  )</span></span>
<span><span>}</span></span>
```

## [Reference](https://nextjs.org/docs/app/api-reference/file-conventions/layout#reference)

### [Props](https://nextjs.org/docs/app/api-reference/file-conventions/layout#props)

#### [`children` (required)](https://nextjs.org/docs/app/api-reference/file-conventions/layout#children-required)

Layout components should accept and use a `children` prop. During rendering, `children` will be populated with the route segments the layout is wrapping. These will primarily be the component of a child [Layout](https://nextjs.org/docs/app/api-reference/file-conventions/page) (if it exists) or [Page](https://nextjs.org/docs/app/api-reference/file-conventions/page), but could also be other special files like [Loading](https://nextjs.org/docs/app/building-your-application/routing/loading-ui-and-streaming) or [Error](https://nextjs.org/docs/app/building-your-application/routing/error-handling) when applicable.

#### [`params` (optional)](https://nextjs.org/docs/app/api-reference/file-conventions/layout#params-optional)

A promise that resolves to an object containing the [dynamic route parameters](https://nextjs.org/docs/app/building-your-application/routing/dynamic-routes) object from the root segment down to that layout.

```
<span><span>export</span><span> </span><span>default</span><span> </span><span>async</span><span> </span><span>function</span><span> </span><span>Layout</span><span>({</span></span>
<span><span>  params</span><span>,</span></span>
<span><span>}</span><span>:</span><span> {</span></span>
<span><span>  params</span><span>:</span><span> </span><span>Promise</span><span>&lt;{ team</span><span>:</span><span> </span><span>string</span><span> }&gt;</span></span>
<span><span>}) {</span></span>
<span><span>  </span><span>const</span><span> { </span><span>team</span><span> } </span><span>=</span><span> </span><span>await</span><span> params</span></span>
<span><span>}</span></span>
```

| Example Route | URL | `params` |
| --- | --- | --- |
| `app/dashboard/[team]/layout.js` | `/dashboard/1` | `Promise<{ team: '1' }>` |
| `app/shop/[tag]/[item]/layout.js` | `/shop/1/2` | `Promise<{ tag: '1', item: '2' }>` |
| `app/blog/[...slug]/layout.js` | `/blog/1/2` | `Promise<{ slug: ['1', '2'] }>` |

-   Since the `params` prop is a promise. You must use `async/await` or React's [`use`](https://react.dev/reference/react/use) function to access the values.
    -   In version 14 and earlier, `params` was a synchronous prop. To help with backwards compatibility, you can still access it synchronously in Next.js 15, but this behavior will be deprecated in the future.

### [Root Layouts](https://nextjs.org/docs/app/api-reference/file-conventions/layout#root-layouts)

The `app` directory **must** include a root `app/layout.js`.

```
<span><span>export</span><span> </span><span>default</span><span> </span><span>function</span><span> </span><span>RootLayout</span><span>({</span></span>
<span><span>  children</span><span>,</span></span>
<span><span>}</span><span>:</span><span> {</span></span>
<span><span>  children</span><span>:</span><span> </span><span>React</span><span>.</span><span>ReactNode</span></span>
<span><span>}) {</span></span>
<span><span>  </span><span>return</span><span> (</span></span>
<span><span>    &lt;</span><span>html</span><span>&gt;</span></span>
<span><span>      &lt;</span><span>body</span><span>&gt;{children}&lt;/</span><span>body</span><span>&gt;</span></span>
<span><span>    &lt;/</span><span>html</span><span>&gt;</span></span>
<span><span>  )</span></span>
<span><span>}</span></span>
```

-   The root layout **must** define `<html>` and `<body>` tags.
    -   You should **not** manually add `<head>` tags such as `<title>` and `<meta>` to root layouts. Instead, you should use the [Metadata API](https://nextjs.org/docs/app/building-your-application/optimizing/metadata) which automatically handles advanced requirements such as streaming and de-duplicating `<head>` elements.
-   You can use [route groups](https://nextjs.org/docs/app/building-your-application/routing/route-groups) to create multiple root layouts.
    -   Navigating **across multiple root layouts** will cause a **full page load** (as opposed to a client-side navigation). For example, navigating from `/cart` that uses `app/(shop)/layout.js` to `/blog` that uses `app/(marketing)/layout.js` will cause a full page load. This **only** applies to multiple root layouts.

## [Caveats](https://nextjs.org/docs/app/api-reference/file-conventions/layout#caveats)

### [How can I access the request object in a layout?](https://nextjs.org/docs/app/api-reference/file-conventions/layout#how-can-i-access-the-request-object-in-a-layout)

You intentionally cannot access the raw request object in a layout. However, you can access [`headers`](https://nextjs.org/docs/app/api-reference/functions/headers) and [`cookies`](https://nextjs.org/docs/app/api-reference/functions/cookies) through server-only functions.

[Layouts](https://nextjs.org/docs/app/building-your-application/routing/layouts-and-templates#layouts) do not rerender. They can be cached and reused to avoid unnecessary computation when navigating between pages. By restricting layouts from accessing the raw request, Next.js can prevent the execution of potentially slow or expensive user code within the layout, which could negatively impact performance.

This design also enforces consistent and predictable behavior for layouts across different pages, which simplifies development and debugging.

### [Layouts do not receive `searchParams`](https://nextjs.org/docs/app/api-reference/file-conventions/layout#layouts-do-not-receive-searchparams)

Unlike [Pages](https://nextjs.org/docs/app/api-reference/file-conventions/page), Layout components **do not** receive the `searchParams` prop. This is because a shared layout is [not re-rendered during navigation](https://nextjs.org/docs/app/building-your-application/routing/linking-and-navigating#4-partial-rendering) which could lead to stale `searchParams` between navigations.

When using client-side navigation, Next.js automatically only renders the part of the page below the common layout between two routes.

For example, in the following directory structure, `dashboard/layout.tsx` is the common layout for both `/dashboard/settings` and `/dashboard/analytics`:

![File structure showing a dashboard folder nesting a layout.tsx file, and settings and analytics folders with their own pages](https://nextjs.org/_next/image?url=https%3A%2F%2Fh8DxKfmAPhn8O0p3.public.blob.vercel-storage.com%2Fdocs%2Fdark%2Fshared-dashboard-layout.png&w=3840&q=75)

When navigating from `/dashboard/settings` to `/dashboard/analytics`, `page.tsx` in `/dashboard/analytics` will rerender on the server, while `dashboard/layout.tsx` will **not** rerender because it's a common UI shared between the two routes.

This performance optimization allows navigation between pages that share a layout to be quicker as only the data fetching and rendering for the page has to run, instead of the entire route that could include shared layouts that fetch their own data.

Because `dashboard/layout.tsx` doesn't re-render, the `searchParams` prop in the layout Server Component might become **stale** after navigation.

Instead, use the Page [`searchParams`](https://nextjs.org/docs/app/api-reference/file-conventions/page#searchparams-optional) prop or the [`useSearchParams`](https://nextjs.org/docs/app/api-reference/functions/use-search-params) hook in a Client Component within the layout, which is rerendered on the client with the latest `searchParams`.

### [Layouts cannot access `pathname`](https://nextjs.org/docs/app/api-reference/file-conventions/layout#layouts-cannot-access-pathname)

Layouts cannot access `pathname`. This is because layouts are Server Components by default, and [don't rerender during client-side navigation](https://nextjs.org/docs/app/building-your-application/routing/linking-and-navigating#4-partial-rendering), which could lead to `pathname` becoming stale between navigations. To prevent staleness, Next.js would need to refetch all segments of a route, losing the benefits of caching and increasing the [RSC payload](https://nextjs.org/docs/app/building-your-application/rendering/server-components#what-is-the-react-server-component-payload-rsc) size on navigation.

Instead, you can extract the logic that depends on pathname into a Client Component and import it into your layouts. Since Client Components rerender (but are not refetched) during navigation, you can use Next.js hooks such as [`usePathname`](https://nextjs.org/docs/app/api-reference/functions/use-pathname) to access the current pathname and prevent staleness.

```
<span><span>import</span><span> { ClientComponent } </span><span>from</span><span> </span><span>'@/app/ui/ClientComponent'</span></span>
<span> </span>
<span><span>export</span><span> </span><span>default</span><span> </span><span>function</span><span> </span><span>Layout</span><span>({ children }</span><span>:</span><span> { children</span><span>:</span><span> </span><span>React</span><span>.</span><span>ReactNode</span><span> }) {</span></span>
<span><span>  </span><span>return</span><span> (</span></span>
<span><span>    &lt;&gt;</span></span>
<span><span>      &lt;</span><span>ClientComponent</span><span> /&gt;</span></span>
<span><span>      {</span><span>/* Other Layout UI */</span><span>}</span></span>
<span><span>      &lt;</span><span>main</span><span>&gt;{children}&lt;/</span><span>main</span><span>&gt;</span></span>
<span><span>    &lt;/&gt;</span></span>
<span><span>  )</span></span>
<span><span>}</span></span>
```

Common `pathname` patterns can also be implemented with [`params`](https://nextjs.org/docs/app/api-reference/file-conventions/layout#params-optional) prop.

See the [examples](https://nextjs.org/docs/app/building-your-application/routing/layouts-and-templates#examples) section for more information.

## [Examples](https://nextjs.org/docs/app/api-reference/file-conventions/layout#examples)

### [Displaying content based on `params`](https://nextjs.org/docs/app/api-reference/file-conventions/layout#displaying-content-based-on-params)

Using [dynamic route segments](https://nextjs.org/docs/app/building-your-application/routing/dynamic-routes), you can display or fetch specific content based on the `params` prop.

```
<span><span>export</span><span> </span><span>default</span><span> </span><span>async</span><span> </span><span>function</span><span> </span><span>DashboardLayout</span><span>({</span></span>
<span><span>  children</span><span>,</span></span>
<span><span>  params</span><span>,</span></span>
<span><span>}</span><span>:</span><span> {</span></span>
<span><span>  children</span><span>:</span><span> </span><span>React</span><span>.</span><span>ReactNode</span></span>
<span><span>  params</span><span>:</span><span> </span><span>Promise</span><span>&lt;{ team</span><span>:</span><span> </span><span>string</span><span> }&gt;</span></span>
<span><span>}) {</span></span>
<span><span>  </span><span>const</span><span> { </span><span>team</span><span> } </span><span>=</span><span> </span><span>await</span><span> params</span></span>
<span> </span>
<span><span>  </span><span>return</span><span> (</span></span>
<span><span>    &lt;</span><span>section</span><span>&gt;</span></span>
<span><span>      &lt;</span><span>header</span><span>&gt;</span></span>
<span><span>        &lt;</span><span>h1</span><span>&gt;Welcome to {team}'s Dashboard&lt;/</span><span>h1</span><span>&gt;</span></span>
<span><span>      &lt;/</span><span>header</span><span>&gt;</span></span>
<span><span>      &lt;</span><span>main</span><span>&gt;{children}&lt;/</span><span>main</span><span>&gt;</span></span>
<span><span>    &lt;/</span><span>section</span><span>&gt;</span></span>
<span><span>  )</span></span>
<span><span>}</span></span>
```

### [Reading `params` in Client Components](https://nextjs.org/docs/app/api-reference/file-conventions/layout#reading-params-in-client-components)

To use `params` in a Client Component (which cannot be `async`), you can use React's [`use`](https://react.dev/reference/react/use) function to read the promise:

```
<span><span>'use client'</span></span>
<span> </span>
<span><span>import</span><span> { use } </span><span>from</span><span> </span><span>'react'</span></span>
<span> </span>
<span><span>export</span><span> </span><span>default</span><span> </span><span>function</span><span> </span><span>Page</span><span>({</span></span>
<span><span>  params</span><span>,</span></span>
<span><span>}</span><span>:</span><span> {</span></span>
<span><span>  params</span><span>:</span><span> </span><span>Promise</span><span>&lt;{ slug</span><span>:</span><span> </span><span>string</span><span> }&gt;</span></span>
<span><span>}) {</span></span>
<span><span>  </span><span>const</span><span> { </span><span>slug</span><span> } </span><span>=</span><span> </span><span>use</span><span>(params)</span></span>
<span><span>}</span></span>
```

## [Version History](https://nextjs.org/docs/app/api-reference/file-conventions/layout#version-history)

| Version | Changes |
| --- | --- |
| `v15.0.0-RC` | `params` is now a promise. A [codemod](https://nextjs.org/docs/app/guides/upgrading/codemods#150) is available. |
| `v13.0.0` | `layout` introduced. |