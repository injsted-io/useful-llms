## How to use markdown and MDX in Next.js

[Markdown](https://daringfireball.net/projects/markdown/syntax) is a lightweight markup language used to format text. It allows you to write using plain text syntax and convert it to structurally valid HTML. It's commonly used for writing content on websites and blogs.

You write...

```
<span><span>I </span><span>**love**</span><span> using </span><span>[</span><span>Next.js</span><span>]</span><span>(https://nextjs.org/)</span></span>
```

Output:

```
<span><span>&lt;</span><span>p</span><span>&gt;I &lt;</span><span>strong</span><span>&gt;love&lt;/</span><span>strong</span><span>&gt; using &lt;</span><span>a</span><span> </span><span>href</span><span>=</span><span>"https://nextjs.org/"</span><span>&gt;Next.js&lt;/</span><span>a</span><span>&gt;&lt;/</span><span>p</span><span>&gt;</span></span>
```

[MDX](https://mdxjs.com/) is a superset of markdown that lets you write [JSX](https://react.dev/learn/writing-markup-with-jsx) directly in your markdown files. It is a powerful way to add dynamic interactivity and embed React components within your content.

Next.js can support both local MDX content inside your application, as well as remote MDX files fetched dynamically on the server. The Next.js plugin handles transforming markdown and React components into HTML, including support for usage in Server Components (the default in App Router).

> **Good to know**: View the [Portfolio Starter Kit](https://vercel.com/templates/next.js/portfolio-starter-kit) template for a complete working example.

## [Install dependencies](https://nextjs.org/docs/app/guides/mdx#install-dependencies)

The `@next/mdx` package, and related packages, are used to configure Next.js so it can process markdown and MDX. **It sources data from local files**, allowing you to create pages with a `.md` or `.mdx` extension, directly in your `/pages` or `/app` directory.

Install these packages to render MDX with Next.js:

```
<span><span>npm</span><span> </span><span>install</span><span> </span><span>@next/mdx</span><span> </span><span>@mdx-js/loader</span><span> </span><span>@mdx-js/react</span><span> </span><span>@types/mdx</span></span>
```

## [Configure `next.config.mjs`](https://nextjs.org/docs/app/guides/mdx#configure-nextconfigmjs)

Update the `next.config.mjs` file at your project's root to configure it to use MDX:

```
<span><span>import</span><span> createMDX </span><span>from</span><span> </span><span>'@next/mdx'</span></span>
<span> </span>
<span><span>/** </span><span>@type</span><span> </span><span>{import('next').NextConfig}</span><span> */</span></span>
<span><span>const</span><span> </span><span>nextConfig</span><span> </span><span>=</span><span> {</span></span>
<span><span>  </span><span>// Configure `pageExtensions` to include markdown and MDX files</span></span>
<span><span>  pageExtensions</span><span>:</span><span> [</span><span>'js'</span><span>,</span><span> </span><span>'jsx'</span><span>,</span><span> </span><span>'md'</span><span>,</span><span> </span><span>'mdx'</span><span>,</span><span> </span><span>'ts'</span><span>,</span><span> </span><span>'tsx'</span><span>]</span><span>,</span></span>
<span><span>  </span><span>// Optionally, add any other Next.js config below</span></span>
<span><span>}</span></span>
<span> </span>
<span><span>const</span><span> </span><span>withMDX</span><span> </span><span>=</span><span> </span><span>createMDX</span><span>({</span></span>
<span><span>  </span><span>// Add markdown plugins here, as desired</span></span>
<span><span>})</span></span>
<span> </span>
<span><span>// Merge MDX config with Next.js config</span></span>
<span><span>export</span><span> </span><span>default</span><span> </span><span>withMDX</span><span>(nextConfig)</span></span>
```

This allows `.md` and `.mdx` files to act as pages, routes, or imports in your application.

## [Add an `mdx-components.tsx` file](https://nextjs.org/docs/app/guides/mdx#add-an-mdx-componentstsx-file)

Create an `mdx-components.tsx` (or `.js`) file in the root of your project to define global MDX Components. For example, at the same level as `pages` or `app`, or inside `src` if applicable.

```
<span><span>import</span><span> </span><span>type</span><span> { MDXComponents } </span><span>from</span><span> </span><span>'mdx/types'</span></span>
<span> </span>
<span><span>export</span><span> </span><span>function</span><span> </span><span>useMDXComponents</span><span>(components</span><span>:</span><span> </span><span>MDXComponents</span><span>)</span><span>:</span><span> </span><span>MDXComponents</span><span> {</span></span>
<span><span>  </span><span>return</span><span> {</span></span>
<span><span>    </span><span>...</span><span>components</span><span>,</span></span>
<span><span>  }</span></span>
<span><span>}</span></span>
```

> **Good to know**:
> 
> -   `mdx-components.tsx` is **required** to use `@next/mdx` with App Router and will not work without it.
> -   Learn more about the [`mdx-components.tsx` file convention](https://nextjs.org/docs/app/api-reference/file-conventions/mdx-components).
> -   Learn how to [use custom styles and components](https://nextjs.org/docs/app/guides/mdx#using-custom-styles-and-components).

## [Rendering MDX](https://nextjs.org/docs/app/guides/mdx#rendering-mdx)

You can render MDX using Next.js's file based routing or by importing MDX files into other pages.

### [Using file based routing](https://nextjs.org/docs/app/guides/mdx#using-file-based-routing)

When using file based routing, you can use MDX pages like any other page.

In App Router apps, that includes being able to use [metadata](https://nextjs.org/docs/app/building-your-application/optimizing/metadata).

Create a new MDX page within the `/app` directory:

```
<span><span>  my-project</span></span>
<span><span>  ├── app</span></span>
<span><span>  │   └── mdx-page</span></span>
<span><span>  │       └── page.(mdx/md)</span></span>
<span><span>  |── mdx-components.(tsx/js)</span></span>
<span><span>  └── package.json</span></span>
```

You can use MDX in these files, and even import React components, directly inside your MDX page:

```
<span><span>import</span><span> { MyComponent } </span><span>from</span><span> </span><span>'my-component'</span></span>
<span> </span>
<span><span># Welcome to my </span><span>MDX</span><span> page</span><span>!</span></span>
<span> </span>
<span><span>This is some </span><span>**</span><span>bold</span><span>**</span><span> and _italics_ text.</span></span>
<span> </span>
<span><span>This is a list </span><span>in</span><span> markdown</span><span>:</span></span>
<span> </span>
<span><span>-</span><span> One</span></span>
<span><span>-</span><span> Two</span></span>
<span><span>-</span><span> Three</span></span>
<span> </span>
<span><span>Checkout my React component</span><span>:</span></span>
<span> </span>
<span><span>&lt;</span><span>MyComponent</span><span> /&gt;</span></span>
```

Navigating to the `/mdx-page` route should display your rendered MDX page.

### [Using imports](https://nextjs.org/docs/app/guides/mdx#using-imports)

Create a new page within the `/app` directory and an MDX file wherever you'd like:

```
<span><span>  .</span></span>
<span><span>  ├── app/</span></span>
<span><span>  │   └── mdx-page/</span></span>
<span><span>  │       └── page.(tsx/js)</span></span>
<span><span>  ├── markdown/</span></span>
<span><span>  │   └── welcome.(mdx/md)</span></span>
<span><span>  ├── mdx-components.(tsx/js)</span></span>
<span><span>  └── package.json</span></span>
```

You can use MDX in these files, and even import React components, directly inside your MDX page:

Import the MDX file inside the page to display the content:

```
<span><span>import</span><span> Welcome </span><span>from</span><span> </span><span>'@/markdown/welcome.mdx'</span></span>
<span> </span>
<span><span>export</span><span> </span><span>default</span><span> </span><span>function</span><span> </span><span>Page</span><span>() {</span></span>
<span><span>  </span><span>return</span><span> &lt;</span><span>Welcome</span><span> /&gt;</span></span>
<span><span>}</span></span>
```

Navigating to the `/mdx-page` route should display your rendered MDX page.

### [Using dynamic imports](https://nextjs.org/docs/app/guides/mdx#using-dynamic-imports)

You can import dynamic MDX components instead of using filesystem routing for MDX files.

For example, you can have a dynamic route segment which loads MDX components from a separate directory:

![Route segments for dynamic MDX components](https://nextjs.org/_next/image?url=https%3A%2F%2Fh8DxKfmAPhn8O0p3.public.blob.vercel-storage.com%2Fdocs%2Fdark%2Fmdx-files.png&w=3840&q=75)

[`generateStaticParams`](https://nextjs.org/docs/app/api-reference/functions/generate-static-params) can be used to prerender the provided routes. By marking `dynamicParams` as `false`, accessing a route not defined in `generateStaticParams` will 404.

```
<span><span>export</span><span> </span><span>default</span><span> </span><span>async</span><span> </span><span>function</span><span> </span><span>Page</span><span>({</span></span>
<span><span>  params</span><span>,</span></span>
<span><span>}</span><span>:</span><span> {</span></span>
<span><span>  params</span><span>:</span><span> </span><span>Promise</span><span>&lt;{ slug</span><span>:</span><span> </span><span>string</span><span> }&gt;</span></span>
<span><span>}) {</span></span>
<span><span>  </span><span>const</span><span> { </span><span>slug</span><span> } </span><span>=</span><span> </span><span>await</span><span> params</span></span>
<span><span>  </span><span>const</span><span> { default: </span><span>Post</span><span> } </span><span>=</span><span> </span><span>await</span><span> </span><span>import</span><span>(</span><span>`@/content/</span><span>${</span><span>slug</span><span>}</span><span>.mdx`</span><span>)</span></span>
<span> </span>
<span><span>  </span><span>return</span><span> &lt;</span><span>Post</span><span> /&gt;</span></span>
<span><span>}</span></span>
<span> </span>
<span><span>export</span><span> </span><span>function</span><span> </span><span>generateStaticParams</span><span>() {</span></span>
<span><span>  </span><span>return</span><span> [{ slug</span><span>:</span><span> </span><span>'welcome'</span><span> }</span><span>,</span><span> { slug</span><span>:</span><span> </span><span>'about'</span><span> }]</span></span>
<span><span>}</span></span>
<span> </span>
<span><span>export</span><span> </span><span>const</span><span> </span><span>dynamicParams</span><span> </span><span>=</span><span> </span><span>false</span></span>
```

> **Good to know**: Ensure you specify the `.mdx` file extension in your import. While it is not required to use [module path aliases](https://nextjs.org/docs/app/getting-started/installation#set-up-absolute-imports-and-module-path-aliases) (e.g., `@/content`), it does simplify your import path.

## [Using custom styles and components](https://nextjs.org/docs/app/guides/mdx#using-custom-styles-and-components)

Markdown, when rendered, maps to native HTML elements. For example, writing the following markdown:

```
<span><span>## This is a heading</span></span>
<span> </span>
<span><span>This is a list in markdown:</span></span>
<span> </span>
<span><span>- One</span></span>
<span><span>- Two</span></span>
<span><span>- Three</span></span>
```

Generates the following HTML:

```
<span><span>&lt;</span><span>h2</span><span>&gt;This is a heading&lt;/</span><span>h2</span><span>&gt;</span></span>
<span> </span>
<span><span>&lt;</span><span>p</span><span>&gt;This is a list in markdown:&lt;/</span><span>p</span><span>&gt;</span></span>
<span> </span>
<span><span>&lt;</span><span>ul</span><span>&gt;</span></span>
<span><span>  &lt;</span><span>li</span><span>&gt;One&lt;/</span><span>li</span><span>&gt;</span></span>
<span><span>  &lt;</span><span>li</span><span>&gt;Two&lt;/</span><span>li</span><span>&gt;</span></span>
<span><span>  &lt;</span><span>li</span><span>&gt;Three&lt;/</span><span>li</span><span>&gt;</span></span>
<span><span>&lt;/</span><span>ul</span><span>&gt;</span></span>
```

To style your markdown, you can provide custom components that map to the generated HTML elements. Styles and components can be implemented globally, locally, and with shared layouts.

### [Global styles and components](https://nextjs.org/docs/app/guides/mdx#global-styles-and-components)

Adding styles and components in `mdx-components.tsx` will affect _all_ MDX files in your application.

```
<span><span>import</span><span> </span><span>type</span><span> { MDXComponents } </span><span>from</span><span> </span><span>'mdx/types'</span></span>
<span><span>import</span><span> Image</span><span>,</span><span> { ImageProps } </span><span>from</span><span> </span><span>'next/image'</span></span>
<span> </span>
<span><span>// This file allows you to provide custom React components</span></span>
<span><span>// to be used in MDX files. You can import and use any</span></span>
<span><span>// React component you want, including inline styles,</span></span>
<span><span>// components from other libraries, and more.</span></span>
<span> </span>
<span><span>export</span><span> </span><span>function</span><span> </span><span>useMDXComponents</span><span>(components</span><span>:</span><span> </span><span>MDXComponents</span><span>)</span><span>:</span><span> </span><span>MDXComponents</span><span> {</span></span>
<span><span>  </span><span>return</span><span> {</span></span>
<span><span>    </span><span>// Allows customizing built-in components, e.g. to add styling.</span></span>
<span><span>    </span><span>h1</span><span>:</span><span> ({ children }) </span><span>=&gt;</span><span> (</span></span>
<span><span>      &lt;</span><span>h1</span><span> </span><span>style</span><span>=</span><span>{{ color</span><span>:</span><span> </span><span>'red'</span><span>,</span><span> fontSize</span><span>:</span><span> </span><span>'48px'</span><span> }}&gt;{children}&lt;/</span><span>h1</span><span>&gt;</span></span>
<span><span>    )</span><span>,</span></span>
<span><span>    </span><span>img</span><span>:</span><span> (props) </span><span>=&gt;</span><span> (</span></span>
<span><span>      &lt;</span><span>Image</span></span>
<span><span>        </span><span>sizes</span><span>=</span><span>"100vw"</span></span>
<span><span>        </span><span>style</span><span>=</span><span>{{ width</span><span>:</span><span> </span><span>'100%'</span><span>,</span><span> height</span><span>:</span><span> </span><span>'auto'</span><span> }}</span></span>
<span><span>        {</span><span>...</span><span>(props </span><span>as</span><span> </span><span>ImageProps</span><span>)}</span></span>
<span><span>      /&gt;</span></span>
<span><span>    )</span><span>,</span></span>
<span><span>    </span><span>...</span><span>components</span><span>,</span></span>
<span><span>  }</span></span>
<span><span>}</span></span>
```

### [Local styles and components](https://nextjs.org/docs/app/guides/mdx#local-styles-and-components)

You can apply local styles and components to specific pages by passing them into imported MDX components. These will merge with and override [global styles and components](https://nextjs.org/docs/app/guides/mdx#global-styles-and-components).

```
<span><span>import</span><span> Welcome </span><span>from</span><span> </span><span>'@/markdown/welcome.mdx'</span></span>
<span> </span>
<span><span>function</span><span> </span><span>CustomH1</span><span>({ children }) {</span></span>
<span><span>  </span><span>return</span><span> &lt;</span><span>h1</span><span> </span><span>style</span><span>=</span><span>{{ color</span><span>:</span><span> </span><span>'blue'</span><span>,</span><span> fontSize</span><span>:</span><span> </span><span>'100px'</span><span> }}&gt;{children}&lt;/</span><span>h1</span><span>&gt;</span></span>
<span><span>}</span></span>
<span> </span>
<span><span>const</span><span> </span><span>overrideComponents</span><span> </span><span>=</span><span> {</span></span>
<span><span>  h1</span><span>:</span><span> CustomH1</span><span>,</span></span>
<span><span>}</span></span>
<span> </span>
<span><span>export</span><span> </span><span>default</span><span> </span><span>function</span><span> </span><span>Page</span><span>() {</span></span>
<span><span>  </span><span>return</span><span> &lt;</span><span>Welcome</span><span> </span><span>components</span><span>=</span><span>{overrideComponents} /&gt;</span></span>
<span><span>}</span></span>
```

### [Shared layouts](https://nextjs.org/docs/app/guides/mdx#shared-layouts)

To share a layout across MDX pages, you can use the [built-in layouts support](https://nextjs.org/docs/app/building-your-application/routing/layouts-and-templates#layouts) with the App Router.

```
<span><span>export</span><span> </span><span>default</span><span> </span><span>function</span><span> </span><span>MdxLayout</span><span>({ children }</span><span>:</span><span> { children</span><span>:</span><span> </span><span>React</span><span>.</span><span>ReactNode</span><span> }) {</span></span>
<span><span>  </span><span>// Create any shared layout or styles here</span></span>
<span><span>  </span><span>return</span><span> &lt;</span><span>div</span><span> </span><span>style</span><span>=</span><span>{{ color</span><span>:</span><span> </span><span>'blue'</span><span> }}&gt;{children}&lt;/</span><span>div</span><span>&gt;</span></span>
<span><span>}</span></span>
```

### [Using Tailwind typography plugin](https://nextjs.org/docs/app/guides/mdx#using-tailwind-typography-plugin)

If you are using [Tailwind](https://tailwindcss.com/) to style your application, using the [`@tailwindcss/typography` plugin](https://tailwindcss.com/docs/plugins#typography) will allow you to reuse your Tailwind configuration and styles in your markdown files.

The plugin adds a set of `prose` classes that can be used to add typographic styles to content blocks that come from sources, like markdown.

[Install Tailwind typography](https://github.com/tailwindlabs/tailwindcss-typography?tab=readme-ov-file#installation) and use with [shared layouts](https://nextjs.org/docs/app/guides/mdx#shared-layouts) to add the `prose` you want.

```
<span><span>export</span><span> </span><span>default</span><span> </span><span>function</span><span> </span><span>MdxLayout</span><span>({ children }</span><span>:</span><span> { children</span><span>:</span><span> </span><span>React</span><span>.</span><span>ReactNode</span><span> }) {</span></span>
<span><span>  </span><span>// Create any shared layout or styles here</span></span>
<span><span>  </span><span>return</span><span> (</span></span>
<span><span>    &lt;</span><span>div</span><span> </span><span>className</span><span>=</span><span>"prose prose-headings:mt-8 prose-headings:font-semibold prose-headings:text-black prose-h1:text-5xl prose-h2:text-4xl prose-h3:text-3xl prose-h4:text-2xl prose-h5:text-xl prose-h6:text-lg dark:prose-headings:text-white"</span><span>&gt;</span></span>
<span><span>      {children}</span></span>
<span><span>    &lt;/</span><span>div</span><span>&gt;</span></span>
<span><span>  )</span></span>
<span><span>}</span></span>
```

## [Frontmatter](https://nextjs.org/docs/app/guides/mdx#frontmatter)

Frontmatter is a YAML like key/value pairing that can be used to store data about a page. `@next/mdx` does **not** support frontmatter by default, though there are many solutions for adding frontmatter to your MDX content, such as:

-   [remark-frontmatter](https://github.com/remarkjs/remark-frontmatter)
-   [remark-mdx-frontmatter](https://github.com/remcohaszing/remark-mdx-frontmatter)
-   [gray-matter](https://github.com/jonschlinkert/gray-matter)

`@next/mdx` **does** allow you to use exports like any other JavaScript component:

Metadata can now be referenced outside of the MDX file:

```
<span><span>import</span><span> BlogPost</span><span>,</span><span> { metadata } </span><span>from</span><span> </span><span>'@/content/</span><span>blog</span><span>-post.mdx'</span></span>
<span> </span>
<span><span>export</span><span> </span><span>default</span><span> </span><span>function</span><span> </span><span>Page</span><span>() {</span></span>
<span><span>  </span><span>console</span><span>.log</span><span>(</span><span>'metadata: '</span><span>,</span><span> metadata)</span></span>
<span><span>  </span><span>//=&gt; { author: 'John Doe' }</span></span>
<span><span>  </span><span>return</span><span> &lt;</span><span>BlogPost</span><span> /&gt;</span></span>
<span><span>}</span></span>
```

A common use case for this is when you want to iterate over a collection of MDX and extract data. For example, creating a blog index page from all blog posts. You can use packages like [Node's `fs` module](https://nodejs.org/api/fs.html) or [globby](https://www.npmjs.com/package/globby) to read a directory of posts and extract the metadata.

> **Good to know**:
> 
> -   Using `fs`, `globby`, etc. can only be used server-side.
> -   View the [Portfolio Starter Kit](https://vercel.com/templates/next.js/portfolio-starter-kit) template for a complete working example.

## [remark and rehype Plugins](https://nextjs.org/docs/app/guides/mdx#remark-and-rehype-plugins)

You can optionally provide remark and rehype plugins to transform the MDX content.

For example, you can use [`remark-gfm`](https://github.com/remarkjs/remark-gfm) to support GitHub Flavored Markdown.

Since the remark and rehype ecosystem is ESM only, you'll need to use `next.config.mjs` or `next.config.ts` as the configuration file.

```
<span><span>import</span><span> remarkGfm </span><span>from</span><span> </span><span>'remark-gfm'</span></span>
<span><span>import</span><span> createMDX </span><span>from</span><span> </span><span>'@next/mdx'</span></span>
<span> </span>
<span><span>/** </span><span>@type</span><span> </span><span>{import('next').NextConfig}</span><span> */</span></span>
<span><span>const</span><span> </span><span>nextConfig</span><span> </span><span>=</span><span> {</span></span>
<span><span>  </span><span>// Allow .mdx extensions for files</span></span>
<span><span>  pageExtensions</span><span>:</span><span> [</span><span>'js'</span><span>,</span><span> </span><span>'jsx'</span><span>,</span><span> </span><span>'md'</span><span>,</span><span> </span><span>'mdx'</span><span>,</span><span> </span><span>'ts'</span><span>,</span><span> </span><span>'tsx'</span><span>]</span><span>,</span></span>
<span><span>  </span><span>// Optionally, add any other Next.js config below</span></span>
<span><span>}</span></span>
<span> </span>
<span><span>const</span><span> </span><span>withMDX</span><span> </span><span>=</span><span> </span><span>createMDX</span><span>({</span></span>
<span><span>  </span><span>// Add markdown plugins here, as desired</span></span>
<span><span>  options</span><span>:</span><span> {</span></span>
<span><span>    remarkPlugins</span><span>:</span><span> [remarkGfm]</span><span>,</span></span>
<span><span>    rehypePlugins</span><span>:</span><span> []</span><span>,</span></span>
<span><span>  }</span><span>,</span></span>
<span><span>})</span></span>
<span> </span>
<span><span>// Combine MDX and Next.js config</span></span>
<span><span>export</span><span> </span><span>default</span><span> </span><span>withMDX</span><span>(nextConfig)</span></span>
```

### [Using Plugins with Turbopack](https://nextjs.org/docs/app/guides/mdx#using-plugins-with-turbopack)

To use plugins with [Turbopack](https://nextjs.org/docs/app/api-reference/turbopack), upgrade to the latest `@next/mdx` and specify plugin names using a string:

```
<span><span>import</span><span> createMDX </span><span>from</span><span> </span><span>'@next/mdx'</span></span>
<span> </span>
<span><span>/** </span><span>@type</span><span> </span><span>{import('next').NextConfig}</span><span> */</span></span>
<span><span>const</span><span> </span><span>nextConfig</span><span> </span><span>=</span><span> {</span></span>
<span><span>  pageExtensions</span><span>:</span><span> [</span><span>'js'</span><span>,</span><span> </span><span>'jsx'</span><span>,</span><span> </span><span>'md'</span><span>,</span><span> </span><span>'mdx'</span><span>,</span><span> </span><span>'ts'</span><span>,</span><span> </span><span>'tsx'</span><span>]</span><span>,</span></span>
<span><span>}</span></span>
<span> </span>
<span><span>const</span><span> </span><span>withMDX</span><span> </span><span>=</span><span> </span><span>createMDX</span><span>({</span></span>
<span><span>  options</span><span>:</span><span> {</span></span>
<span><span>    remarkPlugins</span><span>:</span><span> []</span><span>,</span></span>
<span><span>    rehypePlugins</span><span>:</span><span> [[</span><span>'rehype-katex'</span><span>,</span><span> { strict</span><span>:</span><span> </span><span>true</span><span>,</span><span> throwOnError</span><span>:</span><span> </span><span>true</span><span> }]]</span><span>,</span></span>
<span><span>  }</span><span>,</span></span>
<span><span>})</span></span>
<span> </span>
<span><span>export</span><span> </span><span>default</span><span> </span><span>withMDX</span><span>(nextConfig)</span></span>
```

> **Good to know**:
> 
> remark and rehype plugins without serializable options cannot be used yet with [Turbopack](https://nextjs.org/docs/app/api-reference/turbopack), due to [inability to pass JavaScript functions to Rust](https://github.com/vercel/next.js/issues/71819#issuecomment-2461802968)

## [Remote MDX](https://nextjs.org/docs/app/guides/mdx#remote-mdx)

If your MDX files or content lives _somewhere else_, you can fetch it dynamically on the server. This is useful for content stored in a CMS, database, or anywhere else. A popular community package for this use is [`next-mdx-remote`](https://github.com/hashicorp/next-mdx-remote#react-server-components-rsc--nextjs-app-directory-support).

> **Good to know**: Please proceed with caution. MDX compiles to JavaScript and is executed on the server. You should only fetch MDX content from a trusted source, otherwise this can lead to remote code execution (RCE).

The following example uses `next-mdx-remote`:

```
<span><span>import</span><span> { MDXRemote } </span><span>from</span><span> </span><span>'next-mdx-remote/rsc'</span></span>
<span> </span>
<span><span>export</span><span> </span><span>default</span><span> </span><span>async</span><span> </span><span>function</span><span> </span><span>RemoteMdxPage</span><span>() {</span></span>
<span><span>  </span><span>// MDX text - can be from a database, CMS, fetch, anywhere...</span></span>
<span><span>  </span><span>const</span><span> </span><span>res</span><span> </span><span>=</span><span> </span><span>await</span><span> </span><span>fetch</span><span>(</span><span>'https://...'</span><span>)</span></span>
<span><span>  </span><span>const</span><span> </span><span>markdown</span><span> </span><span>=</span><span> </span><span>await</span><span> </span><span>res</span><span>.text</span><span>()</span></span>
<span><span>  </span><span>return</span><span> &lt;</span><span>MDXRemote</span><span> </span><span>source</span><span>=</span><span>{markdown} /&gt;</span></span>
<span><span>}</span></span>
```

Navigating to the `/mdx-page-remote` route should display your rendered MDX.

## [Deep Dive: How do you transform markdown into HTML?](https://nextjs.org/docs/app/guides/mdx#deep-dive-how-do-you-transform-markdown-into-html)

React does not natively understand markdown. The markdown plaintext needs to first be transformed into HTML. This can be accomplished with `remark` and `rehype`.

`remark` is an ecosystem of tools around markdown. `rehype` is the same, but for HTML. For example, the following code snippet transforms markdown into HTML:

```
<span><span>import</span><span> { unified } </span><span>from</span><span> </span><span>'unified'</span></span>
<span><span>import</span><span> remarkParse </span><span>from</span><span> </span><span>'remark-parse'</span></span>
<span><span>import</span><span> remarkRehype </span><span>from</span><span> </span><span>'remark-rehype'</span></span>
<span><span>import</span><span> rehypeSanitize </span><span>from</span><span> </span><span>'rehype-sanitize'</span></span>
<span><span>import</span><span> rehypeStringify </span><span>from</span><span> </span><span>'rehype-stringify'</span></span>
<span> </span>
<span><span>main</span><span>()</span></span>
<span> </span>
<span><span>async</span><span> </span><span>function</span><span> </span><span>main</span><span>() {</span></span>
<span><span>  </span><span>const</span><span> </span><span>file</span><span> </span><span>=</span><span> </span><span>await</span><span> </span><span>unified</span><span>()</span></span>
<span><span>    </span><span>.use</span><span>(remarkParse) </span><span>// Convert into markdown AST</span></span>
<span><span>    </span><span>.use</span><span>(remarkRehype) </span><span>// Transform to HTML AST</span></span>
<span><span>    </span><span>.use</span><span>(rehypeSanitize) </span><span>// Sanitize HTML input</span></span>
<span><span>    </span><span>.use</span><span>(rehypeStringify) </span><span>// Convert AST into serialized HTML</span></span>
<span><span>    </span><span>.process</span><span>(</span><span>'Hello, Next.js!'</span><span>)</span></span>
<span> </span>
<span><span>  </span><span>console</span><span>.log</span><span>(</span><span>String</span><span>(file)) </span><span>// &lt;p&gt;Hello, Next.js!&lt;/p&gt;</span></span>
<span><span>}</span></span>
```

The `remark` and `rehype` ecosystem contains plugins for [syntax highlighting](https://github.com/atomiks/rehype-pretty-code), [linking headings](https://github.com/rehypejs/rehype-autolink-headings), [generating a table of contents](https://github.com/remarkjs/remark-toc), and more.

When using `@next/mdx` as shown above, you **do not** need to use `remark` or `rehype` directly, as it is handled for you. We're describing it here for a deeper understanding of what the `@next/mdx` package is doing underneath.

## [Using the Rust-based MDX compiler (experimental)](https://nextjs.org/docs/app/guides/mdx#using-the-rust-based-mdx-compiler-experimental)

Next.js supports a new MDX compiler written in Rust. This compiler is still experimental and is not recommended for production use. To use the new compiler, you need to configure `next.config.js` when you pass it to `withMDX`:

```
<span><span>module</span><span>.</span><span>exports</span><span> </span><span>=</span><span> </span><span>withMDX</span><span>({</span></span>
<span><span>  experimental</span><span>:</span><span> {</span></span>
<span><span>    mdxRs</span><span>:</span><span> </span><span>true</span><span>,</span></span>
<span><span>  }</span><span>,</span></span>
<span><span>})</span></span>
```

`mdxRs` also accepts an object to configure how to transform mdx files.

```
<span><span>module</span><span>.</span><span>exports</span><span> </span><span>=</span><span> </span><span>withMDX</span><span>({</span></span>
<span><span>  experimental</span><span>:</span><span> {</span></span>
<span><span>    mdxRs</span><span>:</span><span> {</span></span>
<span><span>      jsxRuntime?</span><span>:</span><span> string            </span><span>// Custom jsx runtime</span></span>
<span><span>      jsxImportSource</span><span>?:</span><span> string       </span><span>// Custom jsx import source,</span></span>
<span><span>      mdxType</span><span>?:</span><span> </span><span>'gfm'</span><span> </span><span>|</span><span> </span><span>'commonmark'</span><span> </span><span>// Configure what kind of mdx syntax will be used to parse &amp; transform</span></span>
<span><span>    }</span><span>,</span></span>
<span><span>  }</span><span>,</span></span>
<span><span>})</span></span>
```

## [Helpful Links](https://nextjs.org/docs/app/guides/mdx#helpful-links)

-   [MDX](https://mdxjs.com/)
-   [`@next/mdx`](https://www.npmjs.com/package/@next/mdx)
-   [remark](https://github.com/remarkjs/remark)
-   [rehype](https://github.com/rehypejs/rehype)
-   [Markdoc](https://markdoc.dev/docs/nextjs)