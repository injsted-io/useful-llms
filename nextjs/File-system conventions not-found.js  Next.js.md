The **not-found** file is used to render UI when the [`notFound`](https://nextjs.org/docs/app/api-reference/functions/not-found) function is thrown within a route segment. Along with serving a custom UI, Next.js will return a `200` HTTP status code for streamed responses, and `404` for non-streamed responses.

`not-found.js` components do not accept any props.

**Good to know**: In addition to catching expected `notFound()` errors, the root `app/not-found.js` file also handles any unmatched URLs for your whole application. This means users that visit a URL that is not handled by your app will be shown the UI exported by the `app/not-found.js` file.

By default, `not-found` is a Server Component. You can mark it as `async` to fetch and display data:

```
<span><span>import</span><span> Link </span><span>from</span><span> </span><span>'next/link'</span></span>
<span><span>import</span><span> { headers } </span><span>from</span><span> </span><span>'next/headers'</span></span>
<span> </span>
<span><span>export</span><span> </span><span>default</span><span> </span><span>async</span><span> </span><span>function</span><span> </span><span>NotFound</span><span>() {</span></span>
<span><span>  </span><span>const</span><span> </span><span>headersList</span><span> </span><span>=</span><span> </span><span>await</span><span> </span><span>headers</span><span>()</span></span>
<span><span>  </span><span>const</span><span> </span><span>domain</span><span> </span><span>=</span><span> </span><span>headersList</span><span>.get</span><span>(</span><span>'host'</span><span>)</span></span>
<span><span>  </span><span>const</span><span> </span><span>data</span><span> </span><span>=</span><span> </span><span>await</span><span> </span><span>getSiteData</span><span>(domain)</span></span>
<span><span>  </span><span>return</span><span> (</span></span>
<span><span>    &lt;</span><span>div</span><span>&gt;</span></span>
<span><span>      &lt;</span><span>h2</span><span>&gt;Not Found: {</span><span>data</span><span>.name}&lt;/</span><span>h2</span><span>&gt;</span></span>
<span><span>      &lt;</span><span>p</span><span>&gt;Could not find requested resource&lt;/</span><span>p</span><span>&gt;</span></span>
<span><span>      &lt;</span><span>p</span><span>&gt;</span></span>
<span><span>        View &lt;</span><span>Link</span><span> </span><span>href</span><span>=</span><span>"/blog"</span><span>&gt;all posts&lt;/</span><span>Link</span><span>&gt;</span></span>
<span><span>      &lt;/</span><span>p</span><span>&gt;</span></span>
<span><span>    &lt;/</span><span>div</span><span>&gt;</span></span>
<span><span>  )</span></span>
<span><span>}</span></span>
```

If you need to use Client Component hooks like `usePathname` to display content based on the path, you must fetch data on the client-side instead.