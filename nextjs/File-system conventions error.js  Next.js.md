An **error** file allows you to handle unexpected runtime errors and display fallback UI.

![error.js special file](https://nextjs.org/_next/image?url=https%3A%2F%2Fh8DxKfmAPhn8O0p3.public.blob.vercel-storage.com%2Fdocs%2Fdark%2Ferror-special-file.png&w=3840&q=75)

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

`error.js` wraps a route segment and its nested children in a [React Error Boundary](https://react.dev/reference/react/Component#catching-rendering-errors-with-an-error-boundary). When an error throws within the boundary, the `error` component shows as the fallback UI.

![How error.js works](https://nextjs.org/_next/image?url=https%3A%2F%2Fh8DxKfmAPhn8O0p3.public.blob.vercel-storage.com%2Fdocs%2Fdark%2Ferror-overview.png&w=3840&q=75)

> **Good to know**:
> 
> -   The [React DevTools](https://react.dev/learn/react-developer-tools) allow you to toggle error boundaries to test error states.
> -   If you want errors to bubble up to the parent error boundary, you can `throw` when rendering the `error` component.

## [Reference](https://nextjs.org/docs/app/api-reference/file-conventions/error#reference)

### [Props](https://nextjs.org/docs/app/api-reference/file-conventions/error#props)

#### [`error`](https://nextjs.org/docs/app/api-reference/file-conventions/error#error)

An instance of an [`Error`](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Error) object forwarded to the `error.js` Client Component.

> **Good to know:** During development, the `Error` object forwarded to the client will be serialized and include the `message` of the original error for easier debugging. However, **this behavior is different in production** to avoid leaking potentially sensitive details included in the error to the client.

#### [`error.message`](https://nextjs.org/docs/app/api-reference/file-conventions/error#errormessage)

-   Errors forwarded from Client Components show the original `Error` message.
-   Errors forwarded from Server Components show a generic message with an identifier. This is to prevent leaking sensitive details. You can use the identifier, under `errors.digest`, to match the corresponding server-side logs.

#### [`error.digest`](https://nextjs.org/docs/app/api-reference/file-conventions/error#errordigest)

An automatically generated hash of the error thrown. It can be used to match the corresponding error in server-side logs.

#### [`reset`](https://nextjs.org/docs/app/api-reference/file-conventions/error#reset)

The cause of an error can sometimes be temporary. In these cases, trying again might resolve the issue.

An error component can use the `reset()` function to prompt the user to attempt to recover from the error. When executed, the function will try to re-render the error boundary's contents. If successful, the fallback error component is replaced with the result of the re-render.

```
<span><span>'use client'</span><span> </span><span>// Error boundaries must be Client Components</span></span>
<span> </span>
<span><span>export</span><span> </span><span>default</span><span> </span><span>function</span><span> </span><span>Error</span><span>({</span></span>
<span><span>  error</span><span>,</span></span>
<span><span>  reset</span><span>,</span></span>
<span><span>}</span><span>:</span><span> {</span></span>
<span><span>  error</span><span>:</span><span> </span><span>Error</span><span> </span><span>&amp;</span><span> { digest</span><span>?:</span><span> </span><span>string</span><span> }</span></span>
<span><span>  </span><span>reset</span><span>:</span><span> () </span><span>=&gt;</span><span> </span><span>void</span></span>
<span><span>}) {</span></span>
<span><span>  </span><span>return</span><span> (</span></span>
<span><span>    &lt;</span><span>div</span><span>&gt;</span></span>
<span><span>      &lt;</span><span>h2</span><span>&gt;Something went wrong!&lt;/</span><span>h2</span><span>&gt;</span></span>
<span><span>      &lt;</span><span>button</span><span> </span><span>onClick</span><span>=</span><span>{() </span><span>=&gt;</span><span> </span><span>reset</span><span>()}&gt;Try again&lt;/</span><span>button</span><span>&gt;</span></span>
<span><span>    &lt;/</span><span>div</span><span>&gt;</span></span>
<span><span>  )</span></span>
<span><span>}</span></span>
```

## [Examples](https://nextjs.org/docs/app/api-reference/file-conventions/error#examples)

### [Global Error](https://nextjs.org/docs/app/api-reference/file-conventions/error#global-error)

While less common, you can handle errors in the root layout or template using `global-error.js`, located in the root app directory, even when leveraging [internationalization](https://nextjs.org/docs/app/building-your-application/routing/internationalization). Global error UI must define its own `<html>` and `<body>` tags. This file replaces the root layout or template when active.

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

## [Version History](https://nextjs.org/docs/app/api-reference/file-conventions/error#version-history)

| Version | Changes |
| --- | --- |
| `v15.2.0` | Also display `global-error` in development. |
| `v13.1.0` | `global-error` introduced. |
| `v13.0.0` | `error` introduced. |