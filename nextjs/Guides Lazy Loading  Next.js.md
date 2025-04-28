## How to lazy load Client Components and libraries

[Lazy loading](https://developer.mozilla.org/docs/Web/Performance/Lazy_loading) in Next.js helps improve the initial loading performance of an application by decreasing the amount of JavaScript needed to render a route.

It allows you to defer loading of **Client Components** and imported libraries, and only include them in the client bundle when they're needed. For example, you might want to defer loading a modal until a user clicks to open it.

There are two ways you can implement lazy loading in Next.js:

1.  Using [Dynamic Imports](https://nextjs.org/docs/app/guides/lazy-loading#nextdynamic) with `next/dynamic`
2.  Using [`React.lazy()`](https://react.dev/reference/react/lazy) with [Suspense](https://react.dev/reference/react/Suspense)

By default, Server Components are automatically [code split](https://developer.mozilla.org/docs/Glossary/Code_splitting), and you can use [streaming](https://nextjs.org/docs/app/building-your-application/routing/loading-ui-and-streaming) to progressively send pieces of UI from the server to the client. Lazy loading applies to Client Components.

## [`next/dynamic`](https://nextjs.org/docs/app/guides/lazy-loading#nextdynamic)

`next/dynamic` is a composite of [`React.lazy()`](https://react.dev/reference/react/lazy) and [Suspense](https://react.dev/reference/react/Suspense). It behaves the same way in the `app` and `pages` directories to allow for incremental migration.

## [Examples](https://nextjs.org/docs/app/guides/lazy-loading#examples)

### [Importing Client Components](https://nextjs.org/docs/app/guides/lazy-loading#importing-client-components)

```
<span><span>'use client'</span></span>
<span> </span>
<span><span>import</span><span> { useState } </span><span>from</span><span> </span><span>'react'</span></span>
<span><span>import</span><span> dynamic </span><span>from</span><span> </span><span>'next/dynamic'</span></span>
<span> </span>
<span><span>// Client Components:</span></span>
<span><span>const</span><span> </span><span>ComponentA</span><span> </span><span>=</span><span> </span><span>dynamic</span><span>(() </span><span>=&gt;</span><span> </span><span>import</span><span>(</span><span>'../components/A'</span><span>))</span></span>
<span><span>const</span><span> </span><span>ComponentB</span><span> </span><span>=</span><span> </span><span>dynamic</span><span>(() </span><span>=&gt;</span><span> </span><span>import</span><span>(</span><span>'../components/B'</span><span>))</span></span>
<span><span>const</span><span> </span><span>ComponentC</span><span> </span><span>=</span><span> </span><span>dynamic</span><span>(() </span><span>=&gt;</span><span> </span><span>import</span><span>(</span><span>'../components/C'</span><span>)</span><span>,</span><span> { ssr</span><span>:</span><span> </span><span>false</span><span> })</span></span>
<span> </span>
<span><span>export</span><span> </span><span>default</span><span> </span><span>function</span><span> </span><span>ClientComponentExample</span><span>() {</span></span>
<span><span>  </span><span>const</span><span> [</span><span>showMore</span><span>,</span><span> </span><span>setShowMore</span><span>] </span><span>=</span><span> </span><span>useState</span><span>(</span><span>false</span><span>)</span></span>
<span> </span>
<span><span>  </span><span>return</span><span> (</span></span>
<span><span>    &lt;</span><span>div</span><span>&gt;</span></span>
<span><span>      {</span><span>/* Load immediately, but in a separate client bundle */</span><span>}</span></span>
<span><span>      &lt;</span><span>ComponentA</span><span> /&gt;</span></span>
<span> </span>
<span><span>      {</span><span>/* Load on demand, only when/if the condition is met */</span><span>}</span></span>
<span><span>      {showMore </span><span>&amp;&amp;</span><span> &lt;</span><span>ComponentB</span><span> /&gt;}</span></span>
<span><span>      &lt;</span><span>button</span><span> </span><span>onClick</span><span>=</span><span>{() </span><span>=&gt;</span><span> </span><span>setShowMore</span><span>(</span><span>!</span><span>showMore)}&gt;Toggle&lt;/</span><span>button</span><span>&gt;</span></span>
<span> </span>
<span><span>      {</span><span>/* Load only on the client side */</span><span>}</span></span>
<span><span>      &lt;</span><span>ComponentC</span><span> /&gt;</span></span>
<span><span>    &lt;/</span><span>div</span><span>&gt;</span></span>
<span><span>  )</span></span>
<span><span>}</span></span>
```

> **Note:** When a Server Component dynamically imports a Client Component, automatic [code splitting](https://developer.mozilla.org/docs/Glossary/Code_splitting) is currently **not** supported.

### [Skipping SSR](https://nextjs.org/docs/app/guides/lazy-loading#skipping-ssr)

When using `React.lazy()` and Suspense, Client Components will be [prerendered](https://github.com/reactwg/server-components/discussions/4) (SSR) by default.

> **Note:** `ssr: false` option will only work for Client Components, move it into Client Components ensure the client code-splitting working properly.

If you want to disable pre-rendering for a Client Component, you can use the `ssr` option set to `false`:

```
<span><span>const</span><span> </span><span>ComponentC</span><span> </span><span>=</span><span> </span><span>dynamic</span><span>(() </span><span>=&gt;</span><span> </span><span>import</span><span>(</span><span>'../components/C'</span><span>)</span><span>,</span><span> { ssr</span><span>:</span><span> </span><span>false</span><span> })</span></span>
```

### [Importing Server Components](https://nextjs.org/docs/app/guides/lazy-loading#importing-server-components)

If you dynamically import a Server Component, only the Client Components that are children of the Server Component will be lazy-loaded - not the Server Component itself. It will also help preload the static assets such as CSS when you're using it in Server Components.

```
<span><span>import</span><span> dynamic </span><span>from</span><span> </span><span>'next/dynamic'</span></span>
<span> </span>
<span><span>// Server Component:</span></span>
<span><span>const</span><span> </span><span>ServerComponent</span><span> </span><span>=</span><span> </span><span>dynamic</span><span>(() </span><span>=&gt;</span><span> </span><span>import</span><span>(</span><span>'../components/ServerComponent'</span><span>))</span></span>
<span> </span>
<span><span>export</span><span> </span><span>default</span><span> </span><span>function</span><span> </span><span>ServerComponentExample</span><span>() {</span></span>
<span><span>  </span><span>return</span><span> (</span></span>
<span><span>    &lt;</span><span>div</span><span>&gt;</span></span>
<span><span>      &lt;</span><span>ServerComponent</span><span> /&gt;</span></span>
<span><span>    &lt;/</span><span>div</span><span>&gt;</span></span>
<span><span>  )</span></span>
<span><span>}</span></span>
```

> **Note:** `ssr: false` option is not supported in Server Components. You will see an error if you try to use it in Server Components. `ssr: false` is not allowed with `next/dynamic` in Server Components. Please move it into a Client Component.

### [Loading External Libraries](https://nextjs.org/docs/app/guides/lazy-loading#loading-external-libraries)

External libraries can be loaded on demand using the [`import()`](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Operators/import) function. This example uses the external library `fuse.js` for fuzzy search. The module is only loaded on the client after the user types in the search input.

```
<span><span>'use client'</span></span>
<span> </span>
<span><span>import</span><span> { useState } </span><span>from</span><span> </span><span>'react'</span></span>
<span> </span>
<span><span>const</span><span> </span><span>names</span><span> </span><span>=</span><span> [</span><span>'Tim'</span><span>,</span><span> </span><span>'Joe'</span><span>,</span><span> </span><span>'Bel'</span><span>,</span><span> </span><span>'Lee'</span><span>]</span></span>
<span> </span>
<span><span>export</span><span> </span><span>default</span><span> </span><span>function</span><span> </span><span>Page</span><span>() {</span></span>
<span><span>  </span><span>const</span><span> [</span><span>results</span><span>,</span><span> </span><span>setResults</span><span>] </span><span>=</span><span> </span><span>useState</span><span>()</span></span>
<span> </span>
<span><span>  </span><span>return</span><span> (</span></span>
<span><span>    &lt;</span><span>div</span><span>&gt;</span></span>
<span><span>      &lt;</span><span>input</span></span>
<span><span>        </span><span>type</span><span>=</span><span>"text"</span></span>
<span><span>        </span><span>placeholder</span><span>=</span><span>"Search"</span></span>
<span><span>        </span><span>onChange</span><span>=</span><span>{</span><span>async</span><span> (e) </span><span>=&gt;</span><span> {</span></span>
<span><span>          </span><span>const</span><span> { </span><span>value</span><span> } </span><span>=</span><span> </span><span>e</span><span>.currentTarget</span></span>
<span><span>          </span><span>// Dynamically load fuse.js</span></span>
<span><span>          </span><span>const</span><span> </span><span>Fuse</span><span> </span><span>=</span><span> (</span><span>await</span><span> </span><span>import</span><span>(</span><span>'fuse.js'</span><span>)).default</span></span>
<span><span>          </span><span>const</span><span> </span><span>fuse</span><span> </span><span>=</span><span> </span><span>new</span><span> </span><span>Fuse</span><span>(names)</span></span>
<span> </span>
<span><span>          </span><span>setResults</span><span>(</span><span>fuse</span><span>.search</span><span>(value))</span></span>
<span><span>        }}</span></span>
<span><span>      /&gt;</span></span>
<span><span>      &lt;</span><span>pre</span><span>&gt;Results: {</span><span>JSON</span><span>.stringify</span><span>(results</span><span>,</span><span> </span><span>null</span><span>,</span><span> </span><span>2</span><span>)}&lt;/</span><span>pre</span><span>&gt;</span></span>
<span><span>    &lt;/</span><span>div</span><span>&gt;</span></span>
<span><span>  )</span></span>
<span><span>}</span></span>
```

### [Adding a custom loading component](https://nextjs.org/docs/app/guides/lazy-loading#adding-a-custom-loading-component)

```
<span><span>'use client'</span></span>
<span> </span>
<span><span>import</span><span> dynamic </span><span>from</span><span> </span><span>'next/dynamic'</span></span>
<span> </span>
<span><span>const</span><span> </span><span>WithCustomLoading</span><span> </span><span>=</span><span> </span><span>dynamic</span><span>(</span></span>
<span><span>  () </span><span>=&gt;</span><span> </span><span>import</span><span>(</span><span>'../components/WithCustomLoading'</span><span>)</span><span>,</span></span>
<span><span>  {</span></span>
<span><span>    </span><span>loading</span><span>:</span><span> () </span><span>=&gt;</span><span> &lt;</span><span>p</span><span>&gt;Loading...&lt;/</span><span>p</span><span>&gt;</span><span>,</span></span>
<span><span>  }</span></span>
<span><span>)</span></span>
<span> </span>
<span><span>export</span><span> </span><span>default</span><span> </span><span>function</span><span> </span><span>Page</span><span>() {</span></span>
<span><span>  </span><span>return</span><span> (</span></span>
<span><span>    &lt;</span><span>div</span><span>&gt;</span></span>
<span><span>      {</span><span>/* The loading component will be rendered while  &lt;WithCustomLoading/&gt; is loading */</span><span>}</span></span>
<span><span>      &lt;</span><span>WithCustomLoading</span><span> /&gt;</span></span>
<span><span>    &lt;/</span><span>div</span><span>&gt;</span></span>
<span><span>  )</span></span>
<span><span>}</span></span>
```

### [Importing Named Exports](https://nextjs.org/docs/app/guides/lazy-loading#importing-named-exports)

To dynamically import a named export, you can return it from the Promise returned by [`import()`](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Operators/import) function:

```
<span><span>'use client'</span></span>
<span> </span>
<span><span>export</span><span> </span><span>function</span><span> </span><span>Hello</span><span>() {</span></span>
<span><span>  </span><span>return</span><span> &lt;</span><span>p</span><span>&gt;Hello!&lt;/</span><span>p</span><span>&gt;</span></span>
<span><span>}</span></span>
```

```
<span><span>import</span><span> dynamic </span><span>from</span><span> </span><span>'next/dynamic'</span></span>
<span> </span>
<span><span>const</span><span> </span><span>ClientComponent</span><span> </span><span>=</span><span> </span><span>dynamic</span><span>(() </span><span>=&gt;</span></span>
<span><span>  </span><span>import</span><span>(</span><span>'../components/hello'</span><span>)</span><span>.then</span><span>((mod) </span><span>=&gt;</span><span> </span><span>mod</span><span>.Hello)</span></span>
<span><span>)</span></span>
```