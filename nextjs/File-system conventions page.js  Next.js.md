The `page` file allows you to define UI that is **unique** to a route. You can create a page by default exporting a component from the file:

```
<span><span>export</span><span> </span><span>default</span><span> </span><span>function</span><span> </span><span>Page</span><span>({</span></span>
<span><span>  params</span><span>,</span></span>
<span><span>  searchParams</span><span>,</span></span>
<span><span>}</span><span>:</span><span> {</span></span>
<span><span>  params</span><span>:</span><span> </span><span>Promise</span><span>&lt;{ slug</span><span>:</span><span> </span><span>string</span><span> }&gt;</span></span>
<span><span>  searchParams</span><span>:</span><span> </span><span>Promise</span><span>&lt;{ [key</span><span>:</span><span> </span><span>string</span><span>]</span><span>:</span><span> </span><span>string</span><span> </span><span>|</span><span> </span><span>string</span><span>[] </span><span>|</span><span> </span><span>undefined</span><span> }&gt;</span></span>
<span><span>}) {</span></span>
<span><span>  </span><span>return</span><span> &lt;</span><span>h1</span><span>&gt;My Page&lt;/</span><span>h1</span><span>&gt;</span></span>
<span><span>}</span></span>
```

## [Good to know](https://nextjs.org/docs/app/api-reference/file-conventions/page#good-to-know)

