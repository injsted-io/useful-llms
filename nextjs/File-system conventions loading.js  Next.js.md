A **loading** file can create instant loading states built on [Suspense](https://nextjs.org/docs/app/building-your-application/routing/loading-ui-and-streaming).

By default, this file is a [Server Component](https://nextjs.org/docs/app/building-your-application/rendering/server-components) - but can also be used as a Client Component through the `"use client"` directive.

```
<span><span>export</span><span> </span><span>default</span><span> </span><span>function</span><span> </span><span>Loading</span><span>() {</span></span>
<span><span>  </span><span>// Or a custom loading skeleton component</span></span>
<span><span>  </span><span>return</span><span> &lt;</span><span>p</span><span>&gt;Loading...&lt;/</span><span>p</span><span>&gt;</span></span>
<span><span>}</span></span>
```

Loading UI components do not accept any parameters.

> **Good to know**:
> 
> -   While designing loading UI, you may find it helpful to use the [React Developer Tools](https://react.dev/learn/react-developer-tools) to manually toggle Suspense boundaries.

## [Version History](https://nextjs.org/docs/app/api-reference/file-conventions/loading#version-history)

| Version | Changes |
| --- | --- |
| `v13.0.0` | `loading` introduced. |