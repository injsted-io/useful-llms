The `instrumentation-client.js|ts` file allows you to add monitoring and analytics code that runs before your application's frontend code starts executing. This is useful for setting up performance tracking, error monitoring, or any other client-side observability tools.

To use it, place the file in the **root** of your application or inside a `src` folder.

## [Usage](https://nextjs.org/docs/app/api-reference/file-conventions/instrumentation-client#usage)

Unlike [server-side instrumentation](https://nextjs.org/docs/app/guides/instrumentation), you do not need to export any specific functions. You can write your monitoring code directly in the file:

instrumentation-client.ts

```
<span><span>// Set up performance monitoring</span></span>
<span><span>performance</span><span>.mark</span><span>(</span><span>'app-init'</span><span>)</span></span>
<span> </span>
<span><span>// Initialize analytics</span></span>
<span><span>console</span><span>.log</span><span>(</span><span>'Analytics initialized'</span><span>)</span></span>
<span> </span>
<span><span>// Set up error tracking</span></span>
<span><span>window</span><span>.addEventListener</span><span>(</span><span>'error'</span><span>,</span><span> (event) </span><span>=&gt;</span><span> {</span></span>
<span><span>  </span><span>// Send to your error tracking service</span></span>
<span><span>  </span><span>reportError</span><span>(</span><span>event</span><span>.error)</span></span>
<span><span>})</span></span>
```

## [Version History](https://nextjs.org/docs/app/api-reference/file-conventions/instrumentation-client#version-history)

| Version | Changes |
| --- | --- |
| `v15.3` | `instrumentation-client` introduced |