The `instrumentation.js|ts` file is used to integrate observability tools into your application, allowing you to track the performance and behavior, and to debug issues in production.

To use it, place the file in the **root** of your application or inside a [`src` folder](https://nextjs.org/docs/app/api-reference/file-conventions/src-folder) if using one.

## [Exports](https://nextjs.org/docs/app/api-reference/file-conventions/instrumentation#exports)

### [`register` (optional)](https://nextjs.org/docs/app/api-reference/file-conventions/instrumentation#register-optional)

The file exports a `register` function that is called **once** when a new Next.js server instance is initiated. `register` can be an async function.

```
<span><span>import</span><span> { registerOTel } </span><span>from</span><span> </span><span>'@vercel/otel'</span></span>
<span> </span>
<span><span>export</span><span> </span><span>function</span><span> </span><span>register</span><span>() {</span></span>
<span><span>  </span><span>registerOTel</span><span>(</span><span>'next-app'</span><span>)</span></span>
<span><span>}</span></span>
```

### [`onRequestError` (optional)](https://nextjs.org/docs/app/api-reference/file-conventions/instrumentation#onrequesterror-optional)

You can optionally export an `onRequestError` function to track **server** errors to any custom observability provider.

-   If you're running any async tasks in `onRequestError`, make sure they're awaited. `onRequestError` will be triggered when the Next.js server captures the error.
-   The `error` instance might not be the original error instance thrown, as it may be processed by React if encountered during Server Components rendering. If this happens, you can use `digest` property on an error to identify the actual error type.

```
<span><span>import</span><span> { </span><span>type</span><span> Instrumentation } </span><span>from</span><span> </span><span>'next'</span></span>
<span> </span>
<span><span>export</span><span> </span><span>const</span><span> </span><span>onRequestError</span><span>:</span><span> </span><span>Instrumentation</span><span>.</span><span>onRequestError</span><span> </span><span>=</span><span> </span><span>async</span><span> (</span></span>
<span><span>  err</span><span>,</span></span>
<span><span>  request</span><span>,</span></span>
<span><span>  context</span></span>
<span><span>) </span><span>=&gt;</span><span> {</span></span>
<span><span>  </span><span>await</span><span> </span><span>fetch</span><span>(</span><span>'https://.../report-error'</span><span>,</span><span> {</span></span>
<span><span>    method</span><span>:</span><span> </span><span>'POST'</span><span>,</span></span>
<span><span>    body</span><span>:</span><span> </span><span>JSON</span><span>.stringify</span><span>({</span></span>
<span><span>      message</span><span>:</span><span> </span><span>err</span><span>.message</span><span>,</span></span>
<span><span>      request</span><span>,</span></span>
<span><span>      context</span><span>,</span></span>
<span><span>    })</span><span>,</span></span>
<span><span>    headers</span><span>:</span><span> {</span></span>
<span><span>      </span><span>'Content-Type'</span><span>:</span><span> </span><span>'application/json'</span><span>,</span></span>
<span><span>    }</span><span>,</span></span>
<span><span>  })</span></span>
<span><span>}</span></span>
```

#### [Parameters](https://nextjs.org/docs/app/api-reference/file-conventions/instrumentation#parameters)

The function accepts three parameters: `error`, `request`, and `context`.

```
<span><span>export</span><span> </span><span>function</span><span> </span><span>onRequestError</span><span>(</span></span>
<span><span>  error</span><span>:</span><span> { digest</span><span>:</span><span> </span><span>string</span><span> } </span><span>&amp;</span><span> </span><span>Error</span><span>,</span></span>
<span><span>  request</span><span>:</span><span> {</span></span>
<span><span>    path</span><span>:</span><span> </span><span>string</span><span> </span><span>// resource path, e.g. /blog?name=foo</span></span>
<span><span>    method</span><span>:</span><span> </span><span>string</span><span> </span><span>// request method. e.g. GET, POST, etc</span></span>
<span><span>    headers</span><span>:</span><span> { [key</span><span>:</span><span> </span><span>string</span><span>]</span><span>:</span><span> </span><span>string</span><span> }</span></span>
<span><span>  }</span><span>,</span></span>
<span><span>  context</span><span>:</span><span> {</span></span>
<span><span>    routerKind</span><span>:</span><span> </span><span>'Pages Router'</span><span> </span><span>|</span><span> </span><span>'App Router'</span><span> </span><span>// the router type</span></span>
<span><span>    routePath</span><span>:</span><span> </span><span>string</span><span> </span><span>// the route file path, e.g. /app/blog/[dynamic]</span></span>
<span><span>    routeType</span><span>:</span><span> </span><span>'render'</span><span> </span><span>|</span><span> </span><span>'route'</span><span> </span><span>|</span><span> </span><span>'action'</span><span> </span><span>|</span><span> </span><span>'middleware'</span><span> </span><span>// the context in which the error occurred</span></span>
<span><span>    renderSource</span><span>:</span></span>
<span><span>      </span><span>|</span><span> </span><span>'react-server-components'</span></span>
<span><span>      </span><span>|</span><span> </span><span>'react-server-components-payload'</span></span>
<span><span>      </span><span>|</span><span> </span><span>'server-rendering'</span></span>
<span><span>    </span><span>revalidateReason</span><span>:</span><span> </span><span>'on-demand'</span><span> </span><span>|</span><span> </span><span>'stale'</span><span> </span><span>|</span><span> </span><span>undefined</span><span> </span><span>// undefined is a normal request without revalidation</span></span>
<span><span>    renderType</span><span>:</span><span> </span><span>'dynamic'</span><span> </span><span>|</span><span> </span><span>'dynamic-resume'</span><span> </span><span>// 'dynamic-resume' for PPR</span></span>
<span><span>  }</span></span>
<span><span>)</span><span>:</span><span> </span><span>void</span><span> </span><span>|</span><span> </span><span>Promise</span><span>&lt;</span><span>void</span><span>&gt;</span></span>
```

-   `error`: The caught error itself (type is always `Error`), and a `digest` property which is the unique ID of the error.
-   `request`: Read-only request information associated with the error.
-   `context`: The context in which the error occurred. This can be the type of router (App or Pages Router), and/or (Server Components (`'render'`), Route Handlers (`'route'`), Server Actions (`'action'`), or Middleware (`'middleware'`)).

### [Specifying the runtime](https://nextjs.org/docs/app/api-reference/file-conventions/instrumentation#specifying-the-runtime)

The `instrumentation.js` file works in both the Node.js and Edge runtime, however, you can use `process.env.NEXT_RUNTIME` to target a specific runtime.

```
<span><span>export</span><span> </span><span>function</span><span> </span><span>register</span><span>() {</span></span>
<span><span>  </span><span>if</span><span> (</span><span>process</span><span>.</span><span>env</span><span>.</span><span>NEXT_RUNTIME</span><span> </span><span>===</span><span> </span><span>'edge'</span><span>) {</span></span>
<span><span>    </span><span>return</span><span> </span><span>require</span><span>(</span><span>'./register.edge'</span><span>)</span></span>
<span><span>  } </span><span>else</span><span> {</span></span>
<span><span>    </span><span>return</span><span> </span><span>require</span><span>(</span><span>'./register.node'</span><span>)</span></span>
<span><span>  }</span></span>
<span><span>}</span></span>
<span> </span>
<span><span>export</span><span> </span><span>function</span><span> </span><span>onRequestError</span><span>() {</span></span>
<span><span>  </span><span>if</span><span> (</span><span>process</span><span>.</span><span>env</span><span>.</span><span>NEXT_RUNTIME</span><span> </span><span>===</span><span> </span><span>'edge'</span><span>) {</span></span>
<span><span>    </span><span>return</span><span> </span><span>require</span><span>(</span><span>'./on-request-error.edge'</span><span>)</span></span>
<span><span>  } </span><span>else</span><span> {</span></span>
<span><span>    </span><span>return</span><span> </span><span>require</span><span>(</span><span>'./on-request-error.node'</span><span>)</span></span>
<span><span>  }</span></span>
<span><span>}</span></span>
```

## [Version History](https://nextjs.org/docs/app/api-reference/file-conventions/instrumentation#version-history)

| Version | Changes |
| --- | --- |
| `v15.0.0` | `onRequestError` introduced, `instrumentation` stable |
| `v14.0.4` | Turbopack support for `instrumentation` |
| `v13.2.0` | `instrumentation` introduced as an experimental feature |