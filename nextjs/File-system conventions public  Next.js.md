## public Folder

Next.js can serve static files, like images, under a folder called `public` in the root directory. Files inside `public` can then be referenced by your code starting from the base URL (`/`).

For example, the file `public/avatars/me.png` can be viewed by visiting the `/avatars/me.png` path. The code to display that image might look like:

```
<span><span>import</span><span> Image </span><span>from</span><span> </span><span>'next/image'</span></span>
<span> </span>
<span><span>export</span><span> </span><span>function</span><span> </span><span>Avatar</span><span>({ id</span><span>,</span><span> alt }) {</span></span>
<span><span>  </span><span>return</span><span> &lt;</span><span>Image</span><span> </span><span>src</span><span>=</span><span>{</span><span>`/avatars/</span><span>${</span><span>id</span><span>}</span><span>.png`</span><span>} </span><span>alt</span><span>=</span><span>{alt} </span><span>width</span><span>=</span><span>"64"</span><span> </span><span>height</span><span>=</span><span>"64"</span><span> /&gt;</span></span>
<span><span>}</span></span>
<span> </span>
<span><span>export</span><span> </span><span>function</span><span> </span><span>AvatarOfMe</span><span>() {</span></span>
<span><span>  </span><span>return</span><span> &lt;</span><span>Avatar</span><span> </span><span>id</span><span>=</span><span>"me"</span><span> </span><span>alt</span><span>=</span><span>"A portrait of me"</span><span> /&gt;</span></span>
<span><span>}</span></span>
```

## [Caching](https://nextjs.org/docs/app/api-reference/file-conventions/public-folder#caching)

Next.js cannot safely cache assets in the `public` folder because they may change. The default caching headers applied are:

```
<span><span>Cache</span><span>-</span><span>Control</span><span>:</span><span> public</span><span>,</span><span> max</span><span>-</span><span>age</span><span>=</span><span>0</span></span>
```

## [Robots, Favicons, and others](https://nextjs.org/docs/app/api-reference/file-conventions/public-folder#robots-favicons-and-others)

For static metadata files, such as `robots.txt`, `favicon.ico`, etc, you should use [special metadata files](https://nextjs.org/docs/app/api-reference/file-conventions/metadata) inside the `app` folder.