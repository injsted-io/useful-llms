Route Handlers allow you to create custom request handlers for a given route using the Web [Request](https://developer.mozilla.org/docs/Web/API/Request) and [Response](https://developer.mozilla.org/docs/Web/API/Response) APIs.

```
<span><span>export</span><span> </span><span>async</span><span> </span><span>function</span><span> </span><span>GET</span><span>() {</span></span>
<span><span>  </span><span>return</span><span> </span><span>Response</span><span>.json</span><span>({ message</span><span>:</span><span> </span><span>'Hello World'</span><span> })</span></span>
<span><span>}</span></span>
```

## [Reference](https://nextjs.org/docs/app/api-reference/file-conventions/route#reference)

### [HTTP Methods](https://nextjs.org/docs/app/api-reference/file-conventions/route#http-methods)

A **route** file allows you to create custom request handlers for a given route. The following [HTTP methods](https://developer.mozilla.org/docs/Web/HTTP/Methods) are supported: `GET`, `POST`, `PUT`, `PATCH`, `DELETE`, `HEAD`, and `OPTIONS`.

```
<span><span>export</span><span> </span><span>async</span><span> </span><span>function</span><span> </span><span>GET</span><span>(request</span><span>:</span><span> </span><span>Request</span><span>) {}</span></span>
<span> </span>
<span><span>export</span><span> </span><span>async</span><span> </span><span>function</span><span> </span><span>HEAD</span><span>(request</span><span>:</span><span> </span><span>Request</span><span>) {}</span></span>
<span> </span>
<span><span>export</span><span> </span><span>async</span><span> </span><span>function</span><span> </span><span>POST</span><span>(request</span><span>:</span><span> </span><span>Request</span><span>) {}</span></span>
<span> </span>
<span><span>export</span><span> </span><span>async</span><span> </span><span>function</span><span> </span><span>PUT</span><span>(request</span><span>:</span><span> </span><span>Request</span><span>) {}</span></span>
<span> </span>
<span><span>export</span><span> </span><span>async</span><span> </span><span>function</span><span> </span><span>DELETE</span><span>(request</span><span>:</span><span> </span><span>Request</span><span>) {}</span></span>
<span> </span>
<span><span>export</span><span> </span><span>async</span><span> </span><span>function</span><span> </span><span>PATCH</span><span>(request</span><span>:</span><span> </span><span>Request</span><span>) {}</span></span>
<span> </span>
<span><span>// If `OPTIONS` is not defined, Next.js will automatically implement `OPTIONS` and set the appropriate Response `Allow` header depending on the other methods defined in the Route Handler.</span></span>
<span><span>export</span><span> </span><span>async</span><span> </span><span>function</span><span> </span><span>OPTIONS</span><span>(request</span><span>:</span><span> </span><span>Request</span><span>) {}</span></span>
```

### [Parameters](https://nextjs.org/docs/app/api-reference/file-conventions/route#parameters)

#### [`request` (optional)](https://nextjs.org/docs/app/api-reference/file-conventions/route#request-optional)

The `request` object is a [NextRequest](https://nextjs.org/docs/app/api-reference/functions/next-request) object, which is an extension of the Web [Request](https://developer.mozilla.org/docs/Web/API/Request) API. `NextRequest` gives you further control over the incoming request, including easily accessing `cookies` and an extended, parsed, URL object `nextUrl`.

```
<span><span>import</span><span> </span><span>type</span><span> { NextRequest } </span><span>from</span><span> </span><span>'next/server'</span></span>
<span> </span>
<span><span>export</span><span> </span><span>async</span><span> </span><span>function</span><span> </span><span>GET</span><span>(request</span><span>:</span><span> </span><span>NextRequest</span><span>) {</span></span>
<span><span>  </span><span>const</span><span> </span><span>url</span><span> </span><span>=</span><span> </span><span>request</span><span>.nextUrl</span></span>
<span><span>}</span></span>
```

#### [`context` (optional)](https://nextjs.org/docs/app/api-reference/file-conventions/route#context-optional)

-   **`params`**: a promise that resolves to an object containing the [dynamic route parameters](https://nextjs.org/docs/app/building-your-application/routing/dynamic-routes) for the current route.

```
<span><span>export</span><span> </span><span>async</span><span> </span><span>function</span><span> </span><span>GET</span><span>(</span></span>
<span><span>  request</span><span>:</span><span> </span><span>Request</span><span>,</span></span>
<span><span>  { params }</span><span>:</span><span> { params</span><span>:</span><span> </span><span>Promise</span><span>&lt;{ team</span><span>:</span><span> </span><span>string</span><span> }&gt; }</span></span>
<span><span>) {</span></span>
<span><span>  </span><span>const</span><span> { </span><span>team</span><span> } </span><span>=</span><span> </span><span>await</span><span> params</span></span>
<span><span>}</span></span>
```

| Example | URL | `params` |
| --- | --- | --- |
| `app/dashboard/[team]/route.js` | `/dashboard/1` | `Promise<{ team: '1' }>` |
| `app/shop/[tag]/[item]/route.js` | `/shop/1/2` | `Promise<{ tag: '1', item: '2' }>` |
| `app/blog/[...slug]/route.js` | `/blog/1/2` | `Promise<{ slug: ['1', '2'] }>` |

## [Examples](https://nextjs.org/docs/app/api-reference/file-conventions/route#examples)

### [Handling cookies](https://nextjs.org/docs/app/api-reference/file-conventions/route#handling-cookies)

```
<span><span>import</span><span> { cookies } </span><span>from</span><span> </span><span>'next/headers'</span></span>
<span> </span>
<span><span>export</span><span> </span><span>async</span><span> </span><span>function</span><span> </span><span>GET</span><span>(request</span><span>:</span><span> </span><span>NextRequest</span><span>) {</span></span>
<span><span>  </span><span>const</span><span> </span><span>cookieStore</span><span> </span><span>=</span><span> </span><span>await</span><span> </span><span>cookies</span><span>()</span></span>
<span> </span>
<span><span>  </span><span>const</span><span> </span><span>a</span><span> </span><span>=</span><span> </span><span>cookieStore</span><span>.get</span><span>(</span><span>'a'</span><span>)</span></span>
<span><span>  </span><span>const</span><span> </span><span>b</span><span> </span><span>=</span><span> </span><span>cookieStore</span><span>.set</span><span>(</span><span>'b'</span><span>,</span><span> </span><span>'1'</span><span>)</span></span>
<span><span>  </span><span>const</span><span> </span><span>c</span><span> </span><span>=</span><span> </span><span>cookieStore</span><span>.delete</span><span>(</span><span>'c'</span><span>)</span></span>
<span><span>}</span></span>
```

## [Version History](https://nextjs.org/docs/app/api-reference/file-conventions/route#version-history)

| Version | Changes |
| --- | --- |
| `v15.0.0-RC` | `context.params` is now a promise. A [codemod](https://nextjs.org/docs/app/guides/upgrading/codemods#150) is available |
| `v15.0.0-RC` | The default caching for `GET` handlers was changed from static to dynamic |
| `v13.2.0` | Route Handlers are introduced. |