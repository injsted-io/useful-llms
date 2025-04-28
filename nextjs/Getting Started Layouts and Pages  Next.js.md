## How to create layouts and pages

Next.js uses **file-system based routing**, meaning you can use folders and files to define routes. This page will guide you through how to create layouts and pages, and link between them.

## [Creating a page](https://nextjs.org/docs/app/getting-started/layouts-and-pages#creating-a-page)

A **page** is UI that is rendered on a specific route. To create a page, add a [`page` file](https://nextjs.org/docs/app/api-reference/file-conventions/page) inside the `app` directory and default export a React component. For example, to create an index page (`/`):

![page.js special file](https://nextjs.org/_next/image?url=https%3A%2F%2Fh8DxKfmAPhn8O0p3.public.blob.vercel-storage.com%2Fdocs%2Fdark%2Fpage-special-file.png&w=3840&q=75)

```
<span><span>export</span><span> </span><span>default</span><span> </span><span>function</span><span> </span><span>Page</span><span>() {</span></span>
<span><span>  </span><span>return</span><span> &lt;</span><span>h1</span><span>&gt;Hello Next.js!&lt;/</span><span>h1</span><span>&gt;</span></span>
<span><span>}</span></span>
```

## [Creating a layout](https://nextjs.org/docs/app/getting-started/layouts-and-pages#creating-a-layout)

A layout is UI that is **shared** between multiple pages. On navigation, layouts preserve state, remain interactive, and do not rerender.

You can define a layout by default exporting a React component from a [`layout` file](https://nextjs.org/docs/app/api-reference/file-conventions/layout). The component should accept a `children` prop which can be a page or another [layout](https://nextjs.org/docs/app/getting-started/layouts-and-pages#nesting-layouts).

For example, to create a layout that accepts your index page as child, add a `layout` file inside the `app` directory:

![layout.js special file](https://nextjs.org/_next/image?url=https%3A%2F%2Fh8DxKfmAPhn8O0p3.public.blob.vercel-storage.com%2Fdocs%2Fdark%2Flayout-special-file.png&w=3840&q=75)

```
<span><span>export</span><span> </span><span>default</span><span> </span><span>function</span><span> </span><span>DashboardLayout</span><span>({</span></span>
<span><span>  children</span><span>,</span></span>
<span><span>}</span><span>:</span><span> {</span></span>
<span><span>  children</span><span>:</span><span> </span><span>React</span><span>.</span><span>ReactNode</span></span>
<span><span>}) {</span></span>
<span><span>  </span><span>return</span><span> (</span></span>
<span><span>    &lt;</span><span>html</span><span> </span><span>lang</span><span>=</span><span>"en"</span><span>&gt;</span></span>
<span><span>      &lt;</span><span>body</span><span>&gt;</span></span>
<span><span>        {</span><span>/* Layout UI */</span><span>}</span></span>
<span><span>        {</span><span>/* Place children where you want to render a page or nested layout */</span><span>}</span></span>
<span><span>        &lt;</span><span>main</span><span>&gt;{children}&lt;/</span><span>main</span><span>&gt;</span></span>
<span><span>      &lt;/</span><span>body</span><span>&gt;</span></span>
<span><span>    &lt;/</span><span>html</span><span>&gt;</span></span>
<span><span>  )</span></span>
<span><span>}</span></span>
```

The layout above is called a [root layout](https://nextjs.org/docs/app/api-reference/file-conventions/layout#root-layouts) because it's defined at the root of the `app` directory. The root layout is **required** and must contain `html` and `body` tags.

## [Creating a nested route](https://nextjs.org/docs/app/getting-started/layouts-and-pages#creating-a-nested-route)

A nested route is a route composed of multiple URL segments. For example, the `/blog/[slug]` route is composed of three segments:

-   `/` (Root Segment)
-   `blog` (Segment)
-   `[slug]` (Leaf Segment)

In Next.js:

-   **Folders** are used to define the route segments that map to URL segments.
-   **Files** (like `page` and `layout`) are used to create UI that is shown for a segment.

To create nested routes, you can nest folders inside each other. For example, to add a route for `/blog`, create a folder called `blog` in the `app` directory. Then, to make `/blog` publicly accessible, add a `page.tsx` file:

![File hierarchy showing blog folder and a page.js file](https://nextjs.org/_next/image?url=https%3A%2F%2Fh8DxKfmAPhn8O0p3.public.blob.vercel-storage.com%2Fdocs%2Fdark%2Fblog-nested-route.png&w=3840&q=75)

```
<span><span>// Dummy imports</span></span>
<span><span>import</span><span> { getPosts } </span><span>from</span><span> </span><span>'@/lib/posts'</span></span>
<span><span>import</span><span> { Post } </span><span>from</span><span> </span><span>'@/ui/post'</span></span>
<span> </span>
<span><span>export</span><span> </span><span>default</span><span> </span><span>async</span><span> </span><span>function</span><span> </span><span>Page</span><span>() {</span></span>
<span><span>  </span><span>const</span><span> </span><span>posts</span><span> </span><span>=</span><span> </span><span>await</span><span> </span><span>getPosts</span><span>()</span></span>
<span> </span>
<span><span>  </span><span>return</span><span> (</span></span>
<span><span>    &lt;</span><span>ul</span><span>&gt;</span></span>
<span><span>      {</span><span>posts</span><span>.map</span><span>((post) </span><span>=&gt;</span><span> (</span></span>
<span><span>        &lt;</span><span>Post</span><span> </span><span>key</span><span>=</span><span>{</span><span>post</span><span>.id} </span><span>post</span><span>=</span><span>{post} /&gt;</span></span>
<span><span>      ))}</span></span>
<span><span>    &lt;/</span><span>ul</span><span>&gt;</span></span>
<span><span>  )</span></span>
<span><span>}</span></span>
```

You can continue nesting folders to create nested routes. For example, to create a route for a specific blog post, create a new `[slug]` folder inside `blog` and add a `page` file:

![File hierarchy showing blog folder with a nested slug folder and a page.js file](https://nextjs.org/_next/image?url=https%3A%2F%2Fh8DxKfmAPhn8O0p3.public.blob.vercel-storage.com%2Fdocs%2Fdark%2Fblog-post-nested-route.png&w=3840&q=75)

```
<span><span>function</span><span> </span><span>generateStaticParams</span><span>() {}</span></span>
<span> </span>
<span><span>export</span><span> </span><span>default</span><span> </span><span>function</span><span> </span><span>Page</span><span>() {</span></span>
<span><span>  </span><span>return</span><span> &lt;</span><span>h1</span><span>&gt;Hello, Blog Post Page!&lt;/</span><span>h1</span><span>&gt;</span></span>
<span><span>}</span></span>
```

Wrapping a folder name in square brackets (e.g. `[slug]`) creates a [dynamic route segment](https://nextjs.org/docs/app/building-your-application/routing/dynamic-routes) which is used to generate multiple pages from data. e.g. blog posts, product pages, etc.

## [Nesting layouts](https://nextjs.org/docs/app/getting-started/layouts-and-pages#nesting-layouts)

By default, layouts in the folder hierarchy are also nested, which means they wrap child layouts via their `children` prop. You can nest layouts by adding `layout` inside specific route segments (folders).

For example, to create a layout for the `/blog` route, add a new `layout` file inside the `blog` folder.

![File hierarchy showing root layout wrapping the blog layout](https://nextjs.org/_next/image?url=https%3A%2F%2Fh8DxKfmAPhn8O0p3.public.blob.vercel-storage.com%2Fdocs%2Fdark%2Fnested-layouts.png&w=3840&q=75)

```
<span><span>export</span><span> </span><span>default</span><span> </span><span>function</span><span> </span><span>BlogLayout</span><span>({</span></span>
<span><span>  children</span><span>,</span></span>
<span><span>}</span><span>:</span><span> {</span></span>
<span><span>  children</span><span>:</span><span> </span><span>React</span><span>.</span><span>ReactNode</span></span>
<span><span>}) {</span></span>
<span><span>  </span><span>return</span><span> &lt;</span><span>section</span><span>&gt;{children}&lt;/</span><span>section</span><span>&gt;</span></span>
<span><span>}</span></span>
```

If you were to combine the two layouts above, the root layout (`app/layout.js`) would wrap the blog layout (`app/blog/layout.js`), which would wrap the blog (`app/blog/page.js`) and blog post page (`app/blog/[slug]/page.js`).

## [Linking between pages](https://nextjs.org/docs/app/getting-started/layouts-and-pages#linking-between-pages)

You can use the [`<Link>` component](https://nextjs.org/docs/app/api-reference/components/link) to navigate between routes. `<Link>` is a built-in Next.js component that extends the HTML `<a>` tag to provide [prefetching](https://nextjs.org/docs/app/building-your-application/routing/linking-and-navigating#2-prefetching) and [client-side navigation](https://nextjs.org/docs/app/building-your-application/routing/linking-and-navigating#5-soft-navigation).

For example, to generate a list of blog posts, import `<Link>` from `next/link` and pass a `href` prop to the component:

```
<span><span>import</span><span> Link </span><span>from</span><span> </span><span>'next/link'</span></span>
<span> </span>
<span><span>export</span><span> </span><span>default</span><span> </span><span>async</span><span> </span><span>function</span><span> </span><span>Post</span><span>({ post }) {</span></span>
<span><span>  </span><span>const</span><span> </span><span>posts</span><span> </span><span>=</span><span> </span><span>await</span><span> </span><span>getPosts</span><span>()</span></span>
<span> </span>
<span><span>  </span><span>return</span><span> (</span></span>
<span><span>    &lt;</span><span>ul</span><span>&gt;</span></span>
<span><span>      {</span><span>posts</span><span>.map</span><span>((post) </span><span>=&gt;</span><span> (</span></span>
<span><span>        &lt;</span><span>li</span><span> </span><span>key</span><span>=</span><span>{</span><span>post</span><span>.slug}&gt;</span></span>
<span><span>          &lt;</span><span>Link</span><span> </span><span>href</span><span>=</span><span>{</span><span>`/blog/</span><span>${</span><span>post</span><span>.slug</span><span>}</span><span>`</span><span>}&gt;{</span><span>post</span><span>.title}&lt;/</span><span>Link</span><span>&gt;</span></span>
<span><span>        &lt;/</span><span>li</span><span>&gt;</span></span>
<span><span>      ))}</span></span>
<span><span>    &lt;/</span><span>ul</span><span>&gt;</span></span>
<span><span>  )</span></span>
<span><span>}</span></span>
```

`<Link>` is the primary and recommended way to navigate between routes in your Next.js application. However, you can also use the [`useRouter` hook](https://nextjs.org/docs/app/api-reference/functions/use-router) for more advanced navigation.