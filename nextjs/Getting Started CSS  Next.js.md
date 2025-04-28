## How to use CSS in your application

Next.js provides several ways to use CSS in your application, including:

-   [CSS Modules](https://nextjs.org/docs/app/getting-started/css#css-modules)
-   [Global CSS](https://nextjs.org/docs/app/getting-started/css#global-css)
-   [Tailwind CSS](https://nextjs.org/docs/app/getting-started/css#tailwind-css)
-   [Sass](https://nextjs.org/docs/app/guides/sass)
-   [CSS-in-JS](https://nextjs.org/docs/app/guides/css-in-js)
-   [External Stylesheets](https://nextjs.org/docs/app/getting-started/css#external-stylesheets)

## [CSS Modules](https://nextjs.org/docs/app/getting-started/css#css-modules)

CSS Modules locally scope CSS by generating unique class names. This allows you to use the same class in different files without worrying about naming collisions.

To start using CSS Modules, create a new file with the extension `.module.css` and import it into any component inside the `app` directory:

```
<span><span>import</span><span> styles </span><span>from</span><span> </span><span>'./styles.module.css'</span></span>
<span> </span>
<span><span>export</span><span> </span><span>default</span><span> </span><span>function</span><span> </span><span>Page</span><span>({ children }</span><span>:</span><span> { children</span><span>:</span><span> </span><span>React</span><span>.</span><span>ReactNode</span><span> }) {</span></span>
<span><span>  </span><span>return</span><span> &lt;</span><span>main</span><span> </span><span>className</span><span>=</span><span>{</span><span>styles</span><span>.</span><span>blog</span><span>}&gt;{children}&lt;/</span><span>main</span><span>&gt;</span></span>
<span><span>}</span></span>
```

## [Global CSS](https://nextjs.org/docs/app/getting-started/css#global-css)

You can use global CSS to apply styles across your application.

To use global styles, create a `app/global.css` file and import it in the root layout to apply the styles to **every route** in your application:

```
<span><span>body</span><span> {</span></span>
<span><span>  </span><span>padding</span><span>:</span><span> </span><span>20</span><span>px</span><span> 20</span><span>px</span><span> 60</span><span>px</span><span>;</span></span>
<span><span>  </span><span>max-width</span><span>:</span><span> </span><span>680</span><span>px</span><span>;</span></span>
<span><span>  </span><span>margin</span><span>:</span><span> </span><span>0 auto</span><span>;</span></span>
<span><span>}</span></span>
```

```
<span><span>// These styles apply to every route in the application</span></span>
<span><span>import</span><span> </span><span>'./global.css'</span></span>
<span> </span>
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

> **Good to know:** Global styles can be imported into any layout, page, or component inside the `app` directory. However, since Next.js uses React's built-in support for stylesheets to integrate with Suspense, this currently does not remove stylesheets as you navigate between routes which can lead to conflicts. We recommend using global styles for _truly_ global CSS, and [CSS Modules](https://nextjs.org/docs/app/getting-started/css#css-modules) for scoped CSS.

## [Tailwind CSS](https://nextjs.org/docs/app/getting-started/css#tailwind-css)

[Tailwind CSS](https://tailwindcss.com/) is a utility-first CSS framework that integrates seamlessly with Next.js.

### [Installing Tailwind](https://nextjs.org/docs/app/getting-started/css#installing-tailwind)

To start using Tailwind, install the necessary Tailwind CSS packages:

```
<span><span>npm</span><span> </span><span>install</span><span> </span><span>tailwindcss</span><span> </span><span>@tailwindcss/postcss</span><span> </span><span>postcss</span></span>
```

### [Configuring Tailwind](https://nextjs.org/docs/app/getting-started/css#configuring-tailwind)

Create a `postcss.config.mjs` file in the root of your project and add the `@tailwindcss/postcss` plugin to your PostCSS configuration:

```
<span><span>/** </span><span>@type</span><span> </span><span>{import('tailwindcss').Config}</span><span> */</span></span>
<span><span>export</span><span> </span><span>default</span><span> {</span></span>
<span><span>  plugins</span><span>:</span><span> {</span></span>
<span><span>    </span><span>'@tailwindcss/postcss'</span><span>:</span><span> {}</span><span>,</span></span>
<span><span>  }</span><span>,</span></span>
<span><span>}</span></span>
```

### [Using Tailwind](https://nextjs.org/docs/app/getting-started/css#using-tailwind)

Add the [Tailwind directives](https://tailwindcss.com/docs/functions-and-directives#directives) to your [Global Stylesheet](https://nextjs.org/docs/app/getting-started/css#global-css):

Then, import the styles in the [root layout](https://nextjs.org/docs/app/api-reference/file-conventions/layout#root-layouts):

```
<span><span>import</span><span> </span><span>type</span><span> { Metadata } </span><span>from</span><span> </span><span>'next'</span></span>
<span><span>// These styles apply to every route in the application</span></span>
<span><span>import</span><span> </span><span>'./globals.css'</span></span>
<span> </span>
<span><span>export</span><span> </span><span>const</span><span> </span><span>metadata</span><span>:</span><span> </span><span>Metadata</span><span> </span><span>=</span><span> {</span></span>
<span><span>  title</span><span>:</span><span> </span><span>'Create Next App'</span><span>,</span></span>
<span><span>  description</span><span>:</span><span> </span><span>'Generated by create next app'</span><span>,</span></span>
<span><span>}</span></span>
<span> </span>
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

You can then start writing Tailwind's utility classes in your application.

```
<span><span>export</span><span> </span><span>default</span><span> </span><span>function</span><span> </span><span>Page</span><span>() {</span></span>
<span><span>  </span><span>return</span><span> &lt;</span><span>h1</span><span> </span><span>className</span><span>=</span><span>"text-3xl font-bold underline"</span><span>&gt;Hello, Next.js!&lt;/</span><span>h1</span><span>&gt;</span></span>
<span><span>}</span></span>
```

## [External stylesheets](https://nextjs.org/docs/app/getting-started/css#external-stylesheets)

Stylesheets published by external packages can be imported anywhere in the `app` directory, including colocated components:

```
<span><span>import</span><span> </span><span>'bootstrap/dist/css/bootstrap.css'</span></span>
<span> </span>
<span><span>export</span><span> </span><span>default</span><span> </span><span>function</span><span> </span><span>RootLayout</span><span>({</span></span>
<span><span>  children</span><span>,</span></span>
<span><span>}</span><span>:</span><span> {</span></span>
<span><span>  children</span><span>:</span><span> </span><span>React</span><span>.</span><span>ReactNode</span></span>
<span><span>}) {</span></span>
<span><span>  </span><span>return</span><span> (</span></span>
<span><span>    &lt;</span><span>html</span><span> </span><span>lang</span><span>=</span><span>"en"</span><span>&gt;</span></span>
<span><span>      &lt;</span><span>body</span><span> </span><span>className</span><span>=</span><span>"container"</span><span>&gt;{children}&lt;/</span><span>body</span><span>&gt;</span></span>
<span><span>    &lt;/</span><span>html</span><span>&gt;</span></span>
<span><span>  )</span></span>
<span><span>}</span></span>
```

External stylesheets must be directly imported from an npm package or downloaded and colocated with your codebase. You cannot use `<link rel="stylesheet" />`.