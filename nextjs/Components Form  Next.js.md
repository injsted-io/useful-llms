The `<Form>` component extends the HTML `<form>` element to provide [**prefetching**](https://nextjs.org/docs/app/building-your-application/routing/linking-and-navigating#2-prefetching) of [loading UI](https://nextjs.org/docs/app/building-your-application/routing/loading-ui-and-streaming), **client-side navigation** on submission, and **progressive enhancement**.

It's useful for forms that update URL search params as it reduces the boilerplate code needed to achieve the above.

Basic usage:

```
<span><span>import</span><span> Form </span><span>from</span><span> </span><span>'next/form'</span></span>
<span> </span>
<span><span>export</span><span> </span><span>default</span><span> </span><span>function</span><span> </span><span>Page</span><span>() {</span></span>
<span><span>  </span><span>return</span><span> (</span></span>
<span><span>    &lt;</span><span>Form</span><span> </span><span>action</span><span>=</span><span>"/search"</span><span>&gt;</span></span>
<span><span>      {</span><span>/* On submission, the input value will be </span><span>app</span><span>ended to</span></span>
<span><span>          the URL, e.g. /search?query=abc */</span><span>}</span></span>
<span><span>      &lt;</span><span>input</span><span> </span><span>name</span><span>=</span><span>"query"</span><span> /&gt;</span></span>
<span><span>      &lt;</span><span>button</span><span> </span><span>type</span><span>=</span><span>"submit"</span><span>&gt;Submit&lt;/</span><span>button</span><span>&gt;</span></span>
<span><span>    &lt;/</span><span>Form</span><span>&gt;</span></span>
<span><span>  )</span></span>
<span><span>}</span></span>
```

## [Reference](https://nextjs.org/docs/app/api-reference/components/form#reference)

The behavior of the `<Form>` component depends on whether the `action` prop is passed a `string` or `function`.

-   When `action` is a **string**, the `<Form>` behaves like a native HTML form that uses a **`GET`** method. The form data is encoded into the URL as search params, and when the form is submitted, it navigates to the specified URL. In addition, Next.js:
    -   [Prefetches](https://nextjs.org/docs/app/building-your-application/routing/linking-and-navigating#2-prefetching) the path when the form becomes visible, this preloads shared UI (e.g. `layout.js` and `loading.js`), resulting in faster navigation.
    -   Performs a [client-side navigation](https://nextjs.org/docs/app/building-your-application/routing/linking-and-navigating#5-soft-navigation) instead of a full page reload when the form is submitted. This retains shared UI and client-side state.
-   When `action` is a **function** (Server Action), `<Form>` behaves like a [React form](https://react.dev/reference/react-dom/components/form), executing the action when the form is submitted.

### [`action` (string) Props](https://nextjs.org/docs/app/api-reference/components/form#action-string-props)

When `action` is a string, the `<Form>` component supports the following props:

| Prop | Example | Type | Required |
| --- | --- | --- | --- |
| `action` | `action="/search"` | `string` (URL or relative path) | Yes |
| `replace` | `replace={false}` | `boolean` | \- |
| `scroll` | `scroll={true}` | `boolean` | \- |
| `prefetch` | `prefetch={true}` | `boolean` | \- |

-   **`action`**: The URL or path to navigate to when the form is submitted.
    -   An empty string `""` will navigate to the same route with updated search params.
-   **`replace`**: Replaces the current history state instead of pushing a new one to the [browser's history](https://developer.mozilla.org/en-US/docs/Web/API/History_API) stack. Default is `false`.
-   **`scroll`**: Controls the scroll behavior during navigation. Defaults to `true`, this means it will scroll to the top of the new route, and maintain the scroll position for backwards and forwards navigation.
-   **`prefetch`**: Controls whether the path should be prefetched when the form becomes visible in the user's viewport. Defaults to `true`.

### [`action` (function) Props](https://nextjs.org/docs/app/api-reference/components/form#action-function-props)

When `action` is a function, the `<Form>` component supports the following prop:

| Prop | Example | Type | Required |
| --- | --- | --- | --- |
| `action` | `action={myAction}` | `function` (Server Action) | Yes |

-   **`action`**: The Server Action to be called when the form is submitted. See the [React docs](https://react.dev/reference/react-dom/components/form#props) for more.

> **Good to know**: When `action` is a function, the `replace` and `scroll` props are ignored.

### [Caveats](https://nextjs.org/docs/app/api-reference/components/form#caveats)

-   **`formAction`**: Can be used in a `<button>` or `<input type="submit">` fields to override the `action` prop. Next.js will perform a client-side navigation, however, this approach doesn't support prefetching.
    -   When using [`basePath`](https://nextjs.org/docs/app/api-reference/config/next-config-js/basePath), you must also include it in the `formAction` path. e.g. `formAction="/base-path/search"`.
-   **`key`**: Passing a `key` prop to a string `action` is not supported. If you'd like to trigger a re-render or perform a mutation, consider using a function `action` instead.

-   **`onSubmit`**: Can be used to handle form submission logic. However, calling `event.preventDefault()` will override `<Form>` behavior such as navigating to the specified URL.
-   **[`method`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/form#method), [`encType`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/form#enctype), [`target`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/form#target)**: Are not supported as they override `<Form>` behavior.
    -   Similarly, `formMethod`, `formEncType`, and `formTarget` can be used to override the `method`, `encType`, and `target` props respectively, and using them will fallback to native browser behavior.
    -   If you need to use these props, use the HTML `<form>` element instead.
-   **`<input type="file">`**: Using this input type when the `action` is a string will match browser behavior by submitting the filename instead of the file object.

## [Examples](https://nextjs.org/docs/app/api-reference/components/form#examples)

### [Search form that leads to a search result page](https://nextjs.org/docs/app/api-reference/components/form#search-form-that-leads-to-a-search-result-page)

You can create a search form that navigates to a search results page by passing the path as an `action`:

```
<span><span>import</span><span> Form </span><span>from</span><span> </span><span>'next/form'</span></span>
<span> </span>
<span><span>export</span><span> </span><span>default</span><span> </span><span>function</span><span> </span><span>Page</span><span>() {</span></span>
<span><span>  </span><span>return</span><span> (</span></span>
<span><span>    &lt;</span><span>Form</span><span> </span><span>action</span><span>=</span><span>"/search"</span><span>&gt;</span></span>
<span><span>      &lt;</span><span>input</span><span> </span><span>name</span><span>=</span><span>"query"</span><span> /&gt;</span></span>
<span><span>      &lt;</span><span>button</span><span> </span><span>type</span><span>=</span><span>"submit"</span><span>&gt;Submit&lt;/</span><span>button</span><span>&gt;</span></span>
<span><span>    &lt;/</span><span>Form</span><span>&gt;</span></span>
<span><span>  )</span></span>
<span><span>}</span></span>
```

When the user updates the query input field and submits the form, the form data will be encoded into the URL as search params, e.g. `/search?query=abc`.

> **Good to know**: If you pass an empty string `""` to `action`, the form will navigate to the same route with updated search params.

On the results page, you can access the query using the [`searchParams`](https://nextjs.org/docs/app/api-reference/file-conventions/page#searchparams-optional) `page.js` prop and use it to fetch data from an external source.

```
<span><span>import</span><span> { getSearchResults } </span><span>from</span><span> </span><span>'@/lib/search'</span></span>
<span> </span>
<span><span>export</span><span> </span><span>default</span><span> </span><span>async</span><span> </span><span>function</span><span> </span><span>SearchPage</span><span>({</span></span>
<span><span>  searchParams</span><span>,</span></span>
<span><span>}</span><span>:</span><span> {</span></span>
<span><span>  searchParams</span><span>:</span><span> </span><span>Promise</span><span>&lt;{ [key</span><span>:</span><span> </span><span>string</span><span>]</span><span>:</span><span> </span><span>string</span><span> </span><span>|</span><span> </span><span>string</span><span>[] </span><span>|</span><span> </span><span>undefined</span><span> }&gt;</span></span>
<span><span>}) {</span></span>
<span><span>  </span><span>const</span><span> </span><span>results</span><span> </span><span>=</span><span> </span><span>await</span><span> </span><span>getSearchResults</span><span>((</span><span>await</span><span> searchParams).query)</span></span>
<span> </span>
<span><span>  </span><span>return</span><span> &lt;</span><span>div</span><span>&gt;...&lt;/</span><span>div</span><span>&gt;</span></span>
<span><span>}</span></span>
```

When the `<Form>` becomes visible in the user's viewport, shared UI (such as `layout.js` and `loading.js`) on the `/search` page will be prefetched. On submission, the form will immediately navigate to the new route and show loading UI while the results are being fetched. You can design the fallback UI using [`loading.js`](https://nextjs.org/docs/app/api-reference/file-conventions/loading):

```
<span><span>export</span><span> </span><span>default</span><span> </span><span>function</span><span> </span><span>Loading</span><span>() {</span></span>
<span><span>  </span><span>return</span><span> &lt;</span><span>div</span><span>&gt;Loading...&lt;/</span><span>div</span><span>&gt;</span></span>
<span><span>}</span></span>
```

To cover cases when shared UI hasn't yet loaded, you can show instant feedback to the user using [`useFormStatus`](https://react.dev/reference/react-dom/hooks/useFormStatus).

First, create a component that displays a loading state when the form is pending:

```
<span><span>'use client'</span></span>
<span><span>import</span><span> { useFormStatus } </span><span>from</span><span> </span><span>'react-dom'</span></span>
<span> </span>
<span><span>export</span><span> </span><span>default</span><span> </span><span>function</span><span> </span><span>SearchButton</span><span>() {</span></span>
<span><span>  </span><span>const</span><span> </span><span>status</span><span> </span><span>=</span><span> </span><span>useFormStatus</span><span>()</span></span>
<span><span>  </span><span>return</span><span> (</span></span>
<span><span>    &lt;</span><span>button</span><span> </span><span>type</span><span>=</span><span>"submit"</span><span>&gt;{</span><span>status</span><span>.pending </span><span>?</span><span> </span><span>'Searching...'</span><span> </span><span>:</span><span> </span><span>'Search'</span><span>}&lt;/</span><span>button</span><span>&gt;</span></span>
<span><span>  )</span></span>
<span><span>}</span></span>
```

Then, update the search form page to use the `SearchButton` component:

```
<span><span>import</span><span> Form </span><span>from</span><span> </span><span>'next/form'</span></span>
<span><span>import</span><span> { SearchButton } </span><span>from</span><span> </span><span>'@/ui/search-button'</span></span>
<span> </span>
<span><span>export</span><span> </span><span>default</span><span> </span><span>function</span><span> </span><span>Page</span><span>() {</span></span>
<span><span>  </span><span>return</span><span> (</span></span>
<span><span>    &lt;</span><span>Form</span><span> </span><span>action</span><span>=</span><span>"/search"</span><span>&gt;</span></span>
<span><span>      &lt;</span><span>input</span><span> </span><span>name</span><span>=</span><span>"query"</span><span> /&gt;</span></span>
<span><span>      &lt;</span><span>SearchButton</span><span> /&gt;</span></span>
<span><span>    &lt;/</span><span>Form</span><span>&gt;</span></span>
<span><span>  )</span></span>
<span><span>}</span></span>
```

### [Mutations with Server Actions](https://nextjs.org/docs/app/api-reference/components/form#mutations-with-server-actions)

You can perform mutations by passing a function to the `action` prop.

```
<span><span>import</span><span> Form </span><span>from</span><span> </span><span>'next/form'</span></span>
<span><span>import</span><span> { createPost } </span><span>from</span><span> </span><span>'@/posts/actions'</span></span>
<span> </span>
<span><span>export</span><span> </span><span>default</span><span> </span><span>function</span><span> </span><span>Page</span><span>() {</span></span>
<span><span>  </span><span>return</span><span> (</span></span>
<span><span>    &lt;</span><span>Form</span><span> </span><span>action</span><span>=</span><span>{createPost}&gt;</span></span>
<span><span>      &lt;</span><span>input</span><span> </span><span>name</span><span>=</span><span>"title"</span><span> /&gt;</span></span>
<span><span>      {</span><span>/* ... */</span><span>}</span></span>
<span><span>      &lt;</span><span>button</span><span> </span><span>type</span><span>=</span><span>"submit"</span><span>&gt;Create Post&lt;/</span><span>button</span><span>&gt;</span></span>
<span><span>    &lt;/</span><span>Form</span><span>&gt;</span></span>
<span><span>  )</span></span>
<span><span>}</span></span>
```

After a mutation, it's common to redirect to the new resource. You can use the [`redirect`](https://nextjs.org/docs/app/building-your-application/routing/redirecting) function from `next/navigation` to navigate to the new post page.

> **Good to know**: Since the "destination" of the form submission is not known until the action is executed, `<Form>` cannot automatically prefetch shared UI.

```
<span><span>'use server'</span></span>
<span><span>import</span><span> { redirect } </span><span>from</span><span> </span><span>'next/navigation'</span></span>
<span> </span>
<span><span>export</span><span> </span><span>async</span><span> </span><span>function</span><span> </span><span>createPost</span><span>(formData</span><span>:</span><span> </span><span>FormData</span><span>) {</span></span>
<span><span>  </span><span>// Create a new post</span></span>
<span><span>  </span><span>// ...</span></span>
<span> </span>
<span><span>  </span><span>// Redirect to the new post</span></span>
<span><span>  </span><span>redirect</span><span>(</span><span>`/posts/</span><span>${</span><span>data</span><span>.id</span><span>}</span><span>`</span><span>)</span></span>
<span><span>}</span></span>
```

Then, in the new page, you can fetch data using the `params` prop:

```
<span><span>import</span><span> { getPost } </span><span>from</span><span> </span><span>'@/posts/data'</span></span>
<span> </span>
<span><span>export</span><span> </span><span>default</span><span> </span><span>async</span><span> </span><span>function</span><span> </span><span>PostPage</span><span>({</span></span>
<span><span>  params</span><span>,</span></span>
<span><span>}</span><span>:</span><span> {</span></span>
<span><span>  params</span><span>:</span><span> </span><span>Promise</span><span>&lt;{ id</span><span>:</span><span> </span><span>string</span><span> }&gt;</span></span>
<span><span>}) {</span></span>
<span><span>  </span><span>const</span><span> { </span><span>id</span><span> } </span><span>=</span><span> </span><span>await</span><span> params</span></span>
<span><span>  </span><span>const</span><span> </span><span>data</span><span> </span><span>=</span><span> </span><span>await</span><span> </span><span>getPost</span><span>(id)</span></span>
<span> </span>
<span><span>  </span><span>return</span><span> (</span></span>
<span><span>    &lt;</span><span>div</span><span>&gt;</span></span>
<span><span>      &lt;</span><span>h1</span><span>&gt;{</span><span>data</span><span>.title}&lt;/</span><span>h1</span><span>&gt;</span></span>
<span><span>      {</span><span>/* ... */</span><span>}</span></span>
<span><span>    &lt;/</span><span>div</span><span>&gt;</span></span>
<span><span>  )</span></span>
<span><span>}</span></span>
```

See the [Server Actions](https://nextjs.org/docs/app/building-your-application/data-fetching/server-actions-and-mutations) docs for more examples.