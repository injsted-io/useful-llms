This feature is currently experimental and subject to change, it's not recommended for production. Try it out and share your feedback on [GitHub](https://github.com/vercel/next.js/issues).

The **forbidden** file is used to render UI when the [`forbidden`](https://nextjs.org/docs/app/api-reference/functions/forbidden) function is invoked during authentication. Along with allowing you to customize the UI, Next.js will return a `403` status code.

```
<span><span>import</span><span> Link </span><span>from</span><span> </span><span>'next/link'</span></span>
<span> </span>
<span><span>export</span><span> </span><span>default</span><span> </span><span>function</span><span> </span><span>Forbidden</span><span>() {</span></span>
<span><span>  </span><span>return</span><span> (</span></span>
<span><span>    &lt;</span><span>div</span><span>&gt;</span></span>
<span><span>      &lt;</span><span>h2</span><span>&gt;Forbidden&lt;/</span><span>h2</span><span>&gt;</span></span>
<span><span>      &lt;</span><span>p</span><span>&gt;You are not authorized to access this resource.&lt;/</span><span>p</span><span>&gt;</span></span>
<span><span>      &lt;</span><span>Link</span><span> </span><span>href</span><span>=</span><span>"/"</span><span>&gt;Return Home&lt;/</span><span>Link</span><span>&gt;</span></span>
<span><span>    &lt;/</span><span>div</span><span>&gt;</span></span>
<span><span>  )</span></span>
<span><span>}</span></span>
```

## [Reference](https://nextjs.org/docs/app/api-reference/file-conventions/forbidden#reference)

### [Props](https://nextjs.org/docs/app/api-reference/file-conventions/forbidden#props)

`forbidden.js` components do not accept any props.

## [Version History](https://nextjs.org/docs/app/api-reference/file-conventions/forbidden#version-history)

| Version | Changes |
| --- | --- |
| `v15.1.0` | `forbidden.js` introduced. |