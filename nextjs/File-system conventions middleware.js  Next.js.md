The `middleware.js|ts` file is used to write [Middleware](https://nextjs.org/docs/app/building-your-application/routing/middleware) and run code on the server before a request is completed. Then, based on the incoming request, you can modify the response by rewriting, redirecting, modifying the request or response headers, or responding directly.

Middleware executes before routes are rendered. It's particularly useful for implementing custom server-side logic like authentication, logging, or handling redirects.

Use the file `middleware.ts` (or .js) in the root of your project to define Middleware. For example, at the same level as `app` or `pages`, or inside `src` if applicable.

```
<span><span>import</span><span> { NextResponse</span><span>,</span><span> NextRequest } </span><span>from</span><span> </span><span>'next/server'</span></span>
<span> </span>
<span><span>// This function can be marked `async` if using `await` inside</span></span>
<span><span>export</span><span> </span><span>function</span><span> </span><span>middleware</span><span>(request</span><span>:</span><span> </span><span>NextRequest</span><span>) {</span></span>
<span><span>  </span><span>return</span><span> </span><span>NextResponse</span><span>.redirect</span><span>(</span><span>new</span><span> </span><span>URL</span><span>(</span><span>'/home'</span><span>,</span><span> </span><span>request</span><span>.url))</span></span>
<span><span>}</span></span>
<span> </span>
<span><span>export</span><span> </span><span>const</span><span> </span><span>config</span><span> </span><span>=</span><span> {</span></span>
<span><span>  matcher</span><span>:</span><span> </span><span>'/about/:path*'</span><span>,</span></span>
<span><span>}</span></span>
```

## [Exports](https://nextjs.org/docs/app/api-reference/file-conventions/middleware#exports)

### [Middleware function](https://nextjs.org/docs/app/api-reference/file-conventions/middleware#middleware-function)

The file must export a single function, either as a default export or named `middleware`. Note that multiple middleware from the same file are not supported.

```
<span><span>// Example of default export</span></span>
<span><span>export</span><span> </span><span>default</span><span> </span><span>function</span><span> </span><span>middleware</span><span>(request) {</span></span>
<span><span>  </span><span>// Middleware logic</span></span>
<span><span>}</span></span>
```

### [Config object (optional)](https://nextjs.org/docs/app/api-reference/file-conventions/middleware#config-object-optional)

Optionally, a config object can be exported alongside the Middleware function. This object includes the [matcher](https://nextjs.org/docs/app/api-reference/file-conventions/middleware#matcher) to specify paths where the Middleware applies.

#### [Matcher](https://nextjs.org/docs/app/api-reference/file-conventions/middleware#matcher)

The `matcher` option allows you to target specific paths for the Middleware to run on. You can specify these paths in several ways:

-   For a single path: Directly use a string to define the path, like `'/about'`.
-   For multiple paths: Use an array to list multiple paths, such as `matcher: ['/about', '/contact']`, which applies the Middleware to both `/about` and `/contact`.

Additionally, `matcher` supports complex path specifications through regular expressions, such as `matcher: ['/((?!api|_next/static|_next/image|.*\\.png$).*)']`, enabling precise control over which paths to include or exclude.

The `matcher` option also accepts an array of objects with the following keys:

-   `source`: The path or pattern used to match the request paths. It can be a string for direct path matching or a pattern for more complex matching.
-   `regexp` (optional): A regular expression string that fine-tunes the matching based on the source. It provides additional control over which paths are included or excluded.
-   `locale` (optional): A boolean that, when set to `false`, ignores locale-based routing in path matching.
-   `has` (optional): Specifies conditions based on the presence of specific request elements such as headers, query parameters, or cookies.
-   `missing` (optional): Focuses on conditions where certain request elements are absent, like missing headers or cookies.

```
<span><span>export</span><span> </span><span>const</span><span> </span><span>config</span><span> </span><span>=</span><span> {</span></span>
<span><span>  matcher</span><span>:</span><span> [</span></span>
<span><span>    {</span></span>
<span><span>      source</span><span>:</span><span> </span><span>'/api/*'</span><span>,</span></span>
<span><span>      regexp</span><span>:</span><span> </span><span>'^/api/(.*)'</span><span>,</span></span>
<span><span>      locale</span><span>:</span><span> </span><span>false</span><span>,</span></span>
<span><span>      has</span><span>:</span><span> [</span></span>
<span><span>        { type</span><span>:</span><span> </span><span>'header'</span><span>,</span><span> key</span><span>:</span><span> </span><span>'Authorization'</span><span>,</span><span> value</span><span>:</span><span> </span><span>'Bearer Token'</span><span> }</span><span>,</span></span>
<span><span>        { type</span><span>:</span><span> </span><span>'query'</span><span>,</span><span> key</span><span>:</span><span> </span><span>'userId'</span><span>,</span><span> value</span><span>:</span><span> </span><span>'123'</span><span> }</span><span>,</span></span>
<span><span>      ]</span><span>,</span></span>
<span><span>      missing</span><span>:</span><span> [{ type</span><span>:</span><span> </span><span>'cookie'</span><span>,</span><span> key</span><span>:</span><span> </span><span>'session'</span><span>,</span><span> value</span><span>:</span><span> </span><span>'active'</span><span> }]</span><span>,</span></span>
<span><span>    }</span><span>,</span></span>
<span><span>  ]</span><span>,</span></span>
<span><span>}</span></span>
```

## [Params](https://nextjs.org/docs/app/api-reference/file-conventions/middleware#params)

### [`request`](https://nextjs.org/docs/app/api-reference/file-conventions/middleware#request)

When defining Middleware, the default export function accepts a single parameter, `request`. This parameter is an instance of `NextRequest`, which represents the incoming HTTP request.

```
<span><span>import</span><span> </span><span>type</span><span> { NextRequest } </span><span>from</span><span> </span><span>'next/server'</span></span>
<span> </span>
<span><span>export</span><span> </span><span>function</span><span> </span><span>middleware</span><span>(request</span><span>:</span><span> </span><span>NextRequest</span><span>) {</span></span>
<span><span>  </span><span>// Middleware logic goes here</span></span>
<span><span>}</span></span>
```

> **Good to know**:
> 
> -   `NextRequest` is a type that represents incoming HTTP requests in Next.js Middleware, whereas [`NextResponse`](https://nextjs.org/docs/app/api-reference/file-conventions/middleware#nextresponse) is a class used to manipulate and send back HTTP responses.

## [NextResponse](https://nextjs.org/docs/app/api-reference/file-conventions/middleware#nextresponse)

Middleware can use the [`NextResponse`](https://nextjs.org/docs/app/building-your-application/routing/middleware#nextresponse) object which extends the [Web Response API](https://developer.mozilla.org/en-US/docs/Web/API/Response). By returning a `NextResponse` object, you can directly manipulate cookies, set headers, implement redirects, and rewrite paths.

> **Good to know**: For redirects, you can also use `Response.redirect` instead of `NextResponse.redirect`.

## [Runtime](https://nextjs.org/docs/app/api-reference/file-conventions/middleware#runtime)

Middleware only supports the [Edge runtime](https://nextjs.org/docs/app/building-your-application/rendering/edge-and-nodejs-runtimes). The Node.js runtime cannot be used.

## [Version History](https://nextjs.org/docs/app/api-reference/file-conventions/middleware#version-history)

| Version | Changes |
| --- | --- |
| `v13.1.0` | Advanced Middleware flags added |
| `v13.0.0` | Middleware can modify request headers, response headers, and send responses |
| `v12.2.0` | Middleware is stable, please see the [upgrade guide](https://nextjs.org/docs/messages/middleware-upgrade-guide) |
| `v12.0.9` | Enforce absolute URLs in Edge Runtime ([PR](https://github.com/vercel/next.js/pull/33410)) |
| `v12.0.0` | Middleware (Beta) added |