-   The `.js`, `.jsx`, or `.tsx` file extensions can be used for `page`.
-   A `page` is always the **leaf** of the route subtree.
-   A `page` file is required to make a route segment **publicly accessible**.
-   Pages are [Server Components](https://react.dev/reference/rsc/server-components) by default, but can be set to a [Client Component](https://react.dev/reference/rsc/use-client).

## [Reference](https://nextjs.org/docs/app/api-reference/file-conventions/page#reference)

### [Props](https://nextjs.org/docs/app/api-reference/file-conventions/page#props)

#### [`params` (optional)](https://nextjs.org/docs/app/api-reference/file-conventions/page#params-optional)

A promise that resolves to an object containing the [dynamic route parameters](https://nextjs.org/docs/app/building-your-application/routing/dynamic-routes) from the root segment down to that page.

```
<span><span>export</span><span> </span><span>default</span><span> </span><span>async</span><span> </span><span>function</span><span> </span><span>Page</span><span>({</span></span>
<span><span>  params</span><span>,</span></span>
<span><span>}</span><span>:</span><span> {</span></span>
<span><span>  params</span><span>:</span><span> </span><span>Promise</span><span>&lt;{ slug</span><span>:</span><span> </span><span>string</span><span> }&gt;</span></span>
<span><span>}) {</span></span>
<span><span>  </span><span>const</span><span> { </span><span>slug</span><span> } </span><span>=</span><span> </span><span>await</span><span> params</span></span>
<span><span>}</span></span>
```

| Example Route | URL | `params` |
| --- | --- | --- |
| `app/shop/[slug]/page.js` | `/shop/1` | `Promise<{ slug: '1' }>` |
| `app/shop/[category]/[item]/page.js` | `/shop/1/2` | `Promise<{ category: '1', item: '2' }>` |
| `app/shop/[...slug]/page.js` | `/shop/1/2` | `Promise<{ slug: ['1', '2'] }>` |

-   Since the `params` prop is a promise. You must use `async/await` or React's [`use`](https://react.dev/reference/react/use) function to access the values.
    -   In version 14 and earlier, `params` was a synchronous prop. To help with backwards compatibility, you can still access it synchronously in Next.js 15, but this behavior will be deprecated in the future.

#### [`searchParams` (optional)](https://nextjs.org/docs/app/api-reference/file-conventions/page#searchparams-optional)

A promise that resolves to an object containing the [search parameters](https://developer.mozilla.org/docs/Learn/Common_questions/What_is_a_URL#parameters) of the current URL. For example:

```
<span><span>export</span><span> </span><span>default</span><span> </span><span>async</span><span> </span><span>function</span><span> </span><span>Page</span><span>({</span></span>
<span><span>  searchParams</span><span>,</span></span>
<span><span>}</span><span>:</span><span> {</span></span>
<span><span>  searchParams</span><span>:</span><span> </span><span>Promise</span><span>&lt;{ [key</span><span>:</span><span> </span><span>string</span><span>]</span><span>:</span><span> </span><span>string</span><span> </span><span>|</span><span> </span><span>string</span><span>[] </span><span>|</span><span> </span><span>undefined</span><span> }&gt;</span></span>
<span><span>}) {</span></span>
<span><span>  </span><span>const</span><span> </span><span>filters</span><span> </span><span>=</span><span> (</span><span>await</span><span> searchParams).filters</span></span>
<span><span>}</span></span>
```

| Example URL | `searchParams` |
| --- | --- |
| `/shop?a=1` | `Promise<{ a: '1' }>` |
| `/shop?a=1&b=2` | `Promise<{ a: '1', b: '2' }>` |
| `/shop?a=1&a=2` | `Promise<{ a: ['1', '2'] }>` |

-   Since the `searchParams` prop is a promise. You must use `async/await` or React's [`use`](https://react.dev/reference/react/use) function to access the values.
    -   In version 14 and earlier, `searchParams` was a synchronous prop. To help with backwards compatibility, you can still access it synchronously in Next.js 15, but this behavior will be deprecated in the future.
-   `searchParams` is a **[Dynamic API](https://nextjs.org/docs/app/building-your-application/rendering/server-components#dynamic-apis)** whose values cannot be known ahead of time. Using it will opt the page into **[dynamic rendering](https://nextjs.org/docs/app/building-your-application/rendering/server-components#dynamic-rendering)** at request time.
-   `searchParams` is a plain JavaScript object, not a `URLSearchParams` instance.

## [Examples](https://nextjs.org/docs/app/api-reference/file-conventions/page#examples)

### [Displaying content based on `params`](https://nextjs.org/docs/app/api-reference/file-conventions/page#displaying-content-based-on-params)

Using [dynamic route segments](https://nextjs.org/docs/app/building-your-application/routing/dynamic-routes), you can display or fetch specific content for the page based on the `params` prop.

```
<span><span>export</span><span> </span><span>default</span><span> </span><span>async</span><span> </span><span>function</span><span> </span><span>Page</span><span>({</span></span>
<span><span>  params</span><span>,</span></span>
<span><span>}</span><span>:</span><span> {</span></span>
<span><span>  params</span><span>:</span><span> </span><span>Promise</span><span>&lt;{ slug</span><span>:</span><span> </span><span>string</span><span> }&gt;</span></span>
<span><span>}) {</span></span>
<span><span>  </span><span>const</span><span> { </span><span>slug</span><span> } </span><span>=</span><span> </span><span>await</span><span> params</span></span>
<span><span>  </span><span>return</span><span> &lt;</span><span>h1</span><span>&gt;Blog Post: {slug}&lt;/</span><span>h1</span><span>&gt;</span></span>
<span><span>}</span></span>
```

### [Handling filtering with `searchParams`](https://nextjs.org/docs/app/api-reference/file-conventions/page#handling-filtering-with-searchparams)

You can use the `searchParams` prop to handle filtering, pagination, or sorting based on the query string of the URL.

```
<span><span>export</span><span> </span><span>default</span><span> </span><span>async</span><span> </span><span>function</span><span> </span><span>Page</span><span>({</span></span>
<span><span>  searchParams</span><span>,</span></span>
<span><span>}</span><span>:</span><span> {</span></span>
<span><span>  searchParams</span><span>:</span><span> </span><span>Promise</span><span>&lt;{ [key</span><span>:</span><span> </span><span>string</span><span>]</span><span>:</span><span> </span><span>string</span><span> </span><span>|</span><span> </span><span>string</span><span>[] </span><span>|</span><span> </span><span>undefined</span><span> }&gt;</span></span>
<span><span>}) {</span></span>
<span><span>  </span><span>const</span><span> { </span><span>page</span><span> </span><span>=</span><span> </span><span>'1'</span><span>,</span><span> </span><span>sort</span><span> </span><span>=</span><span> </span><span>'asc'</span><span>,</span><span> </span><span>query</span><span> </span><span>=</span><span> </span><span>''</span><span> } </span><span>=</span><span> </span><span>await</span><span> searchParams</span></span>
<span> </span>
<span><span>  </span><span>return</span><span> (</span></span>
<span><span>    &lt;</span><span>div</span><span>&gt;</span></span>
<span><span>      &lt;</span><span>h1</span><span>&gt;Product Listing&lt;/</span><span>h1</span><span>&gt;</span></span>
<span><span>      &lt;</span><span>p</span><span>&gt;Search query: {query}&lt;/</span><span>p</span><span>&gt;</span></span>
<span><span>      &lt;</span><span>p</span><span>&gt;Current page: {page}&lt;/</span><span>p</span><span>&gt;</span></span>
<span><span>      &lt;</span><span>p</span><span>&gt;Sort order: {sort}&lt;/</span><span>p</span><span>&gt;</span></span>
<span><span>    &lt;/</span><span>div</span><span>&gt;</span></span>
<span><span>  )</span></span>
<span><span>}</span></span>
```

### [Reading `searchParams` and `params` in Client Components](https://nextjs.org/docs/app/api-reference/file-conventions/page#reading-searchparams-and-params-in-client-components)

To use `searchParams` and `params` in a Client Component (which cannot be `async`), you can use React's [`use`](https://react.dev/reference/react/use) function to read the promise:

```
<span><span>'use client'</span></span>
<span> </span>
<span><span>import</span><span> { use } </span><span>from</span><span> </span><span>'react'</span></span>
<span> </span>
<span><span>export</span><span> </span><span>default</span><span> </span><span>function</span><span> </span><span>Page</span><span>({</span></span>
<span><span>  params</span><span>,</span></span>
<span><span>  searchParams</span><span>,</span></span>
<span><span>}</span><span>:</span><span> {</span></span>
<span><span>  params</span><span>:</span><span> </span><span>Promise</span><span>&lt;{ slug</span><span>:</span><span> </span><span>string</span><span> }&gt;</span></span>
<span><span>  searchParams</span><span>:</span><span> </span><span>Promise</span><span>&lt;{ [key</span><span>:</span><span> </span><span>string</span><span>]</span><span>:</span><span> </span><span>string</span><span> </span><span>|</span><span> </span><span>string</span><span>[] </span><span>|</span><span> </span><span>undefined</span><span> }&gt;</span></span>
<span><span>}) {</span></span>
<span><span>  </span><span>const</span><span> { </span><span>slug</span><span> } </span><span>=</span><span> </span><span>use</span><span>(params)</span></span>
<span><span>  </span><span>const</span><span> { </span><span>query</span><span> } </span><span>=</span><span> </span><span>use</span><span>(searchParams)</span></span>
<span><span>}</span></span>
```

## [Version History](https://nextjs.org/docs/app/api-reference/file-conventions/page#version-history)

| Version | Changes |
| --- | --- |
| `v15.0.0-RC` | `params` and `searchParams` are now promises. A [codemod](https://nextjs.org/docs/app/guides/upgrading/codemods#150) is available. |
| `v13.0.0` | `page` introduced. |