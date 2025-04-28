The `mdx-components.js|tsx` file is **required** to use [`@next/mdx` with App Router](https://nextjs.org/docs/app/guides/mdx) and will not work without it. Additionally, you can use it to [customize styles](https://nextjs.org/docs/app/guides/mdx#using-custom-styles-and-components).

Use the file `mdx-components.tsx` (or `.js`) in the root of your project to define MDX Components. For example, at the same level as `pages` or `app`, or inside `src` if applicable.

```
<span><span>import</span><span> </span><span>type</span><span> { MDXComponents } </span><span>from</span><span> </span><span>'mdx/types'</span></span>
<span> </span>
<span><span>export</span><span> </span><span>function</span><span> </span><span>useMDXComponents</span><span>(components</span><span>:</span><span> </span><span>MDXComponents</span><span>)</span><span>:</span><span> </span><span>MDXComponents</span><span> {</span></span>
<span><span>  </span><span>return</span><span> {</span></span>
<span><span>    </span><span>...</span><span>components</span><span>,</span></span>
<span><span>  }</span></span>
<span><span>}</span></span>
```

## [Exports](https://nextjs.org/docs/app/api-reference/file-conventions/mdx-components#exports)

### [`useMDXComponents` function](https://nextjs.org/docs/app/api-reference/file-conventions/mdx-components#usemdxcomponents-function)

The file must export a single function, either as a default export or named `useMDXComponents`.

```
<span><span>import</span><span> </span><span>type</span><span> { MDXComponents } </span><span>from</span><span> </span><span>'mdx/types'</span></span>
<span> </span>
<span><span>export</span><span> </span><span>function</span><span> </span><span>useMDXComponents</span><span>(components</span><span>:</span><span> </span><span>MDXComponents</span><span>)</span><span>:</span><span> </span><span>MDXComponents</span><span> {</span></span>
<span><span>  </span><span>return</span><span> {</span></span>
<span><span>    </span><span>...</span><span>components</span><span>,</span></span>
<span><span>  }</span></span>
<span><span>}</span></span>
```

## [Params](https://nextjs.org/docs/app/api-reference/file-conventions/mdx-components#params)

### [`components`](https://nextjs.org/docs/app/api-reference/file-conventions/mdx-components#components)

When defining MDX Components, the export function accepts a single parameter, `components`. This parameter is an instance of `MDXComponents`.

-   The key is the name of the HTML element to override.
-   The value is the component to render instead.

> **Good to know**: Remember to pass all other components (i.e. `...components`) that do not have overrides.

## [Version History](https://nextjs.org/docs/app/api-reference/file-conventions/mdx-components#version-history)

| Version | Changes |
| --- | --- |
| `v13.1.2` | MDX Components added |