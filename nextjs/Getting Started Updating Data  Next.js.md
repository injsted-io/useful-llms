## How to update data

You can update data in Next.js using React's [Server Functions](https://react.dev/reference/rsc/server-functions). This page will go through how you can [create](https://nextjs.org/docs/app/getting-started/updating-data#creating-server-functions) and [invoke](https://nextjs.org/docs/app/getting-started/updating-data#invoking-server-functions) Server Functions.

## [Creating Server Functions](https://nextjs.org/docs/app/getting-started/updating-data#creating-server-functions)

A Server Function can be defined by using the [`use server`](https://react.dev/reference/rsc/use-server) directive. You can place the directive at the top of an **asynchronous** function to mark the function as a Server Function, or at the top of a separate file to mark all exports of that file.

```
<span><span>export</span><span> </span><span>async</span><span> </span><span>function</span><span> </span><span>createPost</span><span>(formData</span><span>:</span><span> </span><span>FormData</span><span>) {</span></span>
<span><span>  </span><span>'use server'</span></span>
<span><span>  </span><span>const</span><span> </span><span>title</span><span> </span><span>=</span><span> </span><span>formData</span><span>.get</span><span>(</span><span>'title'</span><span>)</span></span>
<span><span>  </span><span>const</span><span> </span><span>content</span><span> </span><span>=</span><span> </span><span>formData</span><span>.get</span><span>(</span><span>'content'</span><span>)</span></span>
<span> </span>
<span><span>  </span><span>// Update data</span></span>
<span><span>  </span><span>// Revalidate cache</span></span>
<span><span>}</span></span>
<span> </span>
<span><span>export</span><span> </span><span>async</span><span> </span><span>function</span><span> </span><span>deletePost</span><span>(formData</span><span>:</span><span> </span><span>FormData</span><span>) {</span></span>
<span><span>  </span><span>'use server'</span></span>
<span><span>  </span><span>const</span><span> </span><span>id</span><span> </span><span>=</span><span> </span><span>formData</span><span>.get</span><span>(</span><span>'id'</span><span>)</span></span>
<span> </span>
<span><span>  </span><span>// Update data</span></span>
<span><span>  </span><span>// Revalidate cache</span></span>
<span><span>}</span></span>
```

### [Server Components](https://nextjs.org/docs/app/getting-started/updating-data#server-components)

Server Functions can be inlined in Server Components by adding the `"use server"` directive to the top of the function body:

```
<span><span>export</span><span> </span><span>default</span><span> </span><span>function</span><span> </span><span>Page</span><span>() {</span></span>
<span><span>  </span><span>// Server Action</span></span>
<span><span>  </span><span>async</span><span> </span><span>function</span><span> </span><span>createPost</span><span>(formData</span><span>:</span><span> </span><span>FormData</span><span>) {</span></span>
<span><span>    </span><span>'use server'</span></span>
<span><span>    </span><span>// ...</span></span>
<span><span>  }</span></span>
<span> </span>
<span><span>  </span><span>return</span><span> &lt;&gt;&lt;/&gt;</span></span>
<span><span>}</span></span>
```

### [Client Components](https://nextjs.org/docs/app/getting-started/updating-data#client-components)

It's not possible to define Server Functions in Client Components. However, you can invoke them in Client Components by importing them from a file that has the `"use server"` directive at the top of it:

```
<span><span>'use server'</span></span>
<span> </span>
<span><span>export</span><span> </span><span>async</span><span> </span><span>function</span><span> </span><span>createPost</span><span>() {}</span></span>
```

```
<span><span>'use client'</span></span>
<span> </span>
<span><span>import</span><span> { createPost } </span><span>from</span><span> </span><span>'@/app/actions'</span></span>
<span> </span>
<span><span>export</span><span> </span><span>function</span><span> </span><span>Button</span><span>() {</span></span>
<span><span>  </span><span>return</span><span> &lt;</span><span>button</span><span> </span><span>formAction</span><span>=</span><span>{createPost}&gt;Create&lt;/</span><span>button</span><span>&gt;</span></span>
<span><span>}</span></span>
```

## [Invoking Server Functions](https://nextjs.org/docs/app/getting-started/updating-data#invoking-server-functions)

There are two main ways you can invoke a Server Function:

1.  [Forms](https://nextjs.org/docs/app/getting-started/updating-data#forms) in Server and Client Components
2.  [Event Handlers](https://nextjs.org/docs/app/getting-started/updating-data#event-handlers) in Client Components

### [Forms](https://nextjs.org/docs/app/getting-started/updating-data#forms)

React extends the HTML [`<form>`](https://react.dev/reference/react-dom/components/form) element to allow Server Function to be invoked with the HTML `action` prop.

When invoked in a form, the function automatically receives the [`FormData`](https://developer.mozilla.org/docs/Web/API/FormData/FormData) object. You can extract the data using the native [`FormData` methods](https://developer.mozilla.org/en-US/docs/Web/API/FormData#instance_methods):

```
<span><span>import</span><span> { createPost } </span><span>from</span><span> </span><span>'@/app/actions'</span></span>
<span> </span>
<span><span>export</span><span> </span><span>function</span><span> </span><span>Form</span><span>() {</span></span>
<span><span>  </span><span>return</span><span> (</span></span>
<span><span>    &lt;</span><span>form</span><span> </span><span>action</span><span>=</span><span>{createPost}&gt;</span></span>
<span><span>      &lt;</span><span>input</span><span> </span><span>type</span><span>=</span><span>"text"</span><span> </span><span>name</span><span>=</span><span>"title"</span><span> /&gt;</span></span>
<span><span>      &lt;</span><span>input</span><span> </span><span>type</span><span>=</span><span>"text"</span><span> </span><span>name</span><span>=</span><span>"content"</span><span> /&gt;</span></span>
<span><span>      &lt;</span><span>button</span><span> </span><span>type</span><span>=</span><span>"submit"</span><span>&gt;Create&lt;/</span><span>button</span><span>&gt;</span></span>
<span><span>    &lt;/</span><span>form</span><span>&gt;</span></span>
<span><span>  )</span></span>
<span><span>}</span></span>
```

```
<span><span>'use server'</span></span>
<span> </span>
<span><span>export</span><span> </span><span>async</span><span> </span><span>function</span><span> </span><span>createPost</span><span>(formData</span><span>:</span><span> </span><span>FormData</span><span>) {</span></span>
<span><span>  </span><span>const</span><span> </span><span>title</span><span> </span><span>=</span><span> </span><span>formData</span><span>.get</span><span>(</span><span>'title'</span><span>)</span></span>
<span><span>  </span><span>const</span><span> </span><span>content</span><span> </span><span>=</span><span> </span><span>formData</span><span>.get</span><span>(</span><span>'content'</span><span>)</span></span>
<span> </span>
<span><span>  </span><span>// Update data</span></span>
<span><span>  </span><span>// Revalidate cache</span></span>
<span><span>}</span></span>
```

> **Good to know:** When passed to the `action` prop, Server Functions are also known as _Server Actions_.

### [Event Handlers](https://nextjs.org/docs/app/getting-started/updating-data#event-handlers)

You can invoke a Server Function in a Client Component by using event handlers such as `onClick`.

```
<span><span>'use client'</span></span>
<span> </span>
<span><span>import</span><span> { incrementLike } </span><span>from</span><span> </span><span>'./actions'</span></span>
<span><span>import</span><span> { useState } </span><span>from</span><span> </span><span>'react'</span></span>
<span> </span>
<span><span>export</span><span> </span><span>default</span><span> </span><span>function</span><span> </span><span>LikeButton</span><span>({ initialLikes }</span><span>:</span><span> { initialLikes</span><span>:</span><span> </span><span>number</span><span> }) {</span></span>
<span><span>  </span><span>const</span><span> [</span><span>likes</span><span>,</span><span> </span><span>setLikes</span><span>] </span><span>=</span><span> </span><span>useState</span><span>(initialLikes)</span></span>
<span> </span>
<span><span>  </span><span>return</span><span> (</span></span>
<span><span>    &lt;&gt;</span></span>
<span><span>      &lt;</span><span>p</span><span>&gt;Total Likes: {likes}&lt;/</span><span>p</span><span>&gt;</span></span>
<span><span>      &lt;</span><span>button</span></span>
<span><span>        </span><span>onClick</span><span>=</span><span>{</span><span>async</span><span> () </span><span>=&gt;</span><span> {</span></span>
<span><span>          </span><span>const</span><span> </span><span>updatedLikes</span><span> </span><span>=</span><span> </span><span>await</span><span> </span><span>incrementLike</span><span>()</span></span>
<span><span>          </span><span>setLikes</span><span>(updatedLikes)</span></span>
<span><span>        }}</span></span>
<span><span>      &gt;</span></span>
<span><span>        Like</span></span>
<span><span>      &lt;/</span><span>button</span><span>&gt;</span></span>
<span><span>    &lt;/&gt;</span></span>
<span><span>  )</span></span>
<span><span>}</span></span>
```

## [Examples](https://nextjs.org/docs/app/getting-started/updating-data#examples)

### [Showing a pending state](https://nextjs.org/docs/app/getting-started/updating-data#showing-a-pending-state)

While executing a Server Function, you can show a loading indicator with React's [`useActionState`](https://react.dev/reference/react/useActionState) hook. This hook returns a `pending` boolean:

```
<span><span>'use client'</span></span>
<span> </span>
<span><span>import</span><span> { useActionState } </span><span>from</span><span> </span><span>'react'</span></span>
<span><span>import</span><span> { createPost } </span><span>from</span><span> </span><span>'@/app/actions'</span></span>
<span><span>import</span><span> { LoadingSpinner } </span><span>from</span><span> </span><span>'@/app/</span><span>ui</span><span>/loading-spinner'</span></span>
<span> </span>
<span><span>export</span><span> </span><span>function</span><span> </span><span>Button</span><span>() {</span></span>
<span><span>  </span><span>const</span><span> [</span><span>state</span><span>,</span><span> </span><span>action</span><span>,</span><span> </span><span>pending</span><span>] </span><span>=</span><span> </span><span>useActionState</span><span>(createPost</span><span>,</span><span> </span><span>false</span><span>)</span></span>
<span> </span>
<span><span>  </span><span>return</span><span> (</span></span>
<span><span>    &lt;</span><span>button</span><span> </span><span>onClick</span><span>=</span><span>{</span><span>async</span><span> () </span><span>=&gt;</span><span> </span><span>action</span><span>()}&gt;</span></span>
<span><span>      {pending </span><span>?</span><span> &lt;</span><span>LoadingSpinner</span><span> /&gt; </span><span>:</span><span> </span><span>'Create Post'</span><span>}</span></span>
<span><span>    &lt;/</span><span>button</span><span>&gt;</span></span>
<span><span>  )</span></span>
<span><span>}</span></span>
```

### [Revalidating the cache](https://nextjs.org/docs/app/getting-started/updating-data#revalidating-the-cache)

After performing an update, you can revalidate the Next.js cache and show the updated data by calling [`revalidatePath`](https://nextjs.org/docs/app/api-reference/functions/revalidatePath) or [`revalidateTag`](https://nextjs.org/docs/app/api-reference/functions/revalidateTag) within the Server Function:

```
<span><span>import</span><span> { revalidatePath } </span><span>from</span><span> </span><span>'next/cache'</span></span>
<span> </span>
<span><span>export</span><span> </span><span>async</span><span> </span><span>function</span><span> </span><span>createPost</span><span>(formData</span><span>:</span><span> </span><span>FormData</span><span>) {</span></span>
<span><span>  </span><span>'use server'</span></span>
<span><span>  </span><span>// Update data</span></span>
<span><span>  </span><span>// ...</span></span>
<span> </span>
<span><span>  </span><span>revalidatePath</span><span>(</span><span>'/posts'</span><span>)</span></span>
<span><span>}</span></span>
```

### [Redirecting](https://nextjs.org/docs/app/getting-started/updating-data#redirecting)

You may want to redirect the user to a different page after performing an update. You can do this by calling [`redirect`](https://nextjs.org/docs/app/api-reference/functions/redirect) within the Server Function:

```
<span><span>'use server'</span></span>
<span> </span>
<span><span>import</span><span> { redirect } </span><span>from</span><span> </span><span>'next/navigation'</span></span>
<span> </span>
<span><span>export</span><span> </span><span>async</span><span> </span><span>function</span><span> </span><span>createPost</span><span>(formData</span><span>:</span><span> </span><span>FormData</span><span>) {</span></span>
<span><span>  </span><span>// Update data</span></span>
<span><span>  </span><span>// ...</span></span>
<span> </span>
<span><span>  </span><span>redirect</span><span>(</span><span>'/posts'</span><span>)</span></span>
<span><span>}</span></span>
```