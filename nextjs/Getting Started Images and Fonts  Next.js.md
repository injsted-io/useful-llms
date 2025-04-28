## How to optimize images and fonts

Next.js comes with automatic image and font optimization. This page will guide you through how to start using them.

## [Optimizing images](https://nextjs.org/docs/app/getting-started/images-and-fonts#optimizing-images)

The Next.js [`<Image>`](https://nextjs.org/docs/app/building-your-application/optimizing/images) component extends the HTML `<img>` element to provide:

-   **Size optimization:** Automatically serving correctly sized images for each device, using modern image formats like WebP.
-   **Visual stability:** Preventing [layout shift](https://web.dev/articles/cls) automatically when images are loading.
-   **Faster page loads:** Only loading images when they enter the viewport using native browser lazy loading, with optional blur-up placeholders.
-   **Asset flexibility:** Resizing images on-demand, even images stored on remote servers.

To start using `<Image>`, import it from `next/image` and render it within your component.

```
<span><span>import</span><span> Image </span><span>from</span><span> </span><span>'next/image'</span></span>
<span> </span>
<span><span>export</span><span> </span><span>default</span><span> </span><span>function</span><span> </span><span>Page</span><span>() {</span></span>
<span><span>  </span><span>return</span><span> &lt;</span><span>Image</span><span> </span><span>src</span><span>=</span><span>""</span><span> </span><span>alt</span><span>=</span><span>""</span><span> /&gt;</span></span>
<span><span>}</span></span>
```

The `src` property can be a [local](https://nextjs.org/docs/app/getting-started/images-and-fonts#local-images) or [remote](https://nextjs.org/docs/app/getting-started/images-and-fonts#remote-images) image.

### [Local images](https://nextjs.org/docs/app/getting-started/images-and-fonts#local-images)

You can store static files, like images and fonts, under a folder called `public` in the root directory. Files inside `public` can then be referenced by your code starting from the base URL (`/`).

![Folder structure showing app and public folders](https://nextjs.org/_next/image?url=https%3A%2F%2Fh8DxKfmAPhn8O0p3.public.blob.vercel-storage.com%2Fdocs%2Fdark%2Fpublic-folder.png&w=3840&q=75)

```
<span><span>import</span><span> Image </span><span>from</span><span> </span><span>'next/image'</span></span>
<span><span>import</span><span> profilePic </span><span>from</span><span> </span><span>'./me.png'</span></span>
<span> </span>
<span><span>export</span><span> </span><span>default</span><span> </span><span>function</span><span> </span><span>Page</span><span>() {</span></span>
<span><span>  </span><span>return</span><span> (</span></span>
<span><span>    &lt;</span><span>Image</span></span>
<span><span>      </span><span>src</span><span>=</span><span>{profilePic}</span></span>
<span><span>      </span><span>alt</span><span>=</span><span>"Picture of the author"</span></span>
<span><span>      </span><span>// width={500} automatically provided</span></span>
<span><span>      </span><span>// height={500} automatically provided</span></span>
<span><span>      </span><span>// blurDataURL="data:..." automatically provided</span></span>
<span><span>      </span><span>// placeholder="blur" // Optional blur-up while loading</span></span>
<span><span>    /&gt;</span></span>
<span><span>  )</span></span>
<span><span>}</span></span>
```

Next.js will automatically determine the intrinsic [`width`](https://nextjs.org/docs/app/api-reference/components/image#width) and [`height`](https://nextjs.org/docs/app/api-reference/components/image#height) of your image based on the imported file. These values are used to determine the image ratio and prevent [Cumulative Layout Shift](https://web.dev/articles/cls) while your image is loading.

### [Remote images](https://nextjs.org/docs/app/getting-started/images-and-fonts#remote-images)

To use a remote image, you can provide a URL string for the `src` property.

```
<span><span>import</span><span> Image </span><span>from</span><span> </span><span>'next/image'</span></span>
<span> </span>
<span><span>export</span><span> </span><span>default</span><span> </span><span>function</span><span> </span><span>Page</span><span>() {</span></span>
<span><span>  </span><span>return</span><span> (</span></span>
<span><span>    &lt;</span><span>Image</span></span>
<span><span>      </span><span>src</span><span>=</span><span>"https://s3.amazonaws.com/my-bucket/profile.png"</span></span>
<span><span>      </span><span>alt</span><span>=</span><span>"Picture of the author"</span></span>
<span><span>      </span><span>width</span><span>=</span><span>{</span><span>500</span><span>}</span></span>
<span><span>      </span><span>height</span><span>=</span><span>{</span><span>500</span><span>}</span></span>
<span><span>    /&gt;</span></span>
<span><span>  )</span></span>
<span><span>}</span></span>
```

Since Next.js does not have access to remote files during the build process, you'll need to provide the [`width`](https://nextjs.org/docs/app/api-reference/components/image#width), [`height`](https://nextjs.org/docs/app/api-reference/components/image#height) and optional [`blurDataURL`](https://nextjs.org/docs/app/api-reference/components/image#blurdataurl) props manually. The `width` and `height` are used to infer the correct aspect ratio of image and avoid layout shift from the image loading in.

To safely allow images from remote servers, you need to define a list of supported URL patterns in [`next.config.js`](https://nextjs.org/docs/app/api-reference/config/next-config-js). Be as specific as possible to prevent malicious usage. For example, the following configuration will only allow images from a specific AWS S3 bucket:

```
<span><span>import</span><span> { NextConfig } </span><span>from</span><span> </span><span>'next'</span></span>
<span> </span>
<span><span>const</span><span> </span><span>config</span><span>:</span><span> </span><span>NextConfig</span><span> </span><span>=</span><span> {</span></span>
<span><span>  images</span><span>:</span><span> {</span></span>
<span><span>    remotePatterns</span><span>:</span><span> [</span></span>
<span><span>      {</span></span>
<span><span>        protocol</span><span>:</span><span> </span><span>'https'</span><span>,</span></span>
<span><span>        hostname</span><span>:</span><span> </span><span>'s3.amazonaws.com'</span><span>,</span></span>
<span><span>        port</span><span>:</span><span> </span><span>''</span><span>,</span></span>
<span><span>        pathname</span><span>:</span><span> </span><span>'/my-bucket/**'</span><span>,</span></span>
<span><span>        search</span><span>:</span><span> </span><span>''</span><span>,</span></span>
<span><span>      }</span><span>,</span></span>
<span><span>    ]</span><span>,</span></span>
<span><span>  }</span><span>,</span></span>
<span><span>}</span></span>
<span> </span>
<span><span>export</span><span> </span><span>default</span><span> config</span></span>
```

## [Optimizing fonts](https://nextjs.org/docs/app/getting-started/images-and-fonts#optimizing-fonts)

The [`next/font`](https://nextjs.org/docs/app/api-reference/components/font) module automatically optimizes your fonts and removes external network requests for improved privacy and performance.

It includes **built-in self-hosting** for any font file. This means you can optimally load web fonts with no layout shift.

To start using `next/font`, import it from [`next/font/local`](https://nextjs.org/docs/app/getting-started/images-and-fonts#local-fonts) or [`next/font/google`](https://nextjs.org/docs/app/getting-started/images-and-fonts#google-fonts), call it as a function with the appropriate options, and set the `className` of the element you want to apply the font to. For example:

```
<span><span>import</span><span> { Geist } </span><span>from</span><span> </span><span>'next/font/google'</span></span>
<span> </span>
<span><span>const</span><span> </span><span>geist</span><span> </span><span>=</span><span> </span><span>Geist</span><span>({</span></span>
<span><span>  subsets</span><span>:</span><span> [</span><span>'latin'</span><span>]</span><span>,</span></span>
<span><span>})</span></span>
<span> </span>
<span><span>export</span><span> </span><span>default</span><span> </span><span>function</span><span> </span><span>Layout</span><span>({ children }</span><span>:</span><span> { children</span><span>:</span><span> </span><span>React</span><span>.</span><span>ReactNode</span><span> }) {</span></span>
<span><span>  </span><span>return</span><span> (</span></span>
<span><span>    &lt;</span><span>html</span><span> </span><span>lang</span><span>=</span><span>"en"</span><span> </span><span>className</span><span>=</span><span>{</span><span>geist</span><span>.className}&gt;</span></span>
<span><span>      &lt;</span><span>body</span><span>&gt;{children}&lt;/</span><span>body</span><span>&gt;</span></span>
<span><span>    &lt;/</span><span>html</span><span>&gt;</span></span>
<span><span>  )</span></span>
<span><span>}</span></span>
```

### [Google fonts](https://nextjs.org/docs/app/getting-started/images-and-fonts#google-fonts)

You can automatically self-host any Google Font. Fonts are included in the deployment and served from the same domain as your deployment, meaning no requests are sent to Google by the browser when the user visits your site.

To start using a Google Font, import your chosen font from `next/font/google`:

```
<span><span>import</span><span> { Geist } </span><span>from</span><span> </span><span>'next/font/google'</span></span>
<span> </span>
<span><span>const</span><span> </span><span>geist</span><span> </span><span>=</span><span> </span><span>Geist</span><span>({</span></span>
<span><span>  subsets</span><span>:</span><span> [</span><span>'latin'</span><span>]</span><span>,</span></span>
<span><span>})</span></span>
<span> </span>
<span><span>export</span><span> </span><span>default</span><span> </span><span>function</span><span> </span><span>RootLayout</span><span>({</span></span>
<span><span>  children</span><span>,</span></span>
<span><span>}</span><span>:</span><span> {</span></span>
<span><span>  children</span><span>:</span><span> </span><span>React</span><span>.</span><span>ReactNode</span></span>
<span><span>}) {</span></span>
<span><span>  </span><span>return</span><span> (</span></span>
<span><span>    &lt;</span><span>html</span><span> </span><span>lang</span><span>=</span><span>"en"</span><span> </span><span>className</span><span>=</span><span>{</span><span>geist</span><span>.className}&gt;</span></span>
<span><span>      &lt;</span><span>body</span><span>&gt;{children}&lt;/</span><span>body</span><span>&gt;</span></span>
<span><span>    &lt;/</span><span>html</span><span>&gt;</span></span>
<span><span>  )</span></span>
<span><span>}</span></span>
```

We recommend using [variable fonts](https://fonts.google.com/variablefonts) for the best performance and flexibility. But if you can't use a variable font, you will need to specify a weight:

```
<span><span>import</span><span> { Roboto } </span><span>from</span><span> </span><span>'next/font/google'</span></span>
<span> </span>
<span><span>const</span><span> </span><span>roboto</span><span> </span><span>=</span><span> </span><span>Roboto</span><span>({</span></span>
<span><span>  weight</span><span>:</span><span> </span><span>'400'</span><span>,</span></span>
<span><span>  subsets</span><span>:</span><span> [</span><span>'latin'</span><span>]</span><span>,</span></span>
<span><span>})</span></span>
<span> </span>
<span><span>export</span><span> </span><span>default</span><span> </span><span>function</span><span> </span><span>RootLayout</span><span>({</span></span>
<span><span>  children</span><span>,</span></span>
<span><span>}</span><span>:</span><span> {</span></span>
<span><span>  children</span><span>:</span><span> </span><span>React</span><span>.</span><span>ReactNode</span></span>
<span><span>}) {</span></span>
<span><span>  </span><span>return</span><span> (</span></span>
<span><span>    &lt;</span><span>html</span><span> </span><span>lang</span><span>=</span><span>"en"</span><span> </span><span>className</span><span>=</span><span>{</span><span>roboto</span><span>.className}&gt;</span></span>
<span><span>      &lt;</span><span>body</span><span>&gt;{children}&lt;/</span><span>body</span><span>&gt;</span></span>
<span><span>    &lt;/</span><span>html</span><span>&gt;</span></span>
<span><span>  )</span></span>
<span><span>}</span></span>
```

### [Local fonts](https://nextjs.org/docs/app/getting-started/images-and-fonts#local-fonts)

To use a local font, import your font from `next/font/local` and specify the [`src`](https://nextjs.org/docs/app/api-reference/components/font#src) of your local font file.

```
<span><span>import</span><span> localFont </span><span>from</span><span> </span><span>'next/font/local'</span></span>
<span> </span>
<span><span>const</span><span> </span><span>myFont</span><span> </span><span>=</span><span> </span><span>localFont</span><span>({</span></span>
<span><span>  src</span><span>:</span><span> </span><span>'./my-font.woff2'</span><span>,</span></span>
<span><span>})</span></span>
<span> </span>
<span><span>export</span><span> </span><span>default</span><span> </span><span>function</span><span> </span><span>RootLayout</span><span>({</span></span>
<span><span>  children</span><span>,</span></span>
<span><span>}</span><span>:</span><span> {</span></span>
<span><span>  children</span><span>:</span><span> </span><span>React</span><span>.</span><span>ReactNode</span></span>
<span><span>}) {</span></span>
<span><span>  </span><span>return</span><span> (</span></span>
<span><span>    &lt;</span><span>html</span><span> </span><span>lang</span><span>=</span><span>"en"</span><span> </span><span>className</span><span>=</span><span>{</span><span>myFont</span><span>.className}&gt;</span></span>
<span><span>      &lt;</span><span>body</span><span>&gt;{children}&lt;/</span><span>body</span><span>&gt;</span></span>
<span><span>    &lt;/</span><span>html</span><span>&gt;</span></span>
<span><span>  )</span></span>
<span><span>}</span></span>
```

If you want to use multiple files for a single font family, `src` can be an array:

```
<span><span>const</span><span> </span><span>roboto</span><span> </span><span>=</span><span> </span><span>localFont</span><span>({</span></span>
<span><span>  src</span><span>:</span><span> [</span></span>
<span><span>    {</span></span>
<span><span>      path</span><span>:</span><span> </span><span>'./Roboto-Regular.woff2'</span><span>,</span></span>
<span><span>      weight</span><span>:</span><span> </span><span>'400'</span><span>,</span></span>
<span><span>      style</span><span>:</span><span> </span><span>'normal'</span><span>,</span></span>
<span><span>    }</span><span>,</span></span>
<span><span>    {</span></span>
<span><span>      path</span><span>:</span><span> </span><span>'./Roboto-Italic.woff2'</span><span>,</span></span>
<span><span>      weight</span><span>:</span><span> </span><span>'400'</span><span>,</span></span>
<span><span>      style</span><span>:</span><span> </span><span>'italic'</span><span>,</span></span>
<span><span>    }</span><span>,</span></span>
<span><span>    {</span></span>
<span><span>      path</span><span>:</span><span> </span><span>'./Roboto-Bold.woff2'</span><span>,</span></span>
<span><span>      weight</span><span>:</span><span> </span><span>'700'</span><span>,</span></span>
<span><span>      style</span><span>:</span><span> </span><span>'normal'</span><span>,</span></span>
<span><span>    }</span><span>,</span></span>
<span><span>    {</span></span>
<span><span>      path</span><span>:</span><span> </span><span>'./Roboto-BoldItalic.woff2'</span><span>,</span></span>
<span><span>      weight</span><span>:</span><span> </span><span>'700'</span><span>,</span></span>
<span><span>      style</span><span>:</span><span> </span><span>'italic'</span><span>,</span></span>
<span><span>    }</span><span>,</span></span>
<span><span>  ]</span><span>,</span></span>
<span><span>})</span></span>
```