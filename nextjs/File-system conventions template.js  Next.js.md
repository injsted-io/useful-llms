A **template** file is similar to a [layout](https://nextjs.org/docs/app/building-your-application/routing/layouts-and-templates#layouts) in that it wraps a layout or page. Unlike layouts that persist across routes and maintain state, templates are given a unique key, meaning children Client Components reset their state on navigation.

```
<span><span>export</span><span> </span><span>default</span><span> </span><span>function</span><span> </span><span>Template</span><span>({ children }</span><span>:</span><span> { children</span><span>:</span><span> </span><span>React</span><span>.</span><span>ReactNode</span><span> }) {</span></span>
<span><span>  </span><span>return</span><span> &lt;</span><span>div</span><span>&gt;{children}&lt;/</span><span>div</span><span>&gt;</span></span>
<span><span>}</span></span>
```

![template.js special file](https://nextjs.org/_next/image?url=https%3A%2F%2Fh8DxKfmAPhn8O0p3.public.blob.vercel-storage.com%2Fdocs%2Fdark%2Ftemplate-special-file.png&w=3840&q=75)

While less common, you might choose to use a template over a layout if you want:

-   Features that rely on `useEffect` (e.g logging page views) and `useState` (e.g a per-page feedback form).
-   To change the default framework behavior. For example, Suspense Boundaries inside layouts only show the fallback the first time the Layout is loaded and not when switching pages. For templates, the fallback is shown on each navigation.

## [Props](https://nextjs.org/docs/app/api-reference/file-conventions/template#props)

### [`children` (required)](https://nextjs.org/docs/app/api-reference/file-conventions/template#children-required)

Template accepts a `children` prop. For example:

```
<span><span>&lt;</span><span>Layout</span><span>&gt;</span></span>
<span><span>  {</span><span>/* Note that the template is automatically given a unique key. */</span><span>}</span></span>
<span><span>  &lt;</span><span>Template</span><span> </span><span>key</span><span>=</span><span>{routeParam}&gt;{children}&lt;/</span><span>Template</span><span>&gt;</span></span>
<span><span>&lt;/</span><span>Layout</span><span>&gt;</span></span>
```

> **Good to know**:
> 
> -   By default, `template` is a [Server Component](https://nextjs.org/docs/app/building-your-application/rendering/server-components), but can also be used as a [Client Component](https://nextjs.org/docs/app/building-your-application/rendering/client-components) through the `"use client"` directive.
> -   When a user navigates between routes that share a `template`, a new instance of the component is mounted, DOM elements are recreated, state is **not** preserved in Client Components, and effects are re-synchronized.

## [Version History](https://nextjs.org/docs/app/api-reference/file-conventions/template#version-history)

| Version | Changes |
| --- | --- |
| `v13.0.0` | `template` introduced. |