## How to optimize memory usage

As applications grow and become more feature rich, they can demand more resources when developing locally or creating production builds.

Let's explore some strategies and techniques to optimize memory and address common memory issues in Next.js.

## [Reduce number of dependencies](https://nextjs.org/docs/app/guides/memory-usage#reduce-number-of-dependencies)

Applications with a large amount of dependencies will use more memory.

The [Bundle Analyzer](https://nextjs.org/docs/app/guides/package-bundling) can help you investigate large dependencies in your application that may be able to be removed to improve performance and memory usage.

## [Try `experimental.webpackMemoryOptimizations`](https://nextjs.org/docs/app/guides/memory-usage#try-experimentalwebpackmemoryoptimizations)

Starting in `v15.0.0`, you can add `experimental.webpackMemoryOptimizations: true` to your `next.config.js` file to change behavior in Webpack that reduces max memory usage but may increase compilation times by a slight amount.

> **Good to know**: This feature is currently experimental to test on more projects first, but it is considered to be low-risk.

## [Run `next build` with `--experimental-debug-memory-usage`](https://nextjs.org/docs/app/guides/memory-usage#run-next-build-with---experimental-debug-memory-usage)

Starting in `14.2.0`, you can run `next build --experimental-debug-memory-usage` to run the build in a mode where Next.js will print out information about memory usage continuously throughout the build, such as heap usage and garbage collection statistics. Heap snapshots will also be taken automatically when memory usage gets close to the configured limit.

> **Good to know**: This feature is not compatible with the Webpack build worker option which is auto-enabled unless you have custom webpack config.

## [Record a heap profile](https://nextjs.org/docs/app/guides/memory-usage#record-a-heap-profile)

To look for memory issues, you can record a heap profile from Node.js and load it in Chrome DevTools to identify potential sources of memory leaks.

In your terminal, pass the `--heap-prof` flag to Node.js when starting your Next.js build:

```
<span><span>node</span><span> </span><span>--heap-prof</span><span> </span><span>node_modules/next/dist/bin/next</span><span> </span><span>build</span></span>
```

At the end of the build, a `.heapprofile` file will be created by Node.js.

In Chrome DevTools, you can open the Memory tab and click on the "Load Profile" button to visualize the file.

## [Analyze a snapshot of the heap](https://nextjs.org/docs/app/guides/memory-usage#analyze-a-snapshot-of-the-heap)

You can use an inspector tool to analyze the memory usage of the application.

When running the `next build` or `next dev` command, add `NODE_OPTIONS=--inspect` to the beginning of the command. This will expose the inspector agent on the default port. If you wish to break before any user code starts, you can pass `--inspect-brk` instead. While the process is running, you can use a tool such as Chrome DevTools to connect to the debugging port to record and analyze a snapshot of the heap to see what memory is being retained.

Starting in `14.2.0`, you can also run `next build` with the `--experimental-debug-memory-usage` flag to make it easier to take heap snapshots.

While running in this mode, you can send a `SIGUSR2` signal to the process at any point, and the process will take a heap snapshot.

The heap snapshot will be saved to the project root of the Next.js application and can be loaded in any heap analyzer, such as Chrome DevTools, to see what memory is retained. This mode is not yet compatible with Webpack build workers.

See [how to record and analyze heap snapshots](https://developer.chrome.com/docs/devtools/memory-problems/heap-snapshots) for more information.

## [Webpack build worker](https://nextjs.org/docs/app/guides/memory-usage#webpack-build-worker)

The Webpack build worker allows you to run Webpack compilations inside a separate Node.js worker which will decrease memory usage of your application during builds.

This option is enabled by default if your application does not have a custom Webpack configuration starting in `v14.1.0`.

If you are using an older version of Next.js or you have a custom Webpack configuration, you can enable this option by setting `experimental.webpackBuildWorker: true` inside your `next.config.js`.

> **Good to know**: This feature may not be compatible with all custom Webpack plugins.

## [Disable Webpack cache](https://nextjs.org/docs/app/guides/memory-usage#disable-webpack-cache)

The [Webpack cache](https://webpack.js.org/configuration/cache/) saves generated Webpack modules in memory and/or to disk to improve the speed of builds. This can help with performance, but it will also increase the memory usage of your application to store the cached data.

You can disable this behavior by adding a [custom Webpack configuration](https://nextjs.org/docs/app/api-reference/config/next-config-js/webpack) to your application:

```
<span><span>/** </span><span>@type</span><span> </span><span>{import('next').NextConfig}</span><span> */</span></span>
<span><span>const</span><span> </span><span>nextConfig</span><span> </span><span>=</span><span> {</span></span>
<span><span>  </span><span>webpack</span><span>:</span><span> (</span></span>
<span><span>    config</span><span>,</span></span>
<span><span>    { buildId</span><span>,</span><span> dev</span><span>,</span><span> isServer</span><span>,</span><span> defaultLoaders</span><span>,</span><span> nextRuntime</span><span>,</span><span> webpack }</span></span>
<span><span>  ) </span><span>=&gt;</span><span> {</span></span>
<span><span>    </span><span>if</span><span> (</span><span>config</span><span>.cache </span><span>&amp;&amp;</span><span> </span><span>!</span><span>dev) {</span></span>
<span><span>      </span><span>config</span><span>.cache </span><span>=</span><span> </span><span>Object</span><span>.freeze</span><span>({</span></span>
<span><span>        type</span><span>:</span><span> </span><span>'memory'</span><span>,</span></span>
<span><span>      })</span></span>
<span><span>    }</span></span>
<span><span>    </span><span>// Important: return the modified config</span></span>
<span><span>    </span><span>return</span><span> config</span></span>
<span><span>  }</span><span>,</span></span>
<span><span>}</span></span>
<span> </span>
<span><span>export</span><span> </span><span>default</span><span> nextConfig</span></span>
```

## [Disable static analysis](https://nextjs.org/docs/app/guides/memory-usage#disable-static-analysis)

Typechecking and linting may require a lot of memory, especially in large projects. However, most projects have a dedicated CI runner that already handles these tasks. When the build produces out-of-memory issues during the "Linting and checking validity of types" step, you can disable these task during builds:

```
<span><span>/** </span><span>@type</span><span> </span><span>{import('next').NextConfig}</span><span> */</span></span>
<span><span>const</span><span> </span><span>nextConfig</span><span> </span><span>=</span><span> {</span></span>
<span><span>  eslint</span><span>:</span><span> {</span></span>
<span><span>    </span><span>// Warning: This allows production builds to successfully complete even if</span></span>
<span><span>    </span><span>// your project has ESLint errors.</span></span>
<span><span>    ignoreDuringBuilds</span><span>:</span><span> </span><span>true</span><span>,</span></span>
<span><span>  }</span><span>,</span></span>
<span><span>  typescript</span><span>:</span><span> {</span></span>
<span><span>    </span><span>// !! WARN !!</span></span>
<span><span>    </span><span>// Dangerously allow production builds to successfully complete even if</span></span>
<span><span>    </span><span>// your project has type errors.</span></span>
<span><span>    </span><span>// !! WARN !!</span></span>
<span><span>    ignoreBuildErrors</span><span>:</span><span> </span><span>true</span><span>,</span></span>
<span><span>  }</span><span>,</span></span>
<span><span>}</span></span>
<span> </span>
<span><span>export</span><span> </span><span>default</span><span> nextConfig</span></span>
```

-   [Ignoring TypeScript Errors](https://nextjs.org/docs/app/api-reference/config/typescript#disabling-typescript-errors-in-production)
-   [ESLint in Next.js config](https://nextjs.org/docs/pages/api-reference/config/next-config-js/eslint)

Keep in mind that this may produce faulty deploys due to type errors or linting issues. We strongly recommend only promoting builds to production after static analysis has completed. If you deploy to Vercel, you can check out the [guide for staging deployments](https://vercel.com/docs/deployments/managing-deployments#staging-and-promoting-a-production-deployment) to learn how to promote builds to production after custom tasks have succeeded.

## [Disable source maps](https://nextjs.org/docs/app/guides/memory-usage#disable-source-maps)

Generating source maps consumes extra memory during the build process.

You can disable source map generation by adding `productionBrowserSourceMaps: false` and `experimental.serverSourceMaps: false` to your Next.js configuration.

> **Good to know**: Some plugins may turn on source maps and may require custom configuration to disable.

## [Edge memory issues](https://nextjs.org/docs/app/guides/memory-usage#edge-memory-issues)

Next.js `v14.1.3` fixed a memory issue when using the Edge runtime. Please update to this version (or later) to see if it addresses your issue.