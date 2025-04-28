This feature is currently experimental and subject to change, it's not recommended for production. Try it out and share your feedback on [GitHub](https://github.com/vercel/next.js/issues).

The **unauthorized** file is used to render UI when the [`unauthorized`](https://nextjs.org/docs/app/api-reference/functions/unauthorized) function is invoked during authentication. Along with allowing you to customize the UI, Next.js will return a `401` status code.

```
<span><span>import</span><span> Login </span><span>from</span><span> </span><span>'@/app/components/Login'</span></span>
<span> </span>
<span><span>export</span><span> </span><span>default</span><span> </span><span>function</span><span> </span><span>Unauthorized</span><span>() {</span></span>
<span><span>  </span><span>return</span><span> (</span></span>
<span><span>    &lt;</span><span>main</span><span>&gt;</span></span>
<span><span>      &lt;</span><span>h1</span><span>&gt;401 - Unauthorized&lt;/</span><span>h1</span><span>&gt;</span></span>
<span><span>      &lt;</span><span>p</span><span>&gt;Please log in to access this page.&lt;/</span><span>p</span><span>&gt;</span></span>
<span><span>      &lt;</span><span>Login</span><span> /&gt;</span></span>
<span><span>    &lt;/</span><span>main</span><span>&gt;</span></span>
<span><span>  )</span></span>
<span><span>}</span></span>
```

## [Reference](https://nextjs.org/docs/app/api-reference/file-conventions/unauthorized#reference)

### [Props](https://nextjs.org/docs/app/api-reference/file-conventions/unauthorized#props)

`unauthorized.js` components do not accept any props.

## [Examples](https://nextjs.org/docs/app/api-reference/file-conventions/unauthorized#examples)

### [Displaying login UI to unauthenticated users](https://nextjs.org/docs/app/api-reference/file-conventions/unauthorized#displaying-login-ui-to-unauthenticated-users)

You can use [`unauthorized`](https://nextjs.org/docs/app/api-reference/functions/unauthorized) function to render the `unauthorized.js` file with a login UI.

```
<span><span>import</span><span> { verifySession } </span><span>from</span><span> </span><span>'@/app/lib/dal'</span></span>
<span><span>import</span><span> { unauthorized } </span><span>from</span><span> </span><span>'next/navigation'</span></span>
<span> </span>
<span><span>export</span><span> </span><span>default</span><span> </span><span>async</span><span> </span><span>function</span><span> </span><span>DashboardPage</span><span>() {</span></span>
<span><span>  </span><span>const</span><span> </span><span>session</span><span> </span><span>=</span><span> </span><span>await</span><span> </span><span>verifySession</span><span>()</span></span>
<span> </span>
<span><span>  </span><span>if</span><span> (</span><span>!</span><span>session) {</span></span>
<span><span>    </span><span>unauthorized</span><span>()</span></span>
<span><span>  }</span></span>
<span> </span>
<span><span>  </span><span>return</span><span> &lt;</span><span>div</span><span>&gt;Dashboard&lt;/</span><span>div</span><span>&gt;</span></span>
<span><span>}</span></span>
```

```
<span><span>import</span><span> Login </span><span>from</span><span> </span><span>'@/app/components/Login'</span></span>
<span> </span>
<span><span>export</span><span> </span><span>default</span><span> </span><span>function</span><span> </span><span>UnauthorizedPage</span><span>() {</span></span>
<span><span>  </span><span>return</span><span> (</span></span>
<span><span>    &lt;</span><span>main</span><span>&gt;</span></span>
<span><span>      &lt;</span><span>h1</span><span>&gt;401 - Unauthorized&lt;/</span><span>h1</span><span>&gt;</span></span>
<span><span>      &lt;</span><span>p</span><span>&gt;Please log in to access this page.&lt;/</span><span>p</span><span>&gt;</span></span>
<span><span>      &lt;</span><span>Login</span><span> /&gt;</span></span>
<span><span>    &lt;/</span><span>main</span><span>&gt;</span></span>
<span><span>  )</span></span>
<span><span>}</span></span>
```

## [Version History](https://nextjs.org/docs/app/api-reference/file-conventions/unauthorized#version-history)

| Version | Changes |
| --- | --- |
| `v15.1.0` | `unauthorized.js` introduced. |