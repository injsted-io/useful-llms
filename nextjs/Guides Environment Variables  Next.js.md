## How to use environment variables in Next.js

Next.js comes with built-in support for environment variables, which allows you to do the following:

-   [Use `.env` to load environment variables](https://nextjs.org/docs/app/guides/environment-variables#loading-environment-variables)
-   [Bundle environment variables for the browser by prefixing with `NEXT_PUBLIC_`](https://nextjs.org/docs/app/guides/environment-variables#bundling-environment-variables-for-the-browser)

> **Warning:** The default `create-next-app` template ensures all `.env` files are added to your `.gitignore`. You almost never want to commit these files to your repository.

Next.js has built-in support for loading environment variables from `.env*` files into `process.env`.

```
<span><span>DB_HOST=localhost</span></span>
<span><span>DB_USER=myuser</span></span>
<span><span>DB_PASS=mypassword</span></span>
```

> **Note**: Next.js also supports multiline variables inside of your `.env*` files:
> 
> ```
> <span><span># .env</span></span>
> <span> </span>
> <span><span># you can write with line breaks</span></span>
> <span><span>PRIVATE_KEY</span><span>=</span><span>"-----BEGIN RSA PRIVATE KEY-----</span></span>
> <span><span>...</span></span>
> <span><span>Kh9NV...</span></span>
> <span><span>...</span></span>
> <span><span>-----END DSA PRIVATE KEY-----"</span></span>
> <span> </span>
> <span><span># or with `\n` inside double quotes</span></span>
> <span><span>PRIVATE_KEY</span><span>=</span><span>"-----BEGIN RSA PRIVATE KEY-----\nKh9NV...\n-----END DSA PRIVATE KEY-----\n"</span></span>
> ```

> **Note**: If you are using a `/src` folder, please note that Next.js will load the .env files **only** from the parent folder and **not** from the `/src` folder. This loads `process.env.DB_HOST`, `process.env.DB_USER`, and `process.env.DB_PASS` into the Node.js environment automatically allowing you to use them in [Route Handlers](https://nextjs.org/docs/app/building-your-application/routing/route-handlers).

For example:

```
<span><span>export</span><span> </span><span>async</span><span> </span><span>function</span><span> </span><span>GET</span><span>() {</span></span>
<span><span>  </span><span>const</span><span> </span><span>db</span><span> </span><span>=</span><span> </span><span>await</span><span> </span><span>myDB</span><span>.connect</span><span>({</span></span>
<span><span>    host</span><span>:</span><span> </span><span>process</span><span>.</span><span>env</span><span>.</span><span>DB_HOST</span><span>,</span></span>
<span><span>    username</span><span>:</span><span> </span><span>process</span><span>.</span><span>env</span><span>.</span><span>DB_USER</span><span>,</span></span>
<span><span>    password</span><span>:</span><span> </span><span>process</span><span>.</span><span>env</span><span>.</span><span>DB_PASS</span><span>,</span></span>
<span><span>  })</span></span>
<span><span>  </span><span>// ...</span></span>
<span><span>}</span></span>
```

### [Loading Environment Variables with `@next/env`](https://nextjs.org/docs/app/guides/environment-variables#loading-environment-variables-with-nextenv)

If you need to load environment variables outside of the Next.js runtime, such as in a root config file for an ORM or test runner, you can use the `@next/env` package.

This package is used internally by Next.js to load environment variables from `.env*` files.

To use it, install the package and use the `loadEnvConfig` function to load the environment variables:

```
<span><span>import</span><span> { loadEnvConfig } </span><span>from</span><span> </span><span>'@next/env'</span></span>
<span> </span>
<span><span>const</span><span> </span><span>projectDir</span><span> </span><span>=</span><span> </span><span>process</span><span>.cwd</span><span>()</span></span>
<span><span>loadEnvConfig</span><span>(projectDir)</span></span>
```

Then, you can import the configuration where needed. For example:

```
<span><span>import</span><span> </span><span>'./envConfig.ts'</span></span>
<span> </span>
<span><span>export</span><span> </span><span>default</span><span> </span><span>defineConfig</span><span>({</span></span>
<span><span>  dbCredentials</span><span>:</span><span> {</span></span>
<span><span>    connectionString</span><span>:</span><span> </span><span>process</span><span>.</span><span>env</span><span>.</span><span>DATABASE_URL</span><span>!</span><span>,</span></span>
<span><span>  }</span><span>,</span></span>
<span><span>})</span></span>
```

### [Referencing Other Variables](https://nextjs.org/docs/app/guides/environment-variables#referencing-other-variables)

Next.js will automatically expand variables that use `$` to reference other variables e.g. `$VARIABLE` inside of your `.env*` files. This allows you to reference other secrets. For example:

```
<span><span>TWITTER_USER=nextjs</span></span>
<span><span>TWITTER_URL=https://x.com/$TWITTER_USER</span></span>
```

In the above example, `process.env.TWITTER_URL` would be set to `https://x.com/nextjs`.

> **Good to know**: If you need to use variable with a `$` in the actual value, it needs to be escaped e.g. `\$`.

## [Bundling Environment Variables for the Browser](https://nextjs.org/docs/app/guides/environment-variables#bundling-environment-variables-for-the-browser)

Non-`NEXT_PUBLIC_` environment variables are only available in the Node.js environment, meaning they aren't accessible to the browser (the client runs in a different _environment_).

In order to make the value of an environment variable accessible in the browser, Next.js can "inline" a value, at build time, into the js bundle that is delivered to the client, replacing all references to `process.env.[variable]` with a hard-coded value. To tell it to do this, you just have to prefix the variable with `NEXT_PUBLIC_`. For example:

```
<span><span>NEXT_PUBLIC_ANALYTICS_ID=abcdefghijk</span></span>
```

This will tell Next.js to replace all references to `process.env.NEXT_PUBLIC_ANALYTICS_ID` in the Node.js environment with the value from the environment in which you run `next build`, allowing you to use it anywhere in your code. It will be inlined into any JavaScript sent to the browser.

> **Note**: After being built, your app will no longer respond to changes to these environment variables. For instance, if you use a Heroku pipeline to promote slugs built in one environment to another environment, or if you build and deploy a single Docker image to multiple environments, all `NEXT_PUBLIC_` variables will be frozen with the value evaluated at build time, so these values need to be set appropriately when the project is built. If you need access to runtime environment values, you'll have to setup your own API to provide them to the client (either on demand or during initialization).

```
<span><span>import</span><span> setupAnalyticsService </span><span>from</span><span> </span><span>'../lib/my-analytics-service'</span></span>
<span> </span>
<span><span>// 'NEXT_PUBLIC_ANALYTICS_ID' can be used here as it's prefixed by 'NEXT_PUBLIC_'.</span></span>
<span><span>// It will be transformed at build time to `setupAnalyticsService('abcdefghijk')`.</span></span>
<span><span>setupAnalyticsService</span><span>(</span><span>process</span><span>.</span><span>env</span><span>.</span><span>NEXT_PUBLIC_ANALYTICS_ID</span><span>)</span></span>
<span> </span>
<span><span>function</span><span> </span><span>HomePage</span><span>() {</span></span>
<span><span>  </span><span>return</span><span> &lt;</span><span>h1</span><span>&gt;Hello World&lt;/</span><span>h1</span><span>&gt;</span></span>
<span><span>}</span></span>
<span> </span>
<span><span>export</span><span> </span><span>default</span><span> HomePage</span></span>
```

Note that dynamic lookups will _not_ be inlined, such as:

```
<span><span>// This will NOT be inlined, because it uses a variable</span></span>
<span><span>const</span><span> </span><span>varName</span><span> </span><span>=</span><span> </span><span>'NEXT_PUBLIC_ANALYTICS_ID'</span></span>
<span><span>setupAnalyticsService</span><span>(</span><span>process</span><span>.env[varName])</span></span>
<span> </span>
<span><span>// This will NOT be inlined, because it uses a variable</span></span>
<span><span>const</span><span> </span><span>env</span><span> </span><span>=</span><span> </span><span>process</span><span>.env</span></span>
<span><span>setupAnalyticsService</span><span>(</span><span>env</span><span>.</span><span>NEXT_PUBLIC_ANALYTICS_ID</span><span>)</span></span>
```

### [Runtime Environment Variables](https://nextjs.org/docs/app/guides/environment-variables#runtime-environment-variables)

Next.js can support both build time and runtime environment variables.

**By default, environment variables are only available on the server**. To expose an environment variable to the browser, it must be prefixed with `NEXT_PUBLIC_`. However, these public environment variables will be inlined into the JavaScript bundle during `next build`.

You can safely read environment variables on the server during dynamic rendering:

```
<span><span>import</span><span> { connection } </span><span>from</span><span> </span><span>'next/server'</span></span>
<span> </span>
<span><span>export</span><span> </span><span>default</span><span> </span><span>async</span><span> </span><span>function</span><span> </span><span>Component</span><span>() {</span></span>
<span><span>  </span><span>await</span><span> </span><span>connection</span><span>()</span></span>
<span><span>  </span><span>// cookies, headers, and other Dynamic APIs</span></span>
<span><span>  </span><span>// will also opt into dynamic rendering, meaning</span></span>
<span><span>  </span><span>// this env variable is evaluated at runtime</span></span>
<span><span>  </span><span>const</span><span> </span><span>value</span><span> </span><span>=</span><span> </span><span>process</span><span>.</span><span>env</span><span>.</span><span>MY_VALUE</span></span>
<span><span>  </span><span>// ...</span></span>
<span><span>}</span></span>
```

This allows you to use a singular Docker image that can be promoted through multiple environments with different values.

**Good to know:**

-   You can run code on server startup using the [`register` function](https://nextjs.org/docs/app/guides/instrumentation).
-   We do not recommend using the [`runtimeConfig`](https://nextjs.org/docs/pages/api-reference/config/next-config-js/runtime-configuration) option, as this does not work with the standalone output mode. Instead, we recommend [incrementally adopting](https://nextjs.org/docs/app/guides/migrating/app-router-migration) the App Router if you need this feature.

## [Test Environment Variables](https://nextjs.org/docs/app/guides/environment-variables#test-environment-variables)

Apart from `development` and `production` environments, there is a 3rd option available: `test`. In the same way you can set defaults for development or production environments, you can do the same with a `.env.test` file for the `testing` environment (though this one is not as common as the previous two). Next.js will not load environment variables from `.env.development` or `.env.production` in the `testing` environment.

This one is useful when running tests with tools like `jest` or `cypress` where you need to set specific environment vars only for testing purposes. Test default values will be loaded if `NODE_ENV` is set to `test`, though you usually don't need to do this manually as testing tools will address it for you.

There is a small difference between `test` environment, and both `development` and `production` that you need to bear in mind: `.env.local` won't be loaded, as you expect tests to produce the same results for everyone. This way every test execution will use the same env defaults across different executions by ignoring your `.env.local` (which is intended to override the default set).

> **Good to know**: similar to Default Environment Variables, `.env.test` file should be included in your repository, but `.env.test.local` shouldn't, as `.env*.local` are intended to be ignored through `.gitignore`.

While running unit tests you can make sure to load your environment variables the same way Next.js does by leveraging the `loadEnvConfig` function from the `@next/env` package.

```
<span><span>// The below can be used in a Jest global setup file or similar for your testing set-up</span></span>
<span><span>import</span><span> { loadEnvConfig } </span><span>from</span><span> </span><span>'@next/env'</span></span>
<span> </span>
<span><span>export</span><span> </span><span>default</span><span> </span><span>async</span><span> () </span><span>=&gt;</span><span> {</span></span>
<span><span>  </span><span>const</span><span> </span><span>projectDir</span><span> </span><span>=</span><span> </span><span>process</span><span>.cwd</span><span>()</span></span>
<span><span>  </span><span>loadEnvConfig</span><span>(projectDir)</span></span>
<span><span>}</span></span>
```

## [Environment Variable Load Order](https://nextjs.org/docs/app/guides/environment-variables#environment-variable-load-order)

Environment variables are looked up in the following places, in order, stopping once the variable is found.

1.  `process.env`
2.  `.env.$(NODE_ENV).local`
3.  `.env.local` (Not checked when `NODE_ENV` is `test`.)
4.  `.env.$(NODE_ENV)`
5.  `.env`

For example, if `NODE_ENV` is `development` and you define a variable in both `.env.development.local` and `.env`, the value in `.env.development.local` will be used.

> **Good to know**: The allowed values for `NODE_ENV` are `production`, `development` and `test`.

## [Good to know](https://nextjs.org/docs/app/guides/environment-variables#good-to-know)

-   If you are using a [`/src` directory](https://nextjs.org/docs/app/api-reference/file-conventions/src-folder), `.env.*` files should remain in the root of your project.
-   If the environment variable `NODE_ENV` is unassigned, Next.js automatically assigns `development` when running the `next dev` command, or `production` for all other commands.

## [Version History](https://nextjs.org/docs/app/guides/environment-variables#version-history)

| Version | Changes |
| --- | --- |
| `v9.4.0` | Support `.env` and `NEXT_PUBLIC_` introduced. |