`<Link>` is a React component that extends the HTML `<a>` element to provide [prefetching](https://nextjs.org/docs/app/building-your-application/routing/linking-and-navigating#2-prefetching) and client-side navigation between routes. It is the primary way to navigate between routes in Next.js.

Basic usage:

```
<span><span>import</span><span> Link </span><span>from</span><span> </span><span>'next/link'</span></span>
<span> </span>
<span><span>export</span><span> </span><span>default</span><span> </span><span>function</span><span> </span><span>Page</span><span>() {</span></span>
<span><span>  </span><span>return</span><span> &lt;</span><span>Link</span><span> </span><span>href</span><span>=</span><span>"/dashboard"</span><span>&gt;Dashboard&lt;/</span><span>Link</span><span>&gt;</span></span>
<span><span>}</span></span>
```

## [Reference](https://nextjs.org/docs/app/api-reference/components/link#reference)

The following props can be passed to the `<Link>` component:

| Prop | Example | Type | Required |
| --- | --- | --- | --- |
| [`href`](https://nextjs.org/docs/app/api-reference/components/link#href-required) | `href="/dashboard"` | String or Object | Yes |
| [`replace`](https://nextjs.org/docs/app/api-reference/components/link#replace) | `replace={false}` | Boolean | \- |
| [`scroll`](https://nextjs.org/docs/app/api-reference/components/link#scroll) | `scroll={false}` | Boolean | \- |
| [`prefetch`](https://nextjs.org/docs/app/api-reference/components/link#prefetch) | `prefetch={false}` | Boolean or null | \- |
| [`onNavigate`](https://nextjs.org/docs/app/api-reference/components/link#onnavigate) | `onNavigate={(e) => {}}` | Function | \- |

> **Good to know**: `<a>` tag attributes such as `className` or `target="_blank"` can be added to `<Link>` as props and will be passed to the underlying `<a>` element.

### [`href` (required)](https://nextjs.org/docs/app/api-reference/components/link#href-required)

The path or URL to navigate to.

```
<span><span>import</span><span> Link </span><span>from</span><span> </span><span>'next/link'</span></span>
<span> </span>
<span><span>// Navigate to /about?name=test</span></span>
<span><span>export</span><span> </span><span>default</span><span> </span><span>function</span><span> </span><span>Page</span><span>() {</span></span>
<span><span>  </span><span>return</span><span> (</span></span>
<span><span>    &lt;</span><span>Link</span></span>
<span><span>      </span><span>href</span><span>=</span><span>{{</span></span>
<span><span>        pathname</span><span>:</span><span> </span><span>'/about'</span><span>,</span></span>
<span><span>        query</span><span>:</span><span> { name</span><span>:</span><span> </span><span>'test'</span><span> }</span><span>,</span></span>
<span><span>      }}</span></span>
<span><span>    &gt;</span></span>
<span><span>      About</span></span>
<span><span>    &lt;/</span><span>Link</span><span>&gt;</span></span>
<span><span>  )</span></span>
<span><span>}</span></span>
```

### [`replace`](https://nextjs.org/docs/app/api-reference/components/link#replace)

**Defaults to `false`.** When `true`, `next/link` will replace the current history state instead of adding a new URL into the [browser's history](https://developer.mozilla.org/docs/Web/API/History_API) stack.

```
<span><span>import</span><span> Link </span><span>from</span><span> </span><span>'next/link'</span></span>
<span> </span>
<span><span>export</span><span> </span><span>default</span><span> </span><span>function</span><span> </span><span>Page</span><span>() {</span></span>
<span><span>  </span><span>return</span><span> (</span></span>
<span><span>    &lt;</span><span>Link</span><span> </span><span>href</span><span>=</span><span>"/dashboard"</span><span> </span><span>replace</span><span>&gt;</span></span>
<span><span>      Dashboard</span></span>
<span><span>    &lt;/</span><span>Link</span><span>&gt;</span></span>
<span><span>  )</span></span>
<span><span>}</span></span>
```

### [`scroll`](https://nextjs.org/docs/app/api-reference/components/link#scroll)

**Defaults to `true`.** The default scrolling behavior of `<Link>` in Next.js **is to maintain scroll position**, similar to how browsers handle back and forwards navigation. When you navigate to a new [Page](https://nextjs.org/docs/app/api-reference/file-conventions/page), scroll position will stay the same as long as the Page is visible in the viewport. However, if the Page is not visible in the viewport, Next.js will scroll to the top of the first Page element.

When `scroll = {false}`, Next.js will not attempt to scroll to the first Page element.

> **Good to know**: Next.js checks if `scroll: false` before managing scroll behavior. If scrolling is enabled, it identifies the relevant DOM node for navigation and inspects each top-level element. All non-scrollable elements and those without rendered HTML are bypassed, this includes sticky or fixed positioned elements, and non-visible elements such as those calculated with `getBoundingClientRect`. Next.js then continues through siblings until it identifies a scrollable element that is visible in the viewport.

```
<span><span>import</span><span> Link </span><span>from</span><span> </span><span>'next/link'</span></span>
<span> </span>
<span><span>export</span><span> </span><span>default</span><span> </span><span>function</span><span> </span><span>Page</span><span>() {</span></span>
<span><span>  </span><span>return</span><span> (</span></span>
<span><span>    &lt;</span><span>Link</span><span> </span><span>href</span><span>=</span><span>"/dashboard"</span><span> </span><span>scroll</span><span>=</span><span>{</span><span>false</span><span>}&gt;</span></span>
<span><span>      Dashboard</span></span>
<span><span>    &lt;/</span><span>Link</span><span>&gt;</span></span>
<span><span>  )</span></span>
<span><span>}</span></span>
```

### [`prefetch`](https://nextjs.org/docs/app/api-reference/components/link#prefetch)

Prefetching happens when a `<Link />` component enters the user's viewport (initially or through scroll). Next.js prefetches and loads the linked route (denoted by the `href`) and its data in the background to improve the performance of client-side navigations. If the prefetched data has expired by the time the user hovers over a `<Link />`, Next.js will attempt to prefetch it again. **Prefetching is only enabled in production**.

The following values can be passed to the `prefetch` prop:

-   **`null` (default)**: Prefetch behavior depends on whether the route is static or dynamic. For static routes, the full route will be prefetched (including all its data). For dynamic routes, the partial route down to the nearest segment with a [`loading.js`](https://nextjs.org/docs/app/building-your-application/routing/loading-ui-and-streaming#instant-loading-states) boundary will be prefetched.
-   `true`: The full route will be prefetched for both static and dynamic routes.
-   `false`: Prefetching will never happen both on entering the viewport and on hover.

```
<span><span>import</span><span> Link </span><span>from</span><span> </span><span>'next/link'</span></span>
<span> </span>
<span><span>export</span><span> </span><span>default</span><span> </span><span>function</span><span> </span><span>Page</span><span>() {</span></span>
<span><span>  </span><span>return</span><span> (</span></span>
<span><span>    &lt;</span><span>Link</span><span> </span><span>href</span><span>=</span><span>"/dashboard"</span><span> </span><span>prefetch</span><span>=</span><span>{</span><span>false</span><span>}&gt;</span></span>
<span><span>      Dashboard</span></span>
<span><span>    &lt;/</span><span>Link</span><span>&gt;</span></span>
<span><span>  )</span></span>
<span><span>}</span></span>
```

### [`onNavigate`](https://nextjs.org/docs/app/api-reference/components/link#onnavigate)

An event handler called during client-side navigation. The handler receives an event object that includes a `preventDefault()` method, allowing you to cancel the navigation if needed.

```
<span><span>import</span><span> Link </span><span>from</span><span> </span><span>'next/link'</span></span>
<span> </span>
<span><span>export</span><span> </span><span>default</span><span> </span><span>function</span><span> </span><span>Page</span><span>() {</span></span>
<span><span>  </span><span>return</span><span> (</span></span>
<span><span>    &lt;</span><span>Link</span></span>
<span><span>      </span><span>href</span><span>=</span><span>"/dashboard"</span></span>
<span><span>      </span><span>onNavigate</span><span>=</span><span>{(e) </span><span>=&gt;</span><span> {</span></span>
<span><span>        </span><span>// Only executes during SPA navigation</span></span>
<span><span>        </span><span>console</span><span>.log</span><span>(</span><span>'Navigating...'</span><span>)</span></span>
<span> </span>
<span><span>        </span><span>// Optionally prevent navigation</span></span>
<span><span>        </span><span>// e.preventDefault()</span></span>
<span><span>      }}</span></span>
<span><span>    &gt;</span></span>
<span><span>      Dashboard</span></span>
<span><span>    &lt;/</span><span>Link</span><span>&gt;</span></span>
<span><span>  )</span></span>
<span><span>}</span></span>
```

> **Good to know**: While `onClick` and `onNavigate` may seem similar, they serve different purposes. `onClick` executes for all click events, while `onNavigate` only runs during client-side navigation. Some key differences:
> 
> -   When using modifier keys (`Ctrl`/`Cmd` + Click), `onClick` executes but `onNavigate` doesn't since Next.js prevents default navigation for new tabs.
> -   External URLs won't trigger `onNavigate` since it's only for client-side and same-origin navigations.
> -   Links with the `download` attribute will work with `onClick` but not `onNavigate` since the browser will treat the linked URL as a download.

## [Examples](https://nextjs.org/docs/app/api-reference/components/link#examples)

The following examples demonstrate how to use the `<Link>` component in different scenarios.

### [Linking to dynamic segments](https://nextjs.org/docs/app/api-reference/components/link#linking-to-dynamic-segments)

When linking to [dynamic segments](https://nextjs.org/docs/app/building-your-application/routing/dynamic-routes), you can use [template literals and interpolation](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Template_literals) to generate a list of links. For example, to generate a list of blog posts:

```
<span><span>import</span><span> Link </span><span>from</span><span> </span><span>'next/link'</span></span>
<span> </span>
<span><span>interface</span><span> </span><span>Post</span><span> {</span></span>
<span><span>  id</span><span>:</span><span> </span><span>number</span></span>
<span><span>  title</span><span>:</span><span> </span><span>string</span></span>
<span><span>  slug</span><span>:</span><span> </span><span>string</span></span>
<span><span>}</span></span>
<span> </span>
<span><span>export</span><span> </span><span>default</span><span> </span><span>function</span><span> </span><span>PostList</span><span>({ posts }</span><span>:</span><span> { posts</span><span>:</span><span> </span><span>Post</span><span>[] }) {</span></span>
<span><span>  </span><span>return</span><span> (</span></span>
<span><span>    &lt;</span><span>ul</span><span>&gt;</span></span>
<span><span>      {</span><span>posts</span><span>.map</span><span>((post) </span><span>=&gt;</span><span> (</span></span>
<span><span>        &lt;</span><span>li</span><span> </span><span>key</span><span>=</span><span>{</span><span>post</span><span>.id}&gt;</span></span>
<span><span>          &lt;</span><span>Link</span><span> </span><span>href</span><span>=</span><span>{</span><span>`/</span><span>blog</span><span>/</span><span>${</span><span>post</span><span>.slug</span><span>}</span><span>`</span><span>}&gt;{</span><span>post</span><span>.title}&lt;/</span><span>Link</span><span>&gt;</span></span>
<span><span>        &lt;/</span><span>li</span><span>&gt;</span></span>
<span><span>      ))}</span></span>
<span><span>    &lt;/</span><span>ul</span><span>&gt;</span></span>
<span><span>  )</span></span>
<span><span>}</span></span>
```

### [Checking active links](https://nextjs.org/docs/app/api-reference/components/link#checking-active-links)

You can use [`usePathname()`](https://nextjs.org/docs/app/api-reference/functions/use-pathname) to determine if a link is active. For example, to add a class to the active link, you can check if the current `pathname` matches the `href` of the link:

```
<span><span>'use client'</span></span>
<span> </span>
<span><span>import</span><span> { usePathname } </span><span>from</span><span> </span><span>'next/navigation'</span></span>
<span><span>import</span><span> Link </span><span>from</span><span> </span><span>'next/link'</span></span>
<span> </span>
<span><span>export</span><span> </span><span>function</span><span> </span><span>Links</span><span>() {</span></span>
<span><span>  </span><span>const</span><span> </span><span>pathname</span><span> </span><span>=</span><span> </span><span>usePathname</span><span>()</span></span>
<span> </span>
<span><span>  </span><span>return</span><span> (</span></span>
<span><span>    &lt;</span><span>nav</span><span>&gt;</span></span>
<span><span>      &lt;</span><span>Link</span><span> </span><span>className</span><span>=</span><span>{</span><span>`link </span><span>${</span><span>pathname </span><span>===</span><span> </span><span>'/'</span><span> </span><span>?</span><span> </span><span>'active'</span><span> </span><span>:</span><span> </span><span>''</span><span>}</span><span>`</span><span>} </span><span>href</span><span>=</span><span>"/"</span><span>&gt;</span></span>
<span><span>        Home</span></span>
<span><span>      &lt;/</span><span>Link</span><span>&gt;</span></span>
<span> </span>
<span><span>      &lt;</span><span>Link</span></span>
<span><span>        </span><span>className</span><span>=</span><span>{</span><span>`link </span><span>${</span><span>pathname </span><span>===</span><span> </span><span>'/about'</span><span> </span><span>?</span><span> </span><span>'active'</span><span> </span><span>:</span><span> </span><span>''</span><span>}</span><span>`</span><span>}</span></span>
<span><span>        </span><span>href</span><span>=</span><span>"/about"</span></span>
<span><span>      &gt;</span></span>
<span><span>        About</span></span>
<span><span>      &lt;/</span><span>Link</span><span>&gt;</span></span>
<span><span>    &lt;/</span><span>nav</span><span>&gt;</span></span>
<span><span>  )</span></span>
<span><span>}</span></span>
```

### [Scrolling to an `id`](https://nextjs.org/docs/app/api-reference/components/link#scrolling-to-an-id)

If you'd like to scroll to a specific `id` on navigation, you can append your URL with a `#` hash link or just pass a hash link to the `href` prop. This is possible since `<Link>` renders to an `<a>` element.

```
<span><span>&lt;</span><span>Link</span><span> </span><span>href</span><span>=</span><span>"/dashboard#settings"</span><span>&gt;Settings&lt;/</span><span>Link</span><span>&gt;</span></span>
<span> </span>
<span><span>// Output</span></span>
<span><span>&lt;</span><span>a</span><span> </span><span>href</span><span>=</span><span>"/dashboard#settings"</span><span>&gt;Settings&lt;/</span><span>a</span><span>&gt;</span></span>
```

> **Good to know**:
> 
> -   Next.js will scroll to the [Page](https://nextjs.org/docs/app/api-reference/file-conventions/page) if it is not visible in the viewport upon navigation.

### [Linking to dynamic route segments](https://nextjs.org/docs/app/api-reference/components/link#linking-to-dynamic-route-segments)

For [dynamic route segments](https://nextjs.org/docs/app/building-your-application/routing/dynamic-routes), it can be handy to use template literals to create the link's path.

For example, you can generate a list of links to the dynamic route `app/blog/[slug]/page.js`:

```
<span><span>import</span><span> Link </span><span>from</span><span> </span><span>'next/link'</span></span>
<span> </span>
<span><span>export</span><span> </span><span>default</span><span> </span><span>function</span><span> </span><span>Page</span><span>({ posts }) {</span></span>
<span><span>  </span><span>return</span><span> (</span></span>
<span><span>    &lt;</span><span>ul</span><span>&gt;</span></span>
<span><span>      {</span><span>posts</span><span>.map</span><span>((post) </span><span>=&gt;</span><span> (</span></span>
<span><span>        &lt;</span><span>li</span><span> </span><span>key</span><span>=</span><span>{</span><span>post</span><span>.id}&gt;</span></span>
<span><span>          &lt;</span><span>Link</span><span> </span><span>href</span><span>=</span><span>{</span><span>`/</span><span>blog</span><span>/</span><span>${</span><span>post</span><span>.slug</span><span>}</span><span>`</span><span>}&gt;{</span><span>post</span><span>.title}&lt;/</span><span>Link</span><span>&gt;</span></span>
<span><span>        &lt;/</span><span>li</span><span>&gt;</span></span>
<span><span>      ))}</span></span>
<span><span>    &lt;/</span><span>ul</span><span>&gt;</span></span>
<span><span>  )</span></span>
<span><span>}</span></span>
```

### [If the child is a custom component that wraps an `<a>` tag](https://nextjs.org/docs/app/api-reference/components/link#if-the-child-is-a-custom-component-that-wraps-an-a-tag)

If the child of `Link` is a custom component that wraps an `<a>` tag, you must add `passHref` to `Link`. This is necessary if you’re using libraries like [styled-components](https://styled-components.com/). Without this, the `<a>` tag will not have the `href` attribute, which hurts your site's accessibility and might affect SEO. If you're using [ESLint](https://nextjs.org/docs/pages/api-reference/config/eslint), there is a built-in rule `next/link-passhref` to ensure correct usage of `passHref`.

```
<span><span>import</span><span> Link </span><span>from</span><span> </span><span>'next/link'</span></span>
<span><span>import</span><span> styled </span><span>from</span><span> </span><span>'styled-components'</span></span>
<span> </span>
<span><span>// This creates a custom component that wraps an &lt;a&gt; tag</span></span>
<span><span>const</span><span> </span><span>RedLink</span><span> </span><span>=</span><span> </span><span>styled</span><span>.</span><span>a</span><span>`</span></span>
<span><span>  color: red;</span></span>
<span><span>`</span></span>
<span> </span>
<span><span>function</span><span> </span><span>NavLink</span><span>({ href</span><span>,</span><span> name }) {</span></span>
<span><span>  </span><span>return</span><span> (</span></span>
<span><span>    &lt;</span><span>Link</span><span> </span><span>href</span><span>=</span><span>{href} </span><span>passHref</span><span> </span><span>legacyBehavior</span><span>&gt;</span></span>
<span><span>      &lt;</span><span>RedLink</span><span>&gt;{name}&lt;/</span><span>RedLink</span><span>&gt;</span></span>
<span><span>    &lt;/</span><span>Link</span><span>&gt;</span></span>
<span><span>  )</span></span>
<span><span>}</span></span>
<span> </span>
<span><span>export</span><span> </span><span>default</span><span> NavLink</span></span>
```

-   If you’re using [emotion](https://emotion.sh/)’s JSX pragma feature (`@jsx jsx`), you must use `passHref` even if you use an `<a>` tag directly.
-   The component should support `onClick` property to trigger navigation correctly.

### [Nesting a functional component](https://nextjs.org/docs/app/api-reference/components/link#nesting-a-functional-component)

If the child of `Link` is a functional component, in addition to using `passHref` and `legacyBehavior`, you must wrap the component in [`React.forwardRef`](https://react.dev/reference/react/forwardRef):

```
<span><span>import</span><span> Link </span><span>from</span><span> </span><span>'next/link'</span></span>
<span><span>import</span><span> React </span><span>from</span><span> </span><span>'react'</span></span>
<span> </span>
<span><span>// Define the props type for MyButton</span></span>
<span><span>interface</span><span> </span><span>MyButtonProps</span><span> {</span></span>
<span><span>  onClick</span><span>?:</span><span> </span><span>React</span><span>.</span><span>MouseEventHandler</span><span>&lt;</span><span>HTMLAnchorElement</span><span>&gt;</span></span>
<span><span>  href</span><span>?:</span><span> </span><span>string</span></span>
<span><span>}</span></span>
<span> </span>
<span><span>// Use React.ForwardRefRenderFunction to properly type the forwarded ref</span></span>
<span><span>const</span><span> </span><span>MyButton</span><span>:</span><span> </span><span>React</span><span>.</span><span>ForwardRefRenderFunction</span><span>&lt;</span></span>
<span><span>  </span><span>HTMLAnchorElement</span><span>,</span></span>
<span><span>  </span><span>MyButtonProps</span></span>
<span><span>&gt; </span><span>=</span><span> ({ onClick</span><span>,</span><span> href }</span><span>,</span><span> ref) </span><span>=&gt;</span><span> {</span></span>
<span><span>  </span><span>return</span><span> (</span></span>
<span><span>    &lt;</span><span>a</span><span> </span><span>href</span><span>=</span><span>{href} </span><span>onClick</span><span>=</span><span>{onClick} </span><span>ref</span><span>=</span><span>{ref}&gt;</span></span>
<span><span>      Click Me</span></span>
<span><span>    &lt;/</span><span>a</span><span>&gt;</span></span>
<span><span>  )</span></span>
<span><span>}</span></span>
<span> </span>
<span><span>// Use React.forwardRef to wrap the component</span></span>
<span><span>const</span><span> </span><span>ForwardedMyButton</span><span> </span><span>=</span><span> </span><span>React</span><span>.forwardRef</span><span>(MyButton)</span></span>
<span> </span>
<span><span>export</span><span> </span><span>default</span><span> </span><span>function</span><span> </span><span>Page</span><span>() {</span></span>
<span><span>  </span><span>return</span><span> (</span></span>
<span><span>    &lt;</span><span>Link</span><span> </span><span>href</span><span>=</span><span>"/about"</span><span> </span><span>passHref</span><span> </span><span>legacyBehavior</span><span>&gt;</span></span>
<span><span>      &lt;</span><span>ForwardedMyButton</span><span> /&gt;</span></span>
<span><span>    &lt;/</span><span>Link</span><span>&gt;</span></span>
<span><span>  )</span></span>
<span><span>}</span></span>
```

### [Replace the URL instead of push](https://nextjs.org/docs/app/api-reference/components/link#replace-the-url-instead-of-push)

The default behavior of the `Link` component is to `push` a new URL into the `history` stack. You can use the `replace` prop to prevent adding a new entry, as in the following example:

```
<span><span>import</span><span> Link </span><span>from</span><span> </span><span>'next/link'</span></span>
<span> </span>
<span><span>export</span><span> </span><span>default</span><span> </span><span>function</span><span> </span><span>Page</span><span>() {</span></span>
<span><span>  </span><span>return</span><span> (</span></span>
<span><span>    &lt;</span><span>Link</span><span> </span><span>href</span><span>=</span><span>"/about"</span><span> </span><span>replace</span><span>&gt;</span></span>
<span><span>      About us</span></span>
<span><span>    &lt;/</span><span>Link</span><span>&gt;</span></span>
<span><span>  )</span></span>
<span><span>}</span></span>
```

### [Disable scrolling to the top of the page](https://nextjs.org/docs/app/api-reference/components/link#disable-scrolling-to-the-top-of-the-page)

The default scrolling behavior of `<Link>` in Next.js **is to maintain scroll position**, similar to how browsers handle back and forwards navigation. When you navigate to a new [Page](https://nextjs.org/docs/app/api-reference/file-conventions/page), scroll position will stay the same as long as the Page is visible in the viewport.

However, if the Page is not visible in the viewport, Next.js will scroll to the top of the first Page element. If you'd like to disable this behavior, you can pass `scroll={false}` to the `<Link>` component, or `scroll: false` to `router.push()` or `router.replace()`.

```
<span><span>import</span><span> Link </span><span>from</span><span> </span><span>'next/link'</span></span>
<span> </span>
<span><span>export</span><span> </span><span>default</span><span> </span><span>function</span><span> </span><span>Page</span><span>() {</span></span>
<span><span>  </span><span>return</span><span> (</span></span>
<span><span>    &lt;</span><span>Link</span><span> </span><span>href</span><span>=</span><span>"/#hashid"</span><span> </span><span>scroll</span><span>=</span><span>{</span><span>false</span><span>}&gt;</span></span>
<span><span>      Disables scrolling to the top</span></span>
<span><span>    &lt;/</span><span>Link</span><span>&gt;</span></span>
<span><span>  )</span></span>
<span><span>}</span></span>
```

Using `router.push()` or `router.replace()`:

```
<span><span>// useRouter</span></span>
<span><span>import</span><span> { useRouter } </span><span>from</span><span> </span><span>'next/navigation'</span></span>
<span> </span>
<span><span>const</span><span> </span><span>router</span><span> </span><span>=</span><span> </span><span>useRouter</span><span>()</span></span>
<span> </span>
<span><span>router</span><span>.push</span><span>(</span><span>'/dashboard'</span><span>,</span><span> { scroll</span><span>:</span><span> </span><span>false</span><span> })</span></span>
```

### [Prefetching links in Middleware](https://nextjs.org/docs/app/api-reference/components/link#prefetching-links-in-middleware)

It's common to use [Middleware](https://nextjs.org/docs/app/building-your-application/routing/middleware) for authentication or other purposes that involve rewriting the user to a different page. In order for the `<Link />` component to properly prefetch links with rewrites via Middleware, you need to tell Next.js both the URL to display and the URL to prefetch. This is required to avoid un-necessary fetches to middleware to know the correct route to prefetch.

For example, if you want to serve a `/dashboard` route that has authenticated and visitor views, you can add the following in your Middleware to redirect the user to the correct page:

```
<span><span>import</span><span> { NextResponse } </span><span>from</span><span> </span><span>'next/server'</span></span>
<span> </span>
<span><span>export</span><span> </span><span>function</span><span> </span><span>middleware</span><span>(request</span><span>:</span><span> </span><span>Request</span><span>) {</span></span>
<span><span>  </span><span>const</span><span> </span><span>nextUrl</span><span> </span><span>=</span><span> </span><span>request</span><span>.nextUrl</span></span>
<span><span>  </span><span>if</span><span> (</span><span>nextUrl</span><span>.pathname </span><span>===</span><span> </span><span>'/dashboard'</span><span>) {</span></span>
<span><span>    </span><span>if</span><span> (</span><span>request</span><span>.</span><span>cookies</span><span>.authToken) {</span></span>
<span><span>      </span><span>return</span><span> </span><span>NextResponse</span><span>.rewrite</span><span>(</span><span>new</span><span> </span><span>URL</span><span>(</span><span>'/auth/dashboard'</span><span>,</span><span> </span><span>request</span><span>.url))</span></span>
<span><span>    } </span><span>else</span><span> {</span></span>
<span><span>      </span><span>return</span><span> </span><span>NextResponse</span><span>.rewrite</span><span>(</span><span>new</span><span> </span><span>URL</span><span>(</span><span>'/public/dashboard'</span><span>,</span><span> </span><span>request</span><span>.url))</span></span>
<span><span>    }</span></span>
<span><span>  }</span></span>
<span><span>}</span></span>
```

In this case, you would want to use the following code in your `<Link />` component:

```
<span><span>'use client'</span></span>
<span> </span>
<span><span>import</span><span> Link </span><span>from</span><span> </span><span>'next/link'</span></span>
<span><span>import</span><span> useIsAuthed </span><span>from</span><span> </span><span>'./hooks/useIsAuthed'</span><span> </span><span>// Your auth hook</span></span>
<span> </span>
<span><span>export</span><span> </span><span>default</span><span> </span><span>function</span><span> </span><span>Page</span><span>() {</span></span>
<span><span>  </span><span>const</span><span> </span><span>isAuthed</span><span> </span><span>=</span><span> </span><span>useIsAuthed</span><span>()</span></span>
<span><span>  </span><span>const</span><span> </span><span>path</span><span> </span><span>=</span><span> isAuthed </span><span>?</span><span> </span><span>'/auth/dashboard'</span><span> </span><span>:</span><span> </span><span>'/public/dashboard'</span></span>
<span><span>  </span><span>return</span><span> (</span></span>
<span><span>    &lt;</span><span>Link</span><span> </span><span>as</span><span>=</span><span>"/dashboard"</span><span> </span><span>href</span><span>=</span><span>{path}&gt;</span></span>
<span><span>      Dashboard</span></span>
<span><span>    &lt;/</span><span>Link</span><span>&gt;</span></span>
<span><span>  )</span></span>
<span><span>}</span></span>
```

### [Blocking navigation](https://nextjs.org/docs/app/api-reference/components/link#blocking-navigation)

You can use the `onNavigate` prop to block navigation when certain conditions are met, such as when a form has unsaved changes. When you need to block navigation across multiple components in your app (like preventing navigation from any link while a form is being edited), React Context provides a clean way to share this blocking state. First, create a context to track the navigation blocking state:

```
<span><span>'use client'</span></span>
<span> </span>
<span><span>import</span><span> { createContext</span><span>,</span><span> useState</span><span>,</span><span> useContext } </span><span>from</span><span> </span><span>'react'</span></span>
<span> </span>
<span><span>interface</span><span> </span><span>NavigationBlockerContextType</span><span> {</span></span>
<span><span>  isBlocked</span><span>:</span><span> </span><span>boolean</span></span>
<span><span>  </span><span>setIsBlocked</span><span>:</span><span> (isBlocked</span><span>:</span><span> </span><span>boolean</span><span>) </span><span>=&gt;</span><span> </span><span>void</span></span>
<span><span>}</span></span>
<span> </span>
<span><span>export</span><span> </span><span>const</span><span> </span><span>NavigationBlockerContext</span><span> </span><span>=</span></span>
<span><span>  </span><span>createContext</span><span>&lt;</span><span>NavigationBlockerContextType</span><span>&gt;({</span></span>
<span><span>    isBlocked</span><span>:</span><span> </span><span>false</span><span>,</span></span>
<span><span>    </span><span>setIsBlocked</span><span>:</span><span> () </span><span>=&gt;</span><span> {}</span><span>,</span></span>
<span><span>  })</span></span>
<span> </span>
<span><span>export</span><span> </span><span>function</span><span> </span><span>NavigationBlockerProvider</span><span>({</span></span>
<span><span>  children</span><span>,</span></span>
<span><span>}</span><span>:</span><span> {</span></span>
<span><span>  children</span><span>:</span><span> </span><span>React</span><span>.</span><span>ReactNode</span></span>
<span><span>}) {</span></span>
<span><span>  </span><span>const</span><span> [</span><span>isBlocked</span><span>,</span><span> </span><span>setIsBlocked</span><span>] </span><span>=</span><span> </span><span>useState</span><span>(</span><span>false</span><span>)</span></span>
<span> </span>
<span><span>  </span><span>return</span><span> (</span></span>
<span><span>    &lt;</span><span>NavigationBlockerContext.Provider</span><span> </span><span>value</span><span>=</span><span>{{ isBlocked</span><span>,</span><span> setIsBlocked }}&gt;</span></span>
<span><span>      {children}</span></span>
<span><span>    &lt;/</span><span>NavigationBlockerContext.Provider</span><span>&gt;</span></span>
<span><span>  )</span></span>
<span><span>}</span></span>
<span> </span>
<span><span>export</span><span> </span><span>function</span><span> </span><span>useNavigationBlocker</span><span>() {</span></span>
<span><span>  </span><span>return</span><span> </span><span>useContext</span><span>(NavigationBlockerContext)</span></span>
<span><span>}</span></span>
```

Create a form component that uses the context:

```
<span><span>'use client'</span></span>
<span> </span>
<span><span>import</span><span> { useNavigationBlocker } </span><span>from</span><span> </span><span>'../contexts/navigation-blocker'</span></span>
<span> </span>
<span><span>export</span><span> </span><span>default</span><span> </span><span>function</span><span> </span><span>Form</span><span>() {</span></span>
<span><span>  </span><span>const</span><span> { </span><span>setIsBlocked</span><span> } </span><span>=</span><span> </span><span>useNavigationBlocker</span><span>()</span></span>
<span> </span>
<span><span>  </span><span>return</span><span> (</span></span>
<span><span>    &lt;</span><span>form</span></span>
<span><span>      </span><span>onSubmit</span><span>=</span><span>{(e) </span><span>=&gt;</span><span> {</span></span>
<span><span>        </span><span>e</span><span>.preventDefault</span><span>()</span></span>
<span><span>        </span><span>setIsBlocked</span><span>(</span><span>false</span><span>)</span></span>
<span><span>      }}</span></span>
<span><span>      </span><span>onChange</span><span>=</span><span>{() </span><span>=&gt;</span><span> </span><span>setIsBlocked</span><span>(</span><span>true</span><span>)}</span></span>
<span><span>    &gt;</span></span>
<span><span>      &lt;</span><span>input</span><span> </span><span>type</span><span>=</span><span>"text"</span><span> </span><span>name</span><span>=</span><span>"name"</span><span> /&gt;</span></span>
<span><span>      &lt;</span><span>button</span><span> </span><span>type</span><span>=</span><span>"submit"</span><span>&gt;Save&lt;/</span><span>button</span><span>&gt;</span></span>
<span><span>    &lt;/</span><span>form</span><span>&gt;</span></span>
<span><span>  )</span></span>
<span><span>}</span></span>
```

Create a custom Link component that blocks navigation:

```
<span><span>'use client'</span></span>
<span> </span>
<span><span>import</span><span> Link </span><span>from</span><span> </span><span>'next/link'</span></span>
<span><span>import</span><span> { useNavigationBlocker } </span><span>from</span><span> </span><span>'../contexts/navigation-blocker'</span></span>
<span> </span>
<span><span>interface</span><span> </span><span>CustomLinkProps</span><span> </span><span>extends</span><span> </span><span>React</span><span>.</span><span>ComponentProps</span><span>&lt;</span><span>typeof</span><span> Link&gt; {</span></span>
<span><span>  children</span><span>:</span><span> </span><span>React</span><span>.</span><span>ReactNode</span></span>
<span><span>}</span></span>
<span> </span>
<span><span>export</span><span> </span><span>function</span><span> </span><span>CustomLink</span><span>({ children</span><span>,</span><span> </span><span>...</span><span>props }</span><span>:</span><span> </span><span>CustomLinkProps</span><span>) {</span></span>
<span><span>  </span><span>const</span><span> { </span><span>isBlocked</span><span> } </span><span>=</span><span> </span><span>useNavigationBlocker</span><span>()</span></span>
<span> </span>
<span><span>  </span><span>return</span><span> (</span></span>
<span><span>    &lt;</span><span>Link</span></span>
<span><span>      </span><span>onNavigate</span><span>=</span><span>{(e) </span><span>=&gt;</span><span> {</span></span>
<span><span>        </span><span>if</span><span> (</span></span>
<span><span>          isBlocked </span><span>&amp;&amp;</span></span>
<span><span>          </span><span>!</span><span>window</span><span>.confirm</span><span>(</span><span>'You have unsaved changes. Leave anyway?'</span><span>)</span></span>
<span><span>        ) {</span></span>
<span><span>          </span><span>e</span><span>.preventDefault</span><span>()</span></span>
<span><span>        }</span></span>
<span><span>      }}</span></span>
<span><span>      {</span><span>...</span><span>props}</span></span>
<span><span>    &gt;</span></span>
<span><span>      {children}</span></span>
<span><span>    &lt;/</span><span>Link</span><span>&gt;</span></span>
<span><span>  )</span></span>
<span><span>}</span></span>
```

Create a navigation component:

```
<span><span>'use client'</span></span>
<span> </span>
<span><span>import</span><span> { CustomLink </span><span>as</span><span> Link } </span><span>from</span><span> </span><span>'./custom-link'</span></span>
<span> </span>
<span><span>export</span><span> </span><span>default</span><span> </span><span>function</span><span> </span><span>Nav</span><span>() {</span></span>
<span><span>  </span><span>return</span><span> (</span></span>
<span><span>    &lt;</span><span>nav</span><span>&gt;</span></span>
<span><span>      &lt;</span><span>Link</span><span> </span><span>href</span><span>=</span><span>"/"</span><span>&gt;Home&lt;/</span><span>Link</span><span>&gt;</span></span>
<span><span>      &lt;</span><span>Link</span><span> </span><span>href</span><span>=</span><span>"/about"</span><span>&gt;About&lt;/</span><span>Link</span><span>&gt;</span></span>
<span><span>    &lt;/</span><span>nav</span><span>&gt;</span></span>
<span><span>  )</span></span>
<span><span>}</span></span>
```

Finally, wrap your app with the `NavigationBlockerProvider` in the root layout and use the components in your page:

```
<span><span>import</span><span> { NavigationBlockerProvider } </span><span>from</span><span> </span><span>'./contexts/navigation-blocker'</span></span>
<span> </span>
<span><span>export</span><span> </span><span>default</span><span> </span><span>function</span><span> </span><span>RootLayout</span><span>({</span></span>
<span><span>  children</span><span>,</span></span>
<span><span>}</span><span>:</span><span> {</span></span>
<span><span>  children</span><span>:</span><span> </span><span>React</span><span>.</span><span>ReactNode</span></span>
<span><span>}) {</span></span>
<span><span>  </span><span>return</span><span> (</span></span>
<span><span>    &lt;</span><span>html</span><span> </span><span>lang</span><span>=</span><span>"en"</span><span>&gt;</span></span>
<span><span>      &lt;</span><span>body</span><span>&gt;</span></span>
<span><span>        &lt;</span><span>NavigationBlockerProvider</span><span>&gt;{children}&lt;/</span><span>NavigationBlockerProvider</span><span>&gt;</span></span>
<span><span>      &lt;/</span><span>body</span><span>&gt;</span></span>
<span><span>    &lt;/</span><span>html</span><span>&gt;</span></span>
<span><span>  )</span></span>
<span><span>}</span></span>
```

Then, use the `Nav` and `Form` components in your page:

```
<span><span>import</span><span> Nav </span><span>from</span><span> </span><span>'./components/nav'</span></span>
<span><span>import</span><span> Form </span><span>from</span><span> </span><span>'./components/form'</span></span>
<span> </span>
<span><span>export</span><span> </span><span>default</span><span> </span><span>function</span><span> </span><span>Page</span><span>() {</span></span>
<span><span>  </span><span>return</span><span> (</span></span>
<span><span>    &lt;</span><span>div</span><span>&gt;</span></span>
<span><span>      &lt;</span><span>Nav</span><span> /&gt;</span></span>
<span><span>      &lt;</span><span>main</span><span>&gt;</span></span>
<span><span>        &lt;</span><span>h1</span><span>&gt;Welcome to the Dashboard&lt;/</span><span>h1</span><span>&gt;</span></span>
<span><span>        &lt;</span><span>Form</span><span> /&gt;</span></span>
<span><span>      &lt;/</span><span>main</span><span>&gt;</span></span>
<span><span>    &lt;/</span><span>div</span><span>&gt;</span></span>
<span><span>  )</span></span>
<span><span>}</span></span>
```

When a user tries to navigate away using `CustomLink` while the form has unsaved changes, they'll be prompted to confirm before leaving.

## [Version history](https://nextjs.org/docs/app/api-reference/components/link#version-history)

| Version | Changes |
| --- | --- |
| `v15.3.0` | Add `onNavigate` API |
| `v13.0.0` | No longer requires a child `<a>` tag. A [codemod](https://nextjs.org/docs/app/guides/upgrading/codemods#remove-a-tags-from-link-components) is provided to automatically update your codebase. |
| `v10.0.0` | `href` props pointing to a dynamic route are automatically resolved and no longer require an `as` prop. |
| `v8.0.0` | Improved prefetching performance. |
| `v1.0.0` | `next/link` introduced. |