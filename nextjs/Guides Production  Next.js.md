## How to optimize your Next.js application for production

Before taking your Next.js application to production, there are some optimizations and patterns you should consider implementing for the best user experience, performance, and security.

This page provides best practices that you can use as a reference when [building your application](https://nextjs.org/docs/app/guides/production-checklist#during-development) and [before going to production](https://nextjs.org/docs/app/guides/production-checklist#before-going-to-production), as well as the [automatic Next.js optimizations](https://nextjs.org/docs/app/guides/production-checklist#automatic-optimizations) you should be aware of.

## [Automatic optimizations](https://nextjs.org/docs/app/guides/production-checklist#automatic-optimizations)

These Next.js optimizations are enabled by default and require no configuration:

-   **[Server Components](https://nextjs.org/docs/app/building-your-application/rendering/server-components):** Next.js uses Server Components by default. Server Components run on the server, and don't require JavaScript to render on the client. As such, they have no impact on the size of your client-side JavaScript bundles. You can then use [Client Components](https://nextjs.org/docs/app/building-your-application/rendering/client-components) as needed for interactivity.
-   **[Code-splitting](https://nextjs.org/docs/app/building-your-application/routing/linking-and-navigating#how-routing-and-navigation-works):** Server Components enable automatic code-splitting by route segments. You may also consider [lazy loading](https://nextjs.org/docs/app/guides/lazy-loading) Client Components and third-party libraries, where appropriate.
-   **[Prefetching](https://nextjs.org/docs/app/building-your-application/routing/linking-and-navigating#2-prefetching):** When a link to a new route enters the user's viewport, Next.js prefetches the route in background. This makes navigation to new routes almost instant. You can opt out of prefetching, where appropriate.
-   **[Static Rendering](https://nextjs.org/docs/app/building-your-application/rendering/server-components#static-rendering-default):** Next.js statically renders Server and Client Components on the server at build time and caches the rendered result to improve your application's performance. You can opt into [Dynamic Rendering](https://nextjs.org/docs/app/building-your-application/rendering/server-components#dynamic-rendering) for specific routes, where appropriate.
-   **[Caching](https://nextjs.org/docs/app/deep-dive/caching):** Next.js caches data requests, the rendered result of Server and Client Components, static assets, and more, to reduce the number of network requests to your server, database, and backend services. You may opt out of caching, where appropriate.

These defaults aim to improve your application's performance, and reduce the cost and amount of data transferred on each network request.

## [During development](https://nextjs.org/docs/app/guides/production-checklist#during-development)

While building your application, we recommend using the following features to ensure the best performance and user experience:

### [Routing and rendering](https://nextjs.org/docs/app/guides/production-checklist#routing-and-rendering)

-   **[Layouts](https://nextjs.org/docs/app/building-your-application/routing/layouts-and-templates#layouts):** Use layouts to share UI across pages and enable [partial rendering](https://nextjs.org/docs/app/building-your-application/routing/linking-and-navigating#4-partial-rendering) on navigation.
-   **[`<Link>` component](https://nextjs.org/docs/app/building-your-application/routing/linking-and-navigating#link-component):** Use the `<Link>` component for [client-side navigation and prefetching](https://nextjs.org/docs/app/building-your-application/routing/linking-and-navigating#how-routing-and-navigation-works).
-   **[Error Handling](https://nextjs.org/docs/app/building-your-application/routing/error-handling):** Gracefully handle [catch-all errors](https://nextjs.org/docs/app/building-your-application/routing/error-handling) and [404 errors](https://nextjs.org/docs/app/api-reference/file-conventions/not-found) in production by creating custom error pages.
-   **[Composition Patterns](https://nextjs.org/docs/app/building-your-application/rendering/composition-patterns):** Follow the recommended composition patterns for Server and Client Components, and check the placement of your [`"use client"` boundaries](https://nextjs.org/docs/app/building-your-application/rendering/composition-patterns#moving-client-components-down-the-tree) to avoid unnecessarily increasing your client-side JavaScript bundle.
-   **[Dynamic APIs](https://nextjs.org/docs/app/building-your-application/rendering/server-components#dynamic-apis):** Be aware that Dynamic APIs like [`cookies`](https://nextjs.org/docs/app/api-reference/functions/cookies) and the [`searchParams`](https://nextjs.org/docs/app/api-reference/file-conventions/page#searchparams-optional) prop will opt the entire route into [Dynamic Rendering](https://nextjs.org/docs/app/building-your-application/rendering/server-components#dynamic-rendering) (or your whole application if used in the [Root Layout](https://nextjs.org/docs/app/building-your-application/routing/layouts-and-templates#root-layout-required)). Ensure Dynamic API usage is intentional and wrap them in `<Suspense>` boundaries where appropriate.

> **Good to know**: [Partial Prerendering (experimental)](https://nextjs.org/blog/next-14#partial-prerendering-preview) will allow parts of a route to be dynamic without opting the whole route into dynamic rendering.

### [Data fetching and caching](https://nextjs.org/docs/app/guides/production-checklist#data-fetching-and-caching)

-   **[Server Components](https://nextjs.org/docs/app/building-your-application/data-fetching/fetching):** Leverage the benefits of fetching data on the server using Server Components.
-   **[Route Handlers](https://nextjs.org/docs/app/building-your-application/routing/route-handlers):** Use Route Handlers to access your backend resources from Client Components. But do not call Route Handlers from Server Components to avoid an additional server request.
-   **[Streaming](https://nextjs.org/docs/app/building-your-application/routing/loading-ui-and-streaming):** Use Loading UI and React Suspense to progressively send UI from the server to the client, and prevent the whole route from blocking while data is being fetched.
-   **[Parallel Data Fetching](https://nextjs.org/docs/app/building-your-application/data-fetching/fetching#parallel-and-sequential-data-fetching):** Reduce network waterfalls by fetching data in parallel, where appropriate. Also, consider [preloading data](https://nextjs.org/docs/app/building-your-application/data-fetching/fetching#preloading-data) where appropriate.
-   **[Data Caching](https://nextjs.org/docs/app/deep-dive/caching#data-cache):** Verify whether your data requests are being cached or not, and opt into caching, where appropriate. Ensure requests that don't use `fetch` are [cached](https://nextjs.org/docs/app/api-reference/functions/unstable_cache).
-   **[Static Images](https://nextjs.org/docs/app/api-reference/file-conventions/public-folder):** Use the `public` directory to automatically cache your application's static assets, e.g. images.

### [UI and accessibility](https://nextjs.org/docs/app/guides/production-checklist#ui-and-accessibility)

-   **[Forms and Validation](https://nextjs.org/docs/app/building-your-application/data-fetching/server-actions-and-mutations#forms):** Use Server Actions to handle form submissions, server-side validation, and handle errors.

-   **[Font Module](https://nextjs.org/docs/app/building-your-application/optimizing/fonts):** Optimize fonts by using the Font Module, which automatically hosts your font files with other static assets, removes external network requests, and reduces [layout shift](https://web.dev/articles/cls).
-   **[`<Image>` Component](https://nextjs.org/docs/app/building-your-application/optimizing/images):** Optimize images by using the Image Component, which automatically optimizes images, prevents layout shift, and serves them in modern formats like WebP.
-   **[`<Script>` Component](https://nextjs.org/docs/app/guides/scripts):** Optimize third-party scripts by using the Script Component, which automatically defers scripts and prevents them from blocking the main thread.
-   **[ESLint](https://nextjs.org/docs/architecture/accessibility#linting):** Use the built-in `eslint-plugin-jsx-a11y` plugin to catch accessibility issues early.

### [Security](https://nextjs.org/docs/app/guides/production-checklist#security)

-   **[Tainting](https://nextjs.org/docs/app/building-your-application/data-fetching/fetching#preventing-sensitive-data-from-being-exposed-to-the-client):** Prevent sensitive data from being exposed to the client by tainting data objects and/or specific values.
-   **[Server Actions](https://nextjs.org/docs/app/building-your-application/data-fetching/server-actions-and-mutations#authentication-and-authorization):** Ensure users are authorized to call Server Actions. Review the recommended [security practices](https://nextjs.org/blog/security-nextjs-server-components-actions).

-   **[Environment Variables](https://nextjs.org/docs/app/guides/environment-variables):** Ensure your `.env.*` files are added to `.gitignore` and only public variables are prefixed with `NEXT_PUBLIC_`.
-   **[Content Security Policy](https://nextjs.org/docs/app/guides/content-security-policy):** Consider adding a Content Security Policy to protect your application against various security threats such as cross-site scripting, clickjacking, and other code injection attacks.

### [Metadata and SEO](https://nextjs.org/docs/app/guides/production-checklist#metadata-and-seo)

-   **[Metadata API](https://nextjs.org/docs/app/building-your-application/optimizing/metadata):** Use the Metadata API to improve your application's Search Engine Optimization (SEO) by adding page titles, descriptions, and more.
-   **[Open Graph (OG) images](https://nextjs.org/docs/app/api-reference/file-conventions/metadata/opengraph-image):** Create OG images to prepare your application for social sharing.
-   **[Sitemaps](https://nextjs.org/docs/app/api-reference/functions/generate-sitemaps) and [Robots](https://nextjs.org/docs/app/api-reference/file-conventions/metadata/robots):** Help Search Engines crawl and index your pages by generating sitemaps and robots files.

### [Type safety](https://nextjs.org/docs/app/guides/production-checklist#type-safety)

-   **TypeScript and [TS Plugin](https://nextjs.org/docs/app/api-reference/config/typescript):** Use TypeScript and the TypeScript plugin for better type-safety, and to help you catch errors early.

## [Before going to production](https://nextjs.org/docs/app/guides/production-checklist#before-going-to-production)

Before going to production, you can run `next build` to build your application locally and catch any build errors, then run `next start` to measure the performance of your application in a production-like environment.

### [Core Web Vitals](https://nextjs.org/docs/app/guides/production-checklist#core-web-vitals)

-   **[Lighthouse](https://developers.google.com/web/tools/lighthouse):** Run lighthouse in incognito to gain a better understanding of how your users will experience your site, and to identify areas for improvement. This is a simulated test and should be paired with looking at field data (such as Core Web Vitals).

-   **[`useReportWebVitals` hook](https://nextjs.org/docs/app/api-reference/functions/use-report-web-vitals):** Use this hook to send [Core Web Vitals](https://web.dev/articles/vitals) data to analytics tools.

### [Analyzing bundles](https://nextjs.org/docs/app/guides/production-checklist#analyzing-bundles)

Use the [`@next/bundle-analyzer` plugin](https://nextjs.org/docs/app/guides/package-bundling#analyzing-javascript-bundles) to analyze the size of your JavaScript bundles and identify large modules and dependencies that might be impacting your application's performance.

Additionally, the following tools can help you understand the impact of adding new dependencies to your application:

-   [Import Cost](https://marketplace.visualstudio.com/items?itemName=wix.vscode-import-cost)
-   [Package Phobia](https://packagephobia.com/)
-   [Bundle Phobia](https://bundlephobia.com/)
-   [bundlejs](https://bundlejs.com/)