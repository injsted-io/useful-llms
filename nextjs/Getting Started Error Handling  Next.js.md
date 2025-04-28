## How to handle errors

Errors can be divided into two categories: [expected errors](https://nextjs.org/docs/app/getting-started/error-handling#handling-expected-errors) and [uncaught exceptions](https://nextjs.org/docs/app/getting-started/error-handling#handling-uncaught-exceptions). This page will walk you through how you can handle these errors in your Next.js application.

## [Handling expected errors](https://nextjs.org/docs/app/getting-started/error-handling#handling-expected-errors)

Expected errors are those that can occur during the normal operation of the application, such as those from [server-side form validation](https://nextjs.org/docs/app/building-your-application/data-fetching/server-actions-and-mutations#server-side-form-validation) or failed requests. These errors should be handled explicitly and returned to the client.

### [Server Functions](https://nextjs.org/docs/app/getting-started/error-handling#server-functions)

You can use the [`useActionState`](https://react.dev/reference/react/useActionState) hook to handle expected errors in [Server Functions](https://react.dev/reference/rsc/server-functions).

For these errors, avoid using `try`/`catch` blocks and throw errors. Instead, model expected errors as return values.

```
<span><span>'use server'</span></span>
<span> </span>
<span><span>export</span><span> </span><span>async</span><span> </span><span>function</span><span> </span><span>createPost</span><span>(prevState</span><span>:</span><span> </span><span>any</span><span>,</span><span> formData</span><span>:</span><span> </span><span>FormData</span><span>) {</span></span>
<span><span>  </span><span>const</span><span> </span><span>title</span><span> </span><span>=</span><span> </span><span>formData</span><span>.get</span><span>(</span><span>'title'</span><span>)</span></span>
<span><span>  </span><span>const</span><span> </span><span>content</span><span> </span><span>=</span><span> </span><span>formData</span><span>.get</span><span>(</span><span>'content'</span><span>)</span></span>
<span> </span>
<span><span>  </span><span>const</span><span> </span><span>res</span><span> </span><span>=</span><span> </span><span>await</span><span> </span><span>fetch</span><span>(</span><span>'https://api.vercel.app/posts'</span><span>,</span><span> {</span></span>
<span><span>    method</span><span>:</span><span> </span><span>'POST'</span><span>,</span></span>
<span><span>    body</span><span>:</span><span> { title</span><span>,</span><span> content }</span><span>,</span></span>
<span><span>  })</span></span>
<span><span>  </span><span>const</span><span> </span><span>json</span><span> </span><span>=</span><span> </span><span>await</span><span> </span><span>res</span><span>.json</span><span>()</span></span>
<span> </span>
<span><span>  </span><span>if</span><span> (</span><span>!</span><span>res</span><span>.ok) {</span></span>
<span><span>    </span><span>return</span><span> { message</span><span>:</span><span> </span><span>'Failed to create post'</span><span> }</span></span>
<span><span>  }</span></span>
<span><span>}</span></span>
```

You can pass your action to the `useActionState` hook and use the returned `state` to display an error message.

```
<span><span>'use client'</span></span>
<span> </span>
<span><span>import</span><span> { useActionState } </span><span>from</span><span> </span><span>'react'</span></span>
<span><span>import</span><span> { createPost } </span><span>from</span><span> </span><span>'@/app/actions'</span></span>
<span> </span>
<span><span>const</span><span> </span><span>initialState</span><span> </span><span>=</span><span> {</span></span>
<span><span>  message</span><span>:</span><span> </span><span>''</span><span>,</span></span>
<span><span>}</span></span>
<span> </span>
<span><span>export</span><span> </span><span>function</span><span> </span><span>Form</span><span>() {</span></span>
<span><span>  </span><span>const</span><span> [</span><span>state</span><span>,</span><span> </span><span>formAction</span><span>,</span><span> </span><span>pending</span><span>] </span><span>=</span><span> </span><span>useActionState</span><span>(createPost</span><span>,</span><span> initialState)</span></span>
<span> </span>
<span><span>  </span><span>return</span><span> (</span></span>
<span><span>    &lt;</span><span>form</span><span> </span><span>action</span><span>=</span><span>{formAction}&gt;</span></span>
<span><span>      &lt;</span><span>label</span><span> </span><span>htmlFor</span><span>=</span><span>"title"</span><span>&gt;Title&lt;/</span><span>label</span><span>&gt;</span></span>
<span><span>      &lt;</span><span>input</span><span> </span><span>type</span><span>=</span><span>"text"</span><span> </span><span>id</span><span>=</span><span>"title"</span><span> </span><span>name</span><span>=</span><span>"title"</span><span> </span><span>req</span><span>ui</span><span>red</span><span> /&gt;</span></span>
<span><span>      &lt;</span><span>label</span><span> </span><span>htmlFor</span><span>=</span><span>"content"</span><span>&gt;Content&lt;/</span><span>label</span><span>&gt;</span></span>
<span><span>      &lt;</span><span>textarea</span><span> </span><span>id</span><span>=</span><span>"content"</span><span> </span><span>name</span><span>=</span><span>"content"</span><span> </span><span>req</span><span>ui</span><span>red</span><span> /&gt;</span></span>
<span><span>      {</span><span>state</span><span>?.message </span><span>&amp;&amp;</span><span> &lt;</span><span>p</span><span> </span><span>aria-live</span><span>=</span><span>"polite"</span><span>&gt;{</span><span>state</span><span>.message}&lt;/</span><span>p</span><span>&gt;}</span></span>
<span><span>      &lt;</span><span>button</span><span> </span><span>disabled</span><span>=</span><span>{pending}&gt;Create Post&lt;/</span><span>button</span><span>&gt;</span></span>
<span><span>    &lt;/</span><span>form</span><span>&gt;</span></span>
<span><span>  )</span></span>
<span><span>}</span></span>
```

### [Server Components](https://nextjs.org/docs/app/getting-started/error-handling#server-components)

When fetching data inside of a Server Component, you can use the response to conditionally render an error message or [`redirect`](https://nextjs.org/docs/app/api-reference/functions/redirect).

```
<span><span>export</span><span> </span><span>default</span><span> </span><span>async</span><span> </span><span>function</span><span> </span><span>Page</span><span>() {</span></span>
<span><span>  </span><span>const</span><span> </span><span>res</span><span> </span><span>=</span><span> </span><span>await</span><span> </span><span>fetch</span><span>(</span><span>`https://...`</span><span>)</span></span>
<span><span>  </span><span>const</span><span> </span><span>data</span><span> </span><span>=</span><span> </span><span>await</span><span> </span><span>res</span><span>.json</span><span>()</span></span>
<span> </span>
<span><span>  </span><span>if</span><span> (</span><span>!</span><span>res</span><span>.ok) {</span></span>
<span><span>    </span><span>return</span><span> </span><span>'There was an error.'</span></span>
<span><span>  }</span></span>
<span> </span>
<span><span>  </span><span>return</span><span> </span><span>'...'</span></span>
<span><span>}</span></span>
```

### [Not found](https://nextjs.org/docs/app/getting-started/error-handling#not-found)

You can call the [`notFound`](https://nextjs.org/docs/app/api-reference/functions/not-found) function within a route segment and use the [`not-found.js`](https://nextjs.org/docs/app/api-reference/file-conventions/not-found) file to show a 404 UI.

```
<span><span>import</span><span> { getPostBySlug } </span><span>from</span><span> </span><span>'@/lib/posts'</span></span>
<span> </span>
<span><span>export</span><span> </span><span>default</span><span> </span><span>async</span><span> </span><span>function</span><span> </span><span>Page</span><span>({ params }</span><span>:</span><span> { params</span><span>:</span><span> { slug</span><span>:</span><span> </span><span>string</span><span> } }) {</span></span>
<span><span>  </span><span>const</span><span> { </span><span>slug</span><span> } </span><span>=</span><span> </span><span>await</span><span> params</span></span>
<span><span>  </span><span>const</span><span> </span><span>post</span><span> </span><span>=</span><span> </span><span>getPostBySlug</span><span>(slug)</span></span>
<span> </span>
<span><span>  </span><span>if</span><span> (</span><span>!</span><span>post) {</span></span>
<span><span>    </span><span>notFound</span><span>()</span></span>
<span><span>  }</span></span>
<span> </span>
<span><span>  </span><span>return</span><span> &lt;</span><span>div</span><span>&gt;{</span><span>post</span><span>.title}&lt;/</span><span>div</span><span>&gt;</span></span>
<span><span>}</span></span>
```

```
<span><span>export</span><span> </span><span>default</span><span> </span><span>function</span><span> </span><span>NotFound</span><span>() {</span></span>
<span><span>  </span><span>return</span><span> &lt;</span><span>div</span><span>&gt;404 - Page Not Found&lt;/</span><span>div</span><span>&gt;</span></span>
<span><span>}</span></span>
```

## [Handling uncaught exceptions](https://nextjs.org/docs/app/getting-started/error-handling#handling-uncaught-exceptions)

Uncaught exceptions are unexpected errors that indicate bugs or issues that should not occur during the normal flow of your application. These should be handled by throwing errors, which will then be caught by error boundaries.

### [Nested error boundaries](https://nextjs.org/docs/app/getting-started/error-handling#nested-error-boundaries)

Next.js uses error boundaries to handle uncaught exceptions. Error boundaries catch errors in their child components and display a fallback UI instead of the component tree that crashed.

Create an error boundary by adding an [`error.js`](https://nextjs.org/docs/app/api-reference/file-conventions/error) file inside a route segment and exporting a React component:

```
<span><span>'use client'</span><span> </span><span>// Error boundaries must be Client Components</span></span>
<span> </span>
<span><span>import</span><span> { useEffect } </span><span>from</span><span> </span><span>'react'</span></span>
<span> </span>
<span><span>export</span><span> </span><span>default</span><span> </span><span>function</span><span> </span><span>Error</span><span>({</span></span>
<span><span>  error</span><span>,</span></span>
<span><span>  reset</span><span>,</span></span>
<span><span>}</span><span>:</span><span> {</span></span>
<span><span>  error</span><span>:</span><span> </span><span>Error</span><span> </span><span>&amp;</span><span> { digest</span><span>?:</span><span> </span><span>string</span><span> }</span></span>
<span><span>  </span><span>reset</span><span>:</span><span> () </span><span>=&gt;</span><span> </span><span>void</span></span>
<span><span>}) {</span></span>
<span><span>  </span><span>useEffect</span><span>(() </span><span>=&gt;</span><span> {</span></span>
<span><span>    </span><span>// Log the error to an error reporting service</span></span>
<span><span>    </span><span>console</span><span>.error</span><span>(error)</span></span>
<span><span>  }</span><span>,</span><span> [error])</span></span>
<span> </span>
<span><span>  </span><span>return</span><span> (</span></span>
<span><span>    &lt;</span><span>div</span><span>&gt;</span></span>
<span><span>      &lt;</span><span>h2</span><span>&gt;Something went wrong!&lt;/</span><span>h2</span><span>&gt;</span></span>
<span><span>      &lt;</span><span>button</span></span>
<span><span>        </span><span>onClick</span><span>=</span><span>{</span></span>
<span><span>          </span><span>// Attempt to recover by trying to re-render the segment</span></span>
<span><span>          () </span><span>=&gt;</span><span> </span><span>reset</span><span>()</span></span>
<span><span>        }</span></span>
<span><span>      &gt;</span></span>
<span><span>        Try again</span></span>
<span><span>      &lt;/</span><span>button</span><span>&gt;</span></span>
<span><span>    &lt;/</span><span>div</span><span>&gt;</span></span>
<span><span>  )</span></span>
<span><span>}</span></span>
```

Errors will bubble up to the nearest parent error boundary. This allows for granular error handling by placing `error.tsx` files at different levels in the [route hierarchy](https://nextjs.org/docs/app/getting-started/project-structure#component-hierarchy).

![Nested Error Component Hierarchy](https://nextjs.org/_next/image?url=https%3A%2F%2Fh8DxKfmAPhn8O0p3.public.blob.vercel-storage.com%2Fdocs%2Fdark%2Fnested-error-component-hierarchy.png&w=3840&q=75)

### [Global errors](https://nextjs.org/docs/app/getting-started/error-handling#global-errors)

While less common, you can handle errors in the root layout using the [`global-error.js`](https://nextjs.org/docs/app/api-reference/file-conventions/error#global-error) file, located in the root app directory, even when leveraging [internationalization](https://nextjs.org/docs/app/building-your-application/routing/internationalization). Global error UI must define its own `<html>` and `<body>` tags, since it is replacing the root layout or template when active.

```
<span><span>'use client'</span><span> </span><span>// Error boundaries must be Client Components</span></span>
<span> </span>
<span><span>export</span><span> </span><span>default</span><span> </span><span>function</span><span> </span><span>GlobalError</span><span>({</span></span>
<span><span>  error</span><span>,</span></span>
<span><span>  reset</span><span>,</span></span>
<span><span>}</span><span>:</span><span> {</span></span>
<span><span>  error</span><span>:</span><span> </span><span>Error</span><span> </span><span>&amp;</span><span> { digest</span><span>?:</span><span> </span><span>string</span><span> }</span></span>
<span><span>  </span><span>reset</span><span>:</span><span> () </span><span>=&gt;</span><span> </span><span>void</span></span>
<span><span>}) {</span></span>
<span><span>  </span><span>return</span><span> (</span></span>
<span><span>    </span><span>// global-error must include html and body tags</span></span>
<span><span>    &lt;</span><span>html</span><span>&gt;</span></span>
<span><span>      &lt;</span><span>body</span><span>&gt;</span></span>
<span><span>        &lt;</span><span>h2</span><span>&gt;Something went wrong!&lt;/</span><span>h2</span><span>&gt;</span></span>
<span><span>        &lt;</span><span>button</span><span> </span><span>onClick</span><span>=</span><span>{() </span><span>=&gt;</span><span> </span><span>reset</span><span>()}&gt;Try again&lt;/</span><span>button</span><span>&gt;</span></span>
<span><span>      &lt;/</span><span>body</span><span>&gt;</span></span>
<span><span>    &lt;/</span><span>html</span><span>&gt;</span></span>
<span><span>  )</span></span>
<span><span>}</span></span>
```