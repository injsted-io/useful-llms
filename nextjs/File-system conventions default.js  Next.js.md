The `default.js` file is used to render a fallback within [Parallel Routes](https://nextjs.org/docs/app/building-your-application/routing/parallel-routes) when Next.js cannot recover a [slot's](https://nextjs.org/docs/app/building-your-application/routing/parallel-routes#slots) active state after a full-page load.

During [soft navigation](https://nextjs.org/docs/app/building-your-application/routing/linking-and-navigating#5-soft-navigation), Next.js keeps track of the active _state_ (subpage) for each slot. However, for hard navigations (full-page load), Next.js cannot recover the active state. In this case, a `default.js` file can be rendered for subpages that don't match the current URL.

Consider the following folder structure. The `@team` slot has a `settings` page, but `@analytics` does not.

![Parallel Routes unmatched routes](https://nextjs.org/_next/image?url=https%3A%2F%2Fh8DxKfmAPhn8O0p3.public.blob.vercel-storage.com%2Fdocs%2Fdark%2Fparallel-routes-unmatched-routes.png&w=3840&q=75)

When navigating to `/settings`, the `@team` slot will render the `settings` page while maintaining the currently active page for the `@analytics` slot.

On refresh, Next.js will render a `default.js` for `@analytics`. If `default.js` doesn't exist, a `404` is rendered instead.

Additionally, since `children` is an implicit slot, you also need to create a `default.js` file to render a fallback for `children` when Next.js cannot recover the active state of the parent page.

## [Reference](https://nextjs.org/docs/app/api-reference/file-conventions/default#reference)

### [`params` (optional)](https://nextjs.org/docs/app/api-reference/file-conventions/default#params-optional)

A promise that resolves to an object containing the [dynamic route parameters](https://nextjs.org/docs/app/building-your-application/routing/dynamic-routes) from the root segment down to the slot's subpages. For example:

```
<span><span>export</span><span> </span><span>default</span><span> </span><span>async</span><span> </span><span>function</span><span> </span><span>Default</span><span>({</span></span>
<span><span>  params</span><span>,</span></span>
<span><span>}</span><span>:</span><span> {</span></span>
<span><span>  params</span><span>:</span><span> </span><span>Promise</span><span>&lt;{ artist</span><span>:</span><span> </span><span>string</span><span> }&gt;</span></span>
<span><span>}) {</span></span>
<span><span>  </span><span>const</span><span> { </span><span>artist</span><span> } </span><span>=</span><span> </span><span>await</span><span> params</span></span>
<span><span>}</span></span>
```

| Example | URL | `params` |
| --- | --- | --- |
| `app/[artist]/@sidebar/default.js` | `/zack` | `Promise<{ artist: 'zack' }>` |
| `app/[artist]/[album]/@sidebar/default.js` | `/zack/next` | `Promise<{ artist: 'zack', album: 'next' }>` |

-   Since the `params` prop is a promise. You must use `async/await` or React's [`use`](https://react.dev/reference/react/use) function to access the values.
    -   In version 14 and earlier, `params` was a synchronous prop. To help with backwards compatibility, you can still access it synchronously in Next.js 15, but this behavior will be deprecated in the future.