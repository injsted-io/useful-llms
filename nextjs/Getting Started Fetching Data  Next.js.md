## How to fetch data and stream

This page will walk you through how you can fetch data in [Server Components](https://nextjs.org/docs/app/getting-started/fetching-data#server-components) and [Client Components](https://nextjs.org/docs/app/getting-started/fetching-data#client-components). As well as how to [stream](https://nextjs.org/docs/app/getting-started/fetching-data#streaming) content that depends on data.

### [Server Components](https://nextjs.org/docs/app/getting-started/fetching-data#server-components)

You can fetch data in Server Components using:

1.  The [`fetch` API](https://nextjs.org/docs/app/getting-started/fetching-data#with-the-fetch-api)
2.  An [ORM or database](https://nextjs.org/docs/app/getting-started/fetching-data#with-an-orm-or-database)

#### [With the `fetch` API](https://nextjs.org/docs/app/getting-started/fetching-data#with-the-fetch-api)

To fetch data with the `fetch` API, turn your component into an asynchronous function, and await the `fetch` call. For example:

```
<span><span>export</span><span> </span><span>default</span><span> </span><span>async</span><span> </span><span>function</span><span> </span><span>Page</span><span>() {</span></span>
<span><span>  </span><span>const</span><span> </span><span>data</span><span> </span><span>=</span><span> </span><span>await</span><span> </span><span>fetch</span><span>(</span><span>'https://api.vercel.app/</span><span>blog</span><span>'</span><span>)</span></span>
<span><span>  </span><span>const</span><span> </span><span>posts</span><span> </span><span>=</span><span> </span><span>await</span><span> </span><span>data</span><span>.json</span><span>()</span></span>
<span><span>  </span><span>return</span><span> (</span></span>
<span><span>    &lt;</span><span>ul</span><span>&gt;</span></span>
<span><span>      {</span><span>posts</span><span>.map</span><span>((post) </span><span>=&gt;</span><span> (</span></span>
<span><span>        &lt;</span><span>li</span><span> </span><span>key</span><span>=</span><span>{</span><span>post</span><span>.id}&gt;{</span><span>post</span><span>.title}&lt;/</span><span>li</span><span>&gt;</span></span>
<span><span>      ))}</span></span>
<span><span>    &lt;/</span><span>ul</span><span>&gt;</span></span>
<span><span>  )</span></span>
<span><span>}</span></span>
```

#### [With an ORM or database](https://nextjs.org/docs/app/getting-started/fetching-data#with-an-orm-or-database)

Since Server Components are rendered on the server, you can safely make database queries using an ORM or database client. Turn your component into an asynchronous function, and await the call:

```
<span><span>import</span><span> { db</span><span>,</span><span> posts } </span><span>from</span><span> </span><span>'@/lib/db'</span></span>
<span> </span>
<span><span>export</span><span> </span><span>default</span><span> </span><span>async</span><span> </span><span>function</span><span> </span><span>Page</span><span>() {</span></span>
<span><span>  </span><span>const</span><span> </span><span>allPosts</span><span> </span><span>=</span><span> </span><span>await</span><span> </span><span>db</span><span>.select</span><span>()</span><span>.from</span><span>(posts)</span></span>
<span><span>  </span><span>return</span><span> (</span></span>
<span><span>    &lt;</span><span>ul</span><span>&gt;</span></span>
<span><span>      {</span><span>allPosts</span><span>.map</span><span>((post) </span><span>=&gt;</span><span> (</span></span>
<span><span>        &lt;</span><span>li</span><span> </span><span>key</span><span>=</span><span>{</span><span>post</span><span>.id}&gt;{</span><span>post</span><span>.title}&lt;/</span><span>li</span><span>&gt;</span></span>
<span><span>      ))}</span></span>
<span><span>    &lt;/</span><span>ul</span><span>&gt;</span></span>
<span><span>  )</span></span>
<span><span>}</span></span>
```

### [Client Components](https://nextjs.org/docs/app/getting-started/fetching-data#client-components)

There are two ways to fetch data in Client Components, using:

1.  React's [`use` hook](https://react.dev/reference/react/use)
2.  A community library like [SWR](https://swr.vercel.app/) or [React Query](https://tanstack.com/query/latest)

#### [With the `use` hook](https://nextjs.org/docs/app/getting-started/fetching-data#with-the-use-hook)

You can use React's [`use` hook](https://react.dev/reference/react/use) to [stream](https://nextjs.org/docs/app/getting-started/fetching-data#streaming) data from the server to client. Start by fetching data in your Server component, and pass the promise to your Client Component as prop:

```
<span><span>import</span><span> Posts </span><span>from</span><span> </span><span>'@/app/ui/posts</span></span>
<span><span>import</span><span> { Suspense } </span><span>from</span><span> </span><span>'react'</span></span>
<span> </span>
<span><span>export</span><span> </span><span>default</span><span> </span><span>function</span><span> </span><span>Page</span><span>() {</span></span>
<span><span>  </span><span>// Don't await the data fetching function</span></span>
<span><span>  </span><span>const</span><span> </span><span>posts</span><span> </span><span>=</span><span> </span><span>getPosts</span><span>()</span></span>
<span> </span>
<span><span>  </span><span>return</span><span> (</span></span>
<span><span>    &lt;</span><span>Suspense</span><span> </span><span>fallback</span><span>=</span><span>{&lt;</span><span>div</span><span>&gt;Loading...&lt;/</span><span>div</span><span>&gt;}&gt;</span></span>
<span><span>      &lt;</span><span>Posts</span><span> </span><span>posts</span><span>=</span><span>{posts} /&gt;</span></span>
<span><span>    &lt;/</span><span>Suspense</span><span>&gt;</span></span>
<span><span>  )</span></span>
<span><span>}</span></span>
```

Then, in your Client Component, use the `use` hook to read the promise:

```
<span><span>'use client'</span></span>
<span><span>import</span><span> { use } </span><span>from</span><span> </span><span>'react'</span></span>
<span> </span>
<span><span>export</span><span> </span><span>default</span><span> </span><span>function</span><span> </span><span>Posts</span><span>({</span></span>
<span><span>  posts</span><span>,</span></span>
<span><span>}</span><span>:</span><span> {</span></span>
<span><span>  posts</span><span>:</span><span> </span><span>Promise</span><span>&lt;{ id</span><span>:</span><span> </span><span>string</span><span>; title</span><span>:</span><span> </span><span>string</span><span> }[]&gt;</span></span>
<span><span>}) {</span></span>
<span><span>  </span><span>const</span><span> </span><span>allPosts</span><span> </span><span>=</span><span> </span><span>use</span><span>(posts)</span></span>
<span> </span>
<span><span>  </span><span>return</span><span> (</span></span>
<span><span>    &lt;</span><span>ul</span><span>&gt;</span></span>
<span><span>      {</span><span>allPosts</span><span>.map</span><span>((post) </span><span>=&gt;</span><span> (</span></span>
<span><span>        &lt;</span><span>li</span><span> </span><span>key</span><span>=</span><span>{</span><span>post</span><span>.id}&gt;{</span><span>post</span><span>.title}&lt;/</span><span>li</span><span>&gt;</span></span>
<span><span>      ))}</span></span>
<span><span>    &lt;/</span><span>ul</span><span>&gt;</span></span>
<span><span>  )</span></span>
<span><span>}</span></span>
```

In the example above, you need to wrap the `<Posts />` component in a [`<Suspense>` boundary](https://react.dev/reference/react/Suspense). This means the fallback will be shown while the promise is being resolved. Learn more about [streaming](https://nextjs.org/docs/app/getting-started/fetching-data#streaming).

You can use a community library like [SWR](https://swr.vercel.app/) or [React Query](https://tanstack.com/query/latest) to fetch data in Client Components. These libraries have their own semantics for caching, streaming, and other features. For example, with SWR:

```
<span><span>'use client'</span></span>
<span><span>import</span><span> useSWR </span><span>from</span><span> </span><span>'swr'</span></span>
<span> </span>
<span><span>const</span><span> </span><span>fetcher</span><span> </span><span>=</span><span> (url) </span><span>=&gt;</span><span> </span><span>fetch</span><span>(url)</span><span>.then</span><span>((r) </span><span>=&gt;</span><span> </span><span>r</span><span>.json</span><span>())</span></span>
<span> </span>
<span><span>export</span><span> </span><span>default</span><span> </span><span>function</span><span> </span><span>BlogPage</span><span>() {</span></span>
<span><span>  </span><span>const</span><span> { </span><span>data</span><span>,</span><span> </span><span>error</span><span>,</span><span> </span><span>isLoading</span><span> } </span><span>=</span><span> </span><span>useSWR</span><span>(</span></span>
<span><span>    </span><span>'https://api.vercel.app/</span><span>blog</span><span>'</span><span>,</span></span>
<span><span>    fetcher</span></span>
<span><span>  )</span></span>
<span> </span>
<span><span>  </span><span>if</span><span> (isLoading) </span><span>return</span><span> &lt;</span><span>div</span><span>&gt;Loading...&lt;/</span><span>div</span><span>&gt;</span></span>
<span><span>  </span><span>if</span><span> (error) </span><span>return</span><span> &lt;</span><span>div</span><span>&gt;Error: {</span><span>error</span><span>.message}&lt;/</span><span>div</span><span>&gt;</span></span>
<span> </span>
<span><span>  </span><span>return</span><span> (</span></span>
<span><span>    &lt;</span><span>ul</span><span>&gt;</span></span>
<span><span>      {</span><span>data</span><span>.map</span><span>((post</span><span>:</span><span> { id</span><span>:</span><span> </span><span>string</span><span>; title</span><span>:</span><span> </span><span>string</span><span> }) </span><span>=&gt;</span><span> (</span></span>
<span><span>        &lt;</span><span>li</span><span> </span><span>key</span><span>=</span><span>{</span><span>post</span><span>.id}&gt;{</span><span>post</span><span>.title}&lt;/</span><span>li</span><span>&gt;</span></span>
<span><span>      ))}</span></span>
<span><span>    &lt;/</span><span>ul</span><span>&gt;</span></span>
<span><span>  )</span></span>
<span><span>}</span></span>
```

## [Streaming](https://nextjs.org/docs/app/getting-started/fetching-data#streaming)

> **Warning:** The content below assumes the [`dynamicIO` config option](https://nextjs.org/docs/app/api-reference/config/next-config-js/dynamicIO) is enabled in your application. The flag was introduced in Next.js 15 canary.

When using `async/await` in Server Components, Next.js will opt into **dynamic rendering**. This means the data will be fetched and rendered on the server for every user request. If there are any slow data requests, the whole route will be blocked from rendering.

To improve the initial load time and user experience, you can use streaming to break up the page's HTML into smaller chunks and progressively send those chunks from the server to the client.

![How Server Rendering with Streaming Works](https://nextjs.org/_next/image?url=https%3A%2F%2Fh8DxKfmAPhn8O0p3.public.blob.vercel-storage.com%2Fdocs%2Fdark%2Fserver-rendering-with-streaming.png&w=3840&q=75)

There are two ways you can implement streaming in your application:

1.  With the [`loading.js` file](https://nextjs.org/docs/app/getting-started/fetching-data#with-loadingjs)
2.  With React's [`<Suspense>` component](https://nextjs.org/docs/app/getting-started/fetching-data#with-suspense)

### [With `loading.js`](https://nextjs.org/docs/app/getting-started/fetching-data#with-loadingjs)

You can create a `loading.js` file in the same folder as your page to stream the **entire page** while the data is being fetched. For example, to stream `app/blog/page.js`, add the file inside the `app/blog` folder.

![Blog folder structure with loading.js file](https://nextjs.org/_next/image?url=https%3A%2F%2Fh8DxKfmAPhn8O0p3.public.blob.vercel-storage.com%2Fdocs%2Fdark%2Floading-file.png&w=3840&q=75)

```
<span><span>export</span><span> </span><span>default</span><span> </span><span>function</span><span> </span><span>Loading</span><span>() {</span></span>
<span><span>  </span><span>// Define the Loading UI here</span></span>
<span><span>  </span><span>return</span><span> &lt;</span><span>div</span><span>&gt;Loading...&lt;/</span><span>div</span><span>&gt;</span></span>
<span><span>}</span></span>
```

On navigation, the user will immediately see the layout and a [loading state](https://nextjs.org/docs/app/getting-started/fetching-data#creating-meaningful-loading-states) while the page is being rendered. The new content will then be automatically swapped in once rendering is complete.

![Loading UI](https://nextjs.org/_next/image?url=https%3A%2F%2Fh8DxKfmAPhn8O0p3.public.blob.vercel-storage.com%2Fdocs%2Fdark%2Floading-ui.png&w=3840&q=75)

Behind-the-scenes, `loading.js` will be nested inside `layout.js`, and will automatically wrap the `page.js` file and any children below in a `<Suspense>` boundary.

![loading.js overview](https://nextjs.org/_next/image?url=https%3A%2F%2Fh8DxKfmAPhn8O0p3.public.blob.vercel-storage.com%2Fdocs%2Fdark%2Floading-overview.png&w=3840&q=75)

This approach works well for route segments (layouts and pages), but for more granular streaming, you can use `<Suspense>`.

### [With `<Suspense>`](https://nextjs.org/docs/app/getting-started/fetching-data#with-suspense)

`<Suspense>` allows you to be more granular about what parts of the page to stream. For example, you can immediately show any page content that falls outside of the `<Suspense>` boundary, and stream in the list of blog posts inside the boundary.

```
<span><span>import</span><span> { Suspense } </span><span>from</span><span> </span><span>'react'</span></span>
<span><span>import</span><span> BlogList </span><span>from</span><span> </span><span>'@/components/BlogList'</span></span>
<span><span>import</span><span> BlogListSkeleton </span><span>from</span><span> </span><span>'@/components/BlogListSkeleton'</span></span>
<span> </span>
<span><span>export</span><span> </span><span>default</span><span> </span><span>function</span><span> </span><span>BlogPage</span><span>() {</span></span>
<span><span>  </span><span>return</span><span> (</span></span>
<span><span>    &lt;</span><span>div</span><span>&gt;</span></span>
<span><span>      {</span><span>/* This content will be sent to the client immediately */</span><span>}</span></span>
<span><span>      &lt;</span><span>header</span><span>&gt;</span></span>
<span><span>        &lt;</span><span>h1</span><span>&gt;Welcome to the Blog&lt;/</span><span>h1</span><span>&gt;</span></span>
<span><span>        &lt;</span><span>p</span><span>&gt;Read the latest posts below.&lt;/</span><span>p</span><span>&gt;</span></span>
<span><span>      &lt;/</span><span>header</span><span>&gt;</span></span>
<span><span>      &lt;</span><span>main</span><span>&gt;</span></span>
<span><span>        {</span><span>/* Any content wrapped in a &lt;Suspense&gt; boundary will be streamed */</span><span>}</span></span>
<span><span>        &lt;</span><span>Suspense</span><span> </span><span>fallback</span><span>=</span><span>{&lt;</span><span>BlogListSkeleton</span><span> /&gt;}&gt;</span></span>
<span><span>          &lt;</span><span>BlogList</span><span> /&gt;</span></span>
<span><span>        &lt;/</span><span>Suspense</span><span>&gt;</span></span>
<span><span>      &lt;/</span><span>main</span><span>&gt;</span></span>
<span><span>    &lt;/</span><span>div</span><span>&gt;</span></span>
<span><span>  )</span></span>
<span><span>}</span></span>
```

### [Creating meaningful loading states](https://nextjs.org/docs/app/getting-started/fetching-data#creating-meaningful-loading-states)

An instant loading state is fallback UI that is shown immediately to the user after navigation. For the best user experience, we recommend designing loading states that are meaningful and help users understand the app is responding. For example, you can use skeletons and spinners, or a small but meaningful part of future screens such as a cover photo, title, etc.

In development, you can preview and inspect the loading state of your components using the [React Devtools](https://react.dev/learn/react-developer-tools).