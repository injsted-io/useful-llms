## How to add metadata and create OG images

The Metadata APIs can be used to define your application metadata for improved SEO and web shareability and include:

1.  [The static `metadata` object](https://nextjs.org/docs/app/getting-started/metadata-and-og-images#static-metadata)
2.  [The dynamic `generateMetadata` function](https://nextjs.org/docs/app/getting-started/metadata-and-og-images#generated-metadata)
3.  Special [file conventions](https://nextjs.org/docs/app/api-reference/file-conventions/metadata) that can be used to add static or dynamically generated [favicons](https://nextjs.org/docs/app/getting-started/metadata-and-og-images#favicons) and [OG images](https://nextjs.org/docs/app/getting-started/metadata-and-og-images#static-open-graph-images).

With all the options above, Next.js will automatically generate the relevant `<head>` tags for your page, which can be inspected in the browser's developer tools.

## [Default fields](https://nextjs.org/docs/app/getting-started/metadata-and-og-images#default-fields)

There are two default `meta` tags that are always added even if a route doesn't define metadata:

-   The [meta charset tag](https://developer.mozilla.org/docs/Web/HTML/Element/meta#attr-charset) sets the character encoding for the website.
-   The [meta viewport tag](https://developer.mozilla.org/docs/Web/HTML/Viewport_meta_tag) sets the viewport width and scale for the website to adjust for different devices.

```
<span><span>&lt;</span><span>meta</span><span> </span><span>charset</span><span>=</span><span>"utf-8"</span><span> /&gt;</span></span>
<span><span>&lt;</span><span>meta</span><span> </span><span>name</span><span>=</span><span>"viewport"</span><span> </span><span>content</span><span>=</span><span>"width=device-width, initial-scale=1"</span><span> /&gt;</span></span>
```

The other metadata fields can be defined with the `Metadata` object (for [static metadata](https://nextjs.org/docs/app/getting-started/metadata-and-og-images#static-metadata)) or the `generateMetadata` function (for [generated metadata](https://nextjs.org/docs/app/getting-started/metadata-and-og-images#generated-metadata)).

To define static metadata, export a [`Metadata` object](https://nextjs.org/docs/app/api-reference/functions/generate-metadata#metadata-object) from a static [`layout.js`](https://nextjs.org/docs/app/api-reference/file-conventions/layout) or [`page.js`](https://nextjs.org/docs/app/api-reference/file-conventions/page) file. For example, to add a title and description to the blog route:

```
<span><span>import</span><span> </span><span>type</span><span> { Metadata } </span><span>from</span><span> </span><span>'next'</span></span>
<span> </span>
<span><span>export</span><span> </span><span>const</span><span> </span><span>metadata</span><span>:</span><span> </span><span>Metadata</span><span> </span><span>=</span><span> {</span></span>
<span><span>  title</span><span>:</span><span> </span><span>'My Blog'</span><span>,</span></span>
<span><span>  description</span><span>:</span><span> </span><span>'...'</span><span>,</span></span>
<span><span>}</span></span>
<span> </span>
<span><span>export</span><span> </span><span>default</span><span> </span><span>function</span><span> </span><span>Page</span><span>() {}</span></span>
```

You can view a full list of available options, in the [generate metadata documentation](https://nextjs.org/docs/app/api-reference/functions/generate-metadata#metadata-fields).

You can use [`generateMetadata`](https://nextjs.org/docs/app/api-reference/functions/generate-metadata) function to `fetch` metadata that depends on data. For example, to fetch the title and description for a specific blog post:

```
<span><span>import</span><span> </span><span>type</span><span> { Metadata</span><span>,</span><span> ResolvingMetadata } </span><span>from</span><span> </span><span>'next'</span></span>
<span> </span>
<span><span>type</span><span> </span><span>Props</span><span> </span><span>=</span><span> {</span></span>
<span><span>  params</span><span>:</span><span> </span><span>Promise</span><span>&lt;{ id</span><span>:</span><span> </span><span>string</span><span> }&gt;</span></span>
<span><span>  searchParams</span><span>:</span><span> </span><span>Promise</span><span>&lt;{ [key</span><span>:</span><span> </span><span>string</span><span>]</span><span>:</span><span> </span><span>string</span><span> </span><span>|</span><span> </span><span>string</span><span>[] </span><span>|</span><span> </span><span>undefined</span><span> }&gt;</span></span>
<span><span>}</span></span>
<span> </span>
<span><span>export</span><span> </span><span>async</span><span> </span><span>function</span><span> </span><span>generateMetadata</span><span>(</span></span>
<span><span>  { params</span><span>,</span><span> searchParams }</span><span>:</span><span> </span><span>Props</span><span>,</span></span>
<span><span>  parent</span><span>:</span><span> </span><span>ResolvingMetadata</span></span>
<span><span>)</span><span>:</span><span> </span><span>Promise</span><span>&lt;</span><span>Metadata</span><span>&gt; {</span></span>
<span><span>  </span><span>const</span><span> </span><span>slug</span><span> </span><span>=</span><span> (</span><span>await</span><span> params).slug</span></span>
<span> </span>
<span><span>  </span><span>// fetch post information</span></span>
<span><span>  </span><span>const</span><span> </span><span>post</span><span> </span><span>=</span><span> </span><span>await</span><span> </span><span>fetch</span><span>(</span><span>`https://api.vercel.app/</span><span>blog</span><span>/</span><span>${</span><span>slug</span><span>}</span><span>`</span><span>)</span><span>.then</span><span>((res) </span><span>=&gt;</span></span>
<span><span>    </span><span>res</span><span>.json</span><span>()</span></span>
<span><span>  )</span></span>
<span> </span>
<span><span>  </span><span>return</span><span> {</span></span>
<span><span>    title</span><span>:</span><span> </span><span>post</span><span>.title</span><span>,</span></span>
<span><span>    description</span><span>:</span><span> </span><span>post</span><span>.description</span><span>,</span></span>
<span><span>  }</span></span>
<span><span>}</span></span>
<span> </span>
<span><span>export</span><span> </span><span>default</span><span> </span><span>function</span><span> </span><span>Page</span><span>({ params</span><span>,</span><span> searchParams }</span><span>:</span><span> </span><span>Props</span><span>) {}</span></span>
```

Behind-the-scenes, Next.js will stream metadata separately from the UI and inject the metadata into the HTML as soon as it's resolved.

### [Memoizing data requests](https://nextjs.org/docs/app/getting-started/metadata-and-og-images#memoizing-data-requests)

There may be cases where you need to fetch the **same** data for metadata and the page itself. To avoid duplicate requests, you can use React's [`cache` function](https://react.dev/reference/react/cache) to memoize the return value and only fetch the data once. For example, to fetch the blog post information for both the metadata and the page:

```
<span><span>import</span><span> { cache } </span><span>from</span><span> </span><span>'react'</span></span>
<span><span>import</span><span> { db } </span><span>from</span><span> </span><span>'@/app/</span><span>lib</span><span>/db'</span></span>
<span> </span>
<span><span>// getPost will be used twice, but execute only once</span></span>
<span><span>export</span><span> </span><span>const</span><span> </span><span>getPost</span><span> </span><span>=</span><span> </span><span>cache</span><span>(</span><span>async</span><span> (slug</span><span>:</span><span> </span><span>string</span><span>) </span><span>=&gt;</span><span> {</span></span>
<span><span>  </span><span>const</span><span> </span><span>res</span><span> </span><span>=</span><span> </span><span>await</span><span> </span><span>db</span><span>.</span><span>query</span><span>.</span><span>posts</span><span>.findFirst</span><span>({ where</span><span>:</span><span> </span><span>eq</span><span>(</span><span>posts</span><span>.slug</span><span>,</span><span> slug) })</span></span>
<span><span>  </span><span>return</span><span> res</span></span>
<span><span>})</span></span>
```

```
<span><span>import</span><span> { getPost } </span><span>from</span><span> </span><span>'@/app/lib/data'</span></span>
<span> </span>
<span><span>export</span><span> </span><span>async</span><span> </span><span>function</span><span> </span><span>generateMetadata</span><span>({</span></span>
<span><span>  params</span><span>,</span></span>
<span><span>}</span><span>:</span><span> {</span></span>
<span><span>  params</span><span>:</span><span> { slug</span><span>:</span><span> </span><span>string</span><span> }</span></span>
<span><span>}) {</span></span>
<span><span>  </span><span>const</span><span> </span><span>post</span><span> </span><span>=</span><span> </span><span>await</span><span> </span><span>getPost</span><span>(</span><span>params</span><span>.slug)</span></span>
<span><span>  </span><span>return</span><span> {</span></span>
<span><span>    title</span><span>:</span><span> </span><span>post</span><span>.title</span><span>,</span></span>
<span><span>    description</span><span>:</span><span> </span><span>post</span><span>.description</span><span>,</span></span>
<span><span>  }</span></span>
<span><span>}</span></span>
<span> </span>
<span><span>export</span><span> </span><span>default</span><span> </span><span>async</span><span> </span><span>function</span><span> </span><span>Page</span><span>({ params }</span><span>:</span><span> { params</span><span>:</span><span> { slug</span><span>:</span><span> </span><span>string</span><span> } }) {</span></span>
<span><span>  </span><span>const</span><span> </span><span>post</span><span> </span><span>=</span><span> </span><span>await</span><span> </span><span>getPost</span><span>(</span><span>params</span><span>.slug)</span></span>
<span><span>  </span><span>return</span><span> &lt;</span><span>div</span><span>&gt;{</span><span>post</span><span>.title}&lt;/</span><span>div</span><span>&gt;</span></span>
<span><span>}</span></span>
```

## [Favicons](https://nextjs.org/docs/app/getting-started/metadata-and-og-images#favicons)

Favicons are small icons that represent your site in bookmarks and search results. To add a favicon to your application, create a `favicon.ico` and add to the root of the app folder.

![Favicon Special File inside the App Folder with sibling layout and page files](https://nextjs.org/_next/image?url=https%3A%2F%2Fh8DxKfmAPhn8O0p3.public.blob.vercel-storage.com%2Fdocs%2Fdark%2Ffavicon-ico.png&w=3840&q=75)

> You can also programmatically generate favicons using code. See the [favicon docs](https://nextjs.org/docs/app/api-reference/file-conventions/metadata/app-icons) for more information.

## [Static Open Graph images](https://nextjs.org/docs/app/getting-started/metadata-and-og-images#static-open-graph-images)

Open Graph (OG) images are images that represent your site in social media. To add a static OG image to your application, create a `opengraph-image.png` file in the root of the app folder.

![OG image special file inside the App folder with sibling layout and page files](https://nextjs.org/_next/image?url=https%3A%2F%2Fh8DxKfmAPhn8O0p3.public.blob.vercel-storage.com%2Fdocs%2Fdark%2Fopengraph-image.png&w=3840&q=75)

You can also add OG images for specific routes by creating a `opengraph-image.png` deeper down the folder structure. For example, to create an OG image specific to the `/blog` route, add a `opengraph-image.jpg` file inside the `blog` folder.

![OG image special file inside the blog folder](https://nextjs.org/_next/image?url=https%3A%2F%2Fh8DxKfmAPhn8O0p3.public.blob.vercel-storage.com%2Fdocs%2Fdark%2Fopengraph-image-blog.png&w=3840&q=75)

The more specific image will take precedence over any OG images above it in the folder structure.

> Other image formats such as `jpeg`, `png`, and `webp` are also supported. See the [Open Graph Image docs](https://nextjs.org/docs/app/api-reference/file-conventions/metadata/opengraph-image) for more information.

## [Generated Open Graph images](https://nextjs.org/docs/app/getting-started/metadata-and-og-images#generated-open-graph-images)

The [`ImageResponse` constructor](https://nextjs.org/docs/app/api-reference/functions/image-response) allows you to generate dynamic images using JSX and CSS. This is useful for OG images that depend on data.

For example, to generate a unique OG image for each blog post, add a `opengraph-image.ts` file inside the `blog` folder, and import the `ImageResponse` constructor from `next/og`:

```
<span><span>import</span><span> { ImageResponse } </span><span>from</span><span> </span><span>'next/og'</span></span>
<span><span>import</span><span> { getPost } </span><span>from</span><span> </span><span>'@/app/lib/data'</span></span>
<span> </span>
<span><span>// Image metadata</span></span>
<span><span>export</span><span> </span><span>const</span><span> </span><span>size</span><span> </span><span>=</span><span> {</span></span>
<span><span>  width</span><span>:</span><span> </span><span>1200</span><span>,</span></span>
<span><span>  height</span><span>:</span><span> </span><span>630</span><span>,</span></span>
<span><span>}</span></span>
<span> </span>
<span><span>export</span><span> </span><span>const</span><span> </span><span>contentType</span><span> </span><span>=</span><span> </span><span>'image/png'</span></span>
<span> </span>
<span><span>// Image generation</span></span>
<span><span>export</span><span> </span><span>default</span><span> </span><span>async</span><span> </span><span>function</span><span> </span><span>Image</span><span>({ params }</span><span>:</span><span> { params</span><span>:</span><span> { slug</span><span>:</span><span> </span><span>string</span><span> } }) {</span></span>
<span><span>  </span><span>const</span><span> </span><span>post</span><span> </span><span>=</span><span> </span><span>await</span><span> </span><span>getPost</span><span>(</span><span>params</span><span>.slug)</span></span>
<span> </span>
<span><span>  </span><span>return</span><span> </span><span>new</span><span> </span><span>ImageResponse</span><span>(</span></span>
<span><span>    (</span></span>
<span><span>      </span><span>// ImageResponse JSX element</span></span>
<span><span>      &lt;</span><span>div</span></span>
<span><span>        </span><span>style</span><span>=</span><span>{{</span></span>
<span><span>          fontSize</span><span>:</span><span> </span><span>128</span><span>,</span></span>
<span><span>          background</span><span>:</span><span> </span><span>'white'</span><span>,</span></span>
<span><span>          width</span><span>:</span><span> </span><span>'100%'</span><span>,</span></span>
<span><span>          height</span><span>:</span><span> </span><span>'100%'</span><span>,</span></span>
<span><span>          display</span><span>:</span><span> </span><span>'flex'</span><span>,</span></span>
<span><span>          alignItems</span><span>:</span><span> </span><span>'center'</span><span>,</span></span>
<span><span>          justifyContent</span><span>:</span><span> </span><span>'center'</span><span>,</span></span>
<span><span>        }}</span></span>
<span><span>      &gt;</span></span>
<span><span>        {</span><span>post</span><span>.title}</span></span>
<span><span>      &lt;/</span><span>div</span><span>&gt;</span></span>
<span><span>    )</span></span>
<span><span>  )</span></span>
<span><span>}</span></span>
```

`ImageResponse` supports common CSS properties including flexbox and absolute positioning, custom fonts, text wrapping, centering, and nested images. [See the full list of supported CSS properties](https://nextjs.org/docs/app/api-reference/functions/image-response).

> **Good to know**:
> 
> -   Examples are available in the [Vercel OG Playground](https://og-playground.vercel.app/).
> -   `ImageResponse` uses [`@vercel/og`](https://vercel.com/docs/og-image-generation), [`satori`](https://github.com/vercel/satori), and `resvg` to convert HTML and CSS into PNG.
> -   Only flexbox and a subset of CSS properties are supported. Advanced layouts (e.g. `display: grid`) will not work.