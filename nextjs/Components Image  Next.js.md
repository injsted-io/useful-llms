Examples

-   [Image Component](https://github.com/vercel/next.js/tree/canary/examples/image-component)

This API reference will help you understand how to use [props](https://nextjs.org/docs/app/api-reference/components/image#props) and [configuration options](https://nextjs.org/docs/app/api-reference/components/image#configuration-options) available for the Image Component. For features and usage, please see the [Image Component](https://nextjs.org/docs/app/building-your-application/optimizing/images) page.

```
<span><span>import</span><span> Image </span><span>from</span><span> </span><span>'next/image'</span></span>
<span> </span>
<span><span>export</span><span> </span><span>default</span><span> </span><span>function</span><span> </span><span>Page</span><span>() {</span></span>
<span><span>  </span><span>return</span><span> (</span></span>
<span><span>    &lt;</span><span>Image</span></span>
<span><span>      </span><span>src</span><span>=</span><span>"/profile.png"</span></span>
<span><span>      </span><span>width</span><span>=</span><span>{</span><span>500</span><span>}</span></span>
<span><span>      </span><span>height</span><span>=</span><span>{</span><span>500</span><span>}</span></span>
<span><span>      </span><span>alt</span><span>=</span><span>"Picture of the author"</span></span>
<span><span>    /&gt;</span></span>
<span><span>  )</span></span>
<span><span>}</span></span>
```

## [Props](https://nextjs.org/docs/app/api-reference/components/image#props)

Here's a summary of the props available for the Image Component:

| Prop | Example | Type | Status |
| --- | --- | --- | --- |
| [`src`](https://nextjs.org/docs/app/api-reference/components/image#src) | `src="/profile.png"` | String | Required |
| [`width`](https://nextjs.org/docs/app/api-reference/components/image#width) | `width={500}` | Integer (px) | Required |
| [`height`](https://nextjs.org/docs/app/api-reference/components/image#height) | `height={500}` | Integer (px) | Required |
| [`alt`](https://nextjs.org/docs/app/api-reference/components/image#alt) | `alt="Picture of the author"` | String | Required |
| [`loader`](https://nextjs.org/docs/app/api-reference/components/image#loader) | `loader={imageLoader}` | Function | \- |
| [`fill`](https://nextjs.org/docs/app/api-reference/components/image#fill) | `fill={true}` | Boolean | \- |
| [`sizes`](https://nextjs.org/docs/app/api-reference/components/image#sizes) | `sizes="(max-width: 768px) 100vw, 33vw"` | String | \- |
| [`quality`](https://nextjs.org/docs/app/api-reference/components/image#quality) | `quality={80}` | Integer (1-100) | \- |
| [`priority`](https://nextjs.org/docs/app/api-reference/components/image#priority) | `priority={true}` | Boolean | \- |
| [`placeholder`](https://nextjs.org/docs/app/api-reference/components/image#placeholder) | `placeholder="blur"` | String | \- |
| [`style`](https://nextjs.org/docs/app/api-reference/components/image#style) | `style={{objectFit: "contain"}}` | Object | \- |
| [`onLoadingComplete`](https://nextjs.org/docs/app/api-reference/components/image#onloadingcomplete) | `onLoadingComplete={img => done())}` | Function | Deprecated |
| [`onLoad`](https://nextjs.org/docs/app/api-reference/components/image#onload) | `onLoad={event => done())}` | Function | \- |
| [`onError`](https://nextjs.org/docs/app/api-reference/components/image#onerror) | `onError(event => fail()}` | Function | \- |
| [`loading`](https://nextjs.org/docs/app/api-reference/components/image#loading) | `loading="lazy"` | String | \- |
| [`blurDataURL`](https://nextjs.org/docs/app/api-reference/components/image#blurdataurl) | `blurDataURL="data:image/jpeg..."` | String | \- |
| [`overrideSrc`](https://nextjs.org/docs/app/api-reference/components/image#overridesrc) | `overrideSrc="/seo.png"` | String | \- |

## [Required Props](https://nextjs.org/docs/app/api-reference/components/image#required-props)

The Image Component requires the following properties: `src`, `alt`, `width` and `height` (or `fill`).

```
<span><span>import</span><span> Image </span><span>from</span><span> </span><span>'next/image'</span></span>
<span> </span>
<span><span>export</span><span> </span><span>default</span><span> </span><span>function</span><span> </span><span>Page</span><span>() {</span></span>
<span><span>  </span><span>return</span><span> (</span></span>
<span><span>    &lt;</span><span>div</span><span>&gt;</span></span>
<span><span>      &lt;</span><span>Image</span></span>
<span><span>        </span><span>src</span><span>=</span><span>"/profile.png"</span></span>
<span><span>        </span><span>width</span><span>=</span><span>{</span><span>500</span><span>}</span></span>
<span><span>        </span><span>height</span><span>=</span><span>{</span><span>500</span><span>}</span></span>
<span><span>        </span><span>alt</span><span>=</span><span>"Picture of the author"</span></span>
<span><span>      /&gt;</span></span>
<span><span>    &lt;/</span><span>div</span><span>&gt;</span></span>
<span><span>  )</span></span>
<span><span>}</span></span>
```

### [`src`](https://nextjs.org/docs/app/api-reference/components/image#src)

Must be one of the following:

-   A [statically imported](https://nextjs.org/docs/app/building-your-application/optimizing/images#local-images) image file
-   A path string. This can be either an absolute external URL, or an internal path depending on the [loader](https://nextjs.org/docs/app/api-reference/components/image#loader) prop.

When using the default [loader](https://nextjs.org/docs/app/api-reference/components/image#loader), also consider the following for source images:

-   When src is an external URL, you must also configure [remotePatterns](https://nextjs.org/docs/app/api-reference/components/image#remotepatterns)
-   When src is [animated](https://nextjs.org/docs/app/api-reference/components/image#animated-images) or not a known format (JPEG, PNG, WebP, AVIF, GIF, TIFF) the image will be served as-is
-   When src is SVG format, it will be blocked unless [`unoptimized`](https://nextjs.org/docs/app/api-reference/components/image#unoptimized) or [`dangerouslyAllowSVG`](https://nextjs.org/docs/app/api-reference/components/image#dangerouslyallowsvg) is enabled

### [`width`](https://nextjs.org/docs/app/api-reference/components/image#width)

The `width` property represents the _intrinsic_ image width in pixels. This property is used to infer the correct aspect ratio of the image and avoid layout shift during loading. It does not determine the rendered size of the image, which is controlled by CSS, similar to the `width` attribute in the HTML `<img>` tag.

Required, except for [statically imported images](https://nextjs.org/docs/app/building-your-application/optimizing/images#local-images) or images with the [`fill` property](https://nextjs.org/docs/app/api-reference/components/image#fill).

### [`height`](https://nextjs.org/docs/app/api-reference/components/image#height)

The `height` property represents the _intrinsic_ image height in pixels. This property is used to infer the correct aspect ratio of the image and avoid layout shift during loading. It does not determine the rendered size of the image, which is controlled by CSS, similar to the `height` attribute in the HTML `<img>` tag.

Required, except for [statically imported images](https://nextjs.org/docs/app/building-your-application/optimizing/images#local-images) or images with the [`fill` property](https://nextjs.org/docs/app/api-reference/components/image#fill).

> **Good to know:**
> 
> -   Combined, both `width` and `height` properties are used to determine the aspect ratio of the image which used by browsers to reserve space for the image before it loads.
> -   The intrinsic size does not always mean the rendered size in the browser, which will be determined by the parent container. For example, if the parent container is smaller than the intrinsic size, the image will be scaled down to fit the container.
> -   You can use the [`fill`](https://nextjs.org/docs/app/api-reference/components/image#fill) property when the width and height are unknown.

### [`alt`](https://nextjs.org/docs/app/api-reference/components/image#alt)

The `alt` property is used to describe the image for screen readers and search engines. It is also the fallback text if images have been disabled or an error occurs while loading the image.

It should contain text that could replace the image [without changing the meaning of the page](https://html.spec.whatwg.org/multipage/images.html#general-guidelines). It is not meant to supplement the image and should not repeat information that is already provided in the captions above or below the image.

If the image is [purely decorative](https://html.spec.whatwg.org/multipage/images.html#a-purely-decorative-image-that-doesn't-add-any-information) or [not intended for the user](https://html.spec.whatwg.org/multipage/images.html#an-image-not-intended-for-the-user), the `alt` property should be an empty string (`alt=""`).

[Learn more](https://html.spec.whatwg.org/multipage/images.html#alt)

## [Optional Props](https://nextjs.org/docs/app/api-reference/components/image#optional-props)

The `<Image />` component accepts a number of additional properties beyond those which are required. This section describes the most commonly-used properties of the Image component. Find details about more rarely-used properties in the [Advanced Props](https://nextjs.org/docs/app/api-reference/components/image#advanced-props) section.

### [`loader`](https://nextjs.org/docs/app/api-reference/components/image#loader)

A custom function used to resolve image URLs.

A `loader` is a function returning a URL string for the image, given the following parameters:

-   [`src`](https://nextjs.org/docs/app/api-reference/components/image#src)
-   [`width`](https://nextjs.org/docs/app/api-reference/components/image#width)
-   [`quality`](https://nextjs.org/docs/app/api-reference/components/image#quality)

Here is an example of using a custom loader:

```
<span><span>'use client'</span></span>
<span> </span>
<span><span>import</span><span> Image </span><span>from</span><span> </span><span>'next/image'</span></span>
<span> </span>
<span><span>const</span><span> </span><span>imageLoader</span><span> </span><span>=</span><span> ({ src</span><span>,</span><span> width</span><span>,</span><span> quality }) </span><span>=&gt;</span><span> {</span></span>
<span><span>  </span><span>return</span><span> </span><span>`https://example.com/</span><span>${</span><span>src</span><span>}</span><span>?w=</span><span>${</span><span>width</span><span>}</span><span>&amp;q=</span><span>${</span><span>quality </span><span>||</span><span> </span><span>75</span><span>}</span><span>`</span></span>
<span><span>}</span></span>
<span> </span>
<span><span>export</span><span> </span><span>default</span><span> </span><span>function</span><span> </span><span>Page</span><span>() {</span></span>
<span><span>  </span><span>return</span><span> (</span></span>
<span><span>    &lt;</span><span>Image</span></span>
<span><span>      </span><span>loader</span><span>=</span><span>{imageLoader}</span></span>
<span><span>      </span><span>src</span><span>=</span><span>"me.png"</span></span>
<span><span>      </span><span>alt</span><span>=</span><span>"Picture of the author"</span></span>
<span><span>      </span><span>width</span><span>=</span><span>{</span><span>500</span><span>}</span></span>
<span><span>      </span><span>height</span><span>=</span><span>{</span><span>500</span><span>}</span></span>
<span><span>    /&gt;</span></span>
<span><span>  )</span></span>
<span><span>}</span></span>
```

> **Good to know**: Using props like `loader`, which accept a function, requires using [Client Components](https://nextjs.org/docs/app/building-your-application/rendering/client-components) to serialize the provided function.

Alternatively, you can use the [loaderFile](https://nextjs.org/docs/app/api-reference/components/image#loaderfile) configuration in `next.config.js` to configure every instance of `next/image` in your application, without passing a prop.

### [`fill`](https://nextjs.org/docs/app/api-reference/components/image#fill)

```
<span><span>fill</span><span>=</span><span>{true} </span><span>// {true} | {false}</span></span>
```

A boolean that causes the image to fill the parent element, which is useful when the [`width`](https://nextjs.org/docs/app/api-reference/components/image#width) and [`height`](https://nextjs.org/docs/app/api-reference/components/image#height) are unknown.

The parent element _must_ assign `position: "relative"`, `position: "fixed"`, or `position: "absolute"` style.

By default, the img element will automatically be assigned the `position: "absolute"` style.

If no styles are applied to the image, the image will stretch to fit the container. You may prefer to set `object-fit: "contain"` for an image which is letterboxed to fit the container and preserve aspect ratio.

Alternatively, `object-fit: "cover"` will cause the image to fill the entire container and be cropped to preserve aspect ratio.

For more information, see also:

-   [`position`](https://developer.mozilla.org/docs/Web/CSS/position)
-   [`object-fit`](https://developer.mozilla.org/docs/Web/CSS/object-fit)
-   [`object-position`](https://developer.mozilla.org/docs/Web/CSS/object-position)

### [`sizes`](https://nextjs.org/docs/app/api-reference/components/image#sizes)

A string, similar to a media query, that provides information about how wide the image will be at different breakpoints. The value of `sizes` will greatly affect performance for images using [`fill`](https://nextjs.org/docs/app/api-reference/components/image#fill) or which are [styled to have a responsive size](https://nextjs.org/docs/app/api-reference/components/image#responsive-images).

The `sizes` property serves two important purposes related to image performance:

-   First, the value of `sizes` is used by the browser to determine which size of the image to download, from `next/image`'s automatically generated `srcset`. When the browser chooses, it does not yet know the size of the image on the page, so it selects an image that is the same size or larger than the viewport. The `sizes` property allows you to tell the browser that the image will actually be smaller than full screen. If you don't specify a `sizes` value in an image with the `fill` property, a default value of `100vw` (full screen width) is used.
-   Second, the `sizes` property changes the behavior of the automatically generated `srcset` value. If no `sizes` value is present, a small `srcset` is generated, suitable for a fixed-size image (1x/2x/etc). If `sizes` is defined, a large `srcset` is generated, suitable for a responsive image (640w/750w/etc). If the `sizes` property includes sizes such as `50vw`, which represent a percentage of the viewport width, then the `srcset` is trimmed to not include any values which are too small to ever be necessary.

For example, if you know your styling will cause an image to be full-width on mobile devices, in a 2-column layout on tablets, and a 3-column layout on desktop displays, you should include a sizes property such as the following:

```
<span><span>import</span><span> Image </span><span>from</span><span> </span><span>'next/image'</span></span>
<span> </span>
<span><span>export</span><span> </span><span>default</span><span> </span><span>function</span><span> </span><span>Page</span><span>() {</span></span>
<span><span>  </span><span>return</span><span> (</span></span>
<span><span>    &lt;</span><span>div</span><span> </span><span>className</span><span>=</span><span>"grid-element"</span><span>&gt;</span></span>
<span><span>      &lt;</span><span>Image</span></span>
<span><span>        </span><span>fill</span></span>
<span><span>        </span><span>src</span><span>=</span><span>"/example.png"</span></span>
<span><span>        </span><span>sizes</span><span>=</span><span>"(max-width: 768px) 100vw, (max-width: 1200px) 50vw, 33vw"</span></span>
<span><span>      /&gt;</span></span>
<span><span>    &lt;/</span><span>div</span><span>&gt;</span></span>
<span><span>  )</span></span>
<span><span>}</span></span>
```

This example `sizes` could have a dramatic effect on performance metrics. Without the `33vw` sizes, the image selected from the server would be 3 times as wide as it needs to be. Because file size is proportional to the square of the width, without `sizes` the user would download an image that's 9 times larger than necessary.

Learn more about `srcset` and `sizes`:

-   [web.dev](https://web.dev/learn/design/responsive-images/#sizes)
-   [mdn](https://developer.mozilla.org/docs/Web/HTML/Element/img#sizes)

### [`quality`](https://nextjs.org/docs/app/api-reference/components/image#quality)

```
<span><span>quality</span><span>=</span><span>{</span><span>75</span><span>} </span><span>// {number 1-100}</span></span>
```

The quality of the optimized image, an integer between `1` and `100`, where `100` is the best quality and therefore largest file size. Defaults to `75`.

If the [`qualities`](https://nextjs.org/docs/app/api-reference/components/image#qualities) configuration is defined in `next.config.js`, the `quality` prop must match one of the values defined in the configuration.

> **Good to know**: If the original source image was already low quality, setting the quality prop too high could cause the resulting optimized image to be larger than the original source image.

### [`priority`](https://nextjs.org/docs/app/api-reference/components/image#priority)

```
<span><span>priority</span><span>=</span><span>{false} </span><span>// {false} | {true}</span></span>
```

When true, Next.js will [preload](https://web.dev/preload-responsive-images/) the image. Lazy loading is automatically disabled for images using `priority`. If the [`loading`](https://nextjs.org/docs/app/api-reference/components/image#loading) property is also used and set to `lazy`, the `priority` property can't be used. The [`loading`](https://nextjs.org/docs/app/api-reference/components/image#loading) property is only meant for advanced use cases. Remove `loading` when `priority` is needed.

You should use the `priority` property on any image detected as the [Largest Contentful Paint (LCP)](https://nextjs.org/learn/seo/web-performance/lcp) element. It may be appropriate to have multiple priority images, as different images may be the LCP element for different viewport sizes.

Should only be used when the image is visible above the fold. Defaults to `false`.

### [`placeholder`](https://nextjs.org/docs/app/api-reference/components/image#placeholder)

```
<span><span>placeholder </span><span>=</span><span> </span><span>'empty'</span><span> </span><span>// "empty" | "blur" | "data:image/..."</span></span>
```

A placeholder to use while the image is loading. Possible values are `blur`, `empty`, or `data:image/...`. Defaults to `empty`.

When `blur`, the [`blurDataURL`](https://nextjs.org/docs/app/api-reference/components/image#blurdataurl) property will be used as the placeholder. If `src` is an object from a [static import](https://nextjs.org/docs/app/building-your-application/optimizing/images#local-images) and the imported image is `.jpg`, `.png`, `.webp`, or `.avif`, then `blurDataURL` will be automatically populated, except when the image is detected to be animated.

For dynamic images, you must provide the [`blurDataURL`](https://nextjs.org/docs/app/api-reference/components/image#blurdataurl) property. Solutions such as [Plaiceholder](https://github.com/joe-bell/plaiceholder) can help with `base64` generation.

When `data:image/...`, the [Data URL](https://developer.mozilla.org/docs/Web/HTTP/Basics_of_HTTP/Data_URIs) will be used as the placeholder while the image is loading.

When `empty`, there will be no placeholder while the image is loading, only empty space.

Try it out:

-   [Demo the `blur` placeholder](https://image-component.nextjs.gallery/placeholder)
-   [Demo the shimmer effect with data URL `placeholder` prop](https://image-component.nextjs.gallery/shimmer)
-   [Demo the color effect with `blurDataURL` prop](https://image-component.nextjs.gallery/color)

## [Advanced Props](https://nextjs.org/docs/app/api-reference/components/image#advanced-props)

In some cases, you may need more advanced usage. The `<Image />` component optionally accepts the following advanced properties.

### [`style`](https://nextjs.org/docs/app/api-reference/components/image#style)

Allows passing CSS styles to the underlying image element.

```
<span><span>const</span><span> </span><span>imageStyle</span><span> </span><span>=</span><span> {</span></span>
<span><span>  borderRadius</span><span>:</span><span> </span><span>'50%'</span><span>,</span></span>
<span><span>  border</span><span>:</span><span> </span><span>'1px solid #fff'</span><span>,</span></span>
<span><span>}</span></span>
<span> </span>
<span><span>export</span><span> </span><span>default</span><span> </span><span>function</span><span> </span><span>ProfileImage</span><span>() {</span></span>
<span><span>  </span><span>return</span><span> &lt;</span><span>Image</span><span> </span><span>src</span><span>=</span><span>"..."</span><span> </span><span>style</span><span>=</span><span>{imageStyle} /&gt;</span></span>
<span><span>}</span></span>
```

Remember that the required width and height props can interact with your styling. If you use styling to modify an image's width, you should also style its height to `auto` to preserve its intrinsic aspect ratio, or your image will be distorted.

### [`onLoadingComplete`](https://nextjs.org/docs/app/api-reference/components/image#onloadingcomplete)

```
<span><span>'use client'</span></span>
<span> </span>
<span><span>&lt;</span><span>Image</span><span> </span><span>onLoadingComplete</span><span>=</span><span>{(img) </span><span>=&gt;</span><span> </span><span>console</span><span>.log</span><span>(</span><span>img</span><span>.naturalWidth)} /&gt;</span></span>
```

> **Warning**: Deprecated since Next.js 14 in favor of [`onLoad`](https://nextjs.org/docs/app/api-reference/components/image#onload).

A callback function that is invoked once the image is completely loaded and the [placeholder](https://nextjs.org/docs/app/api-reference/components/image#placeholder) has been removed.

The callback function will be called with one argument, a reference to the underlying `<img>` element.

> **Good to know**: Using props like `onLoadingComplete`, which accept a function, requires using [Client Components](https://nextjs.org/docs/app/building-your-application/rendering/client-components) to serialize the provided function.

### [`onLoad`](https://nextjs.org/docs/app/api-reference/components/image#onload)

```
<span><span>&lt;</span><span>Image</span><span> </span><span>onLoad</span><span>=</span><span>{(e) </span><span>=&gt;</span><span> </span><span>console</span><span>.log</span><span>(</span><span>e</span><span>.</span><span>target</span><span>.naturalWidth)} /&gt;</span></span>
```

A callback function that is invoked once the image is completely loaded and the [placeholder](https://nextjs.org/docs/app/api-reference/components/image#placeholder) has been removed.

The callback function will be called with one argument, the Event which has a `target` that references the underlying `<img>` element.

> **Good to know**: Using props like `onLoad`, which accept a function, requires using [Client Components](https://nextjs.org/docs/app/building-your-application/rendering/client-components) to serialize the provided function.

### [`onError`](https://nextjs.org/docs/app/api-reference/components/image#onerror)

```
<span><span>&lt;</span><span>Image</span><span> </span><span>onError</span><span>=</span><span>{(e) </span><span>=&gt;</span><span> </span><span>console</span><span>.error</span><span>(</span><span>e</span><span>.</span><span>target</span><span>.id)} /&gt;</span></span>
```

A callback function that is invoked if the image fails to load.

> **Good to know**: Using props like `onError`, which accept a function, requires using [Client Components](https://nextjs.org/docs/app/building-your-application/rendering/client-components) to serialize the provided function.

### [`loading`](https://nextjs.org/docs/app/api-reference/components/image#loading)

```
<span><span>loading </span><span>=</span><span> </span><span>'lazy'</span><span> </span><span>// {lazy} | {eager}</span></span>
```

The loading behavior of the image. Defaults to `lazy`.

When `lazy`, defer loading the image until it reaches a calculated distance from the viewport.

When `eager`, load the image immediately.

Learn more about the [`loading` attribute](https://developer.mozilla.org/docs/Web/HTML/Element/img#loading).

### [`blurDataURL`](https://nextjs.org/docs/app/api-reference/components/image#blurdataurl)

A [Data URL](https://developer.mozilla.org/docs/Web/HTTP/Basics_of_HTTP/Data_URIs) to be used as a placeholder image before the `src` image successfully loads. Only takes effect when combined with [`placeholder="blur"`](https://nextjs.org/docs/app/api-reference/components/image#placeholder).

Must be a base64-encoded image. It will be enlarged and blurred, so a very small image (10px or less) is recommended. Including larger images as placeholders may harm your application performance.

Try it out:

-   [Demo the default `blurDataURL` prop](https://image-component.nextjs.gallery/placeholder)
-   [Demo the color effect with `blurDataURL` prop](https://image-component.nextjs.gallery/color)

You can also [generate a solid color Data URL](https://png-pixel.com/) to match the image.

### [`unoptimized`](https://nextjs.org/docs/app/api-reference/components/image#unoptimized)

```
<span><span>unoptimized </span><span>=</span><span> {false} </span><span>// {false} | {true}</span></span>
```

When true, the source image will be served as-is from the `src` instead of changing quality, size, or format. Defaults to `false`.

This is useful for images that do not benefit from optimization such as small images (less than 1KB), vector images (SVG), or animated images (GIF).

```
<span><span>import</span><span> Image </span><span>from</span><span> </span><span>'next/image'</span></span>
<span> </span>
<span><span>const</span><span> </span><span>UnoptimizedImage</span><span> </span><span>=</span><span> (props) </span><span>=&gt;</span><span> {</span></span>
<span><span>  </span><span>return</span><span> &lt;</span><span>Image</span><span> {</span><span>...</span><span>props} </span><span>unoptimized</span><span> /&gt;</span></span>
<span><span>}</span></span>
```

Since Next.js 12.3.0, this prop can be assigned to all images by updating `next.config.js` with the following configuration:

```
<span><span>module</span><span>.</span><span>exports</span><span> </span><span>=</span><span> {</span></span>
<span><span>  images</span><span>:</span><span> {</span></span>
<span><span>    unoptimized</span><span>:</span><span> </span><span>true</span><span>,</span></span>
<span><span>  }</span><span>,</span></span>
<span><span>}</span></span>
```

### [`overrideSrc`](https://nextjs.org/docs/app/api-reference/components/image#overridesrc)

When providing the `src` prop to the `<Image>` component, both the `srcset` and `src` attributes are generated automatically for the resulting `<img>`.

```
<span><span>&lt;</span><span>img</span></span>
<span><span>  </span><span>srcset</span><span>=</span><span>"</span></span>
<span><span>    /_next/image?url=%2Fme.jpg&amp;w=640&amp;q=75 1x,</span></span>
<span><span>    /_next/image?url=%2Fme.jpg&amp;w=828&amp;q=75 2x</span></span>
<span><span>  "</span></span>
<span><span>  </span><span>src</span><span>=</span><span>"/_next/image?url=%2Fme.jpg&amp;w=828&amp;q=75"</span></span>
<span><span>/&gt;</span></span>
```

In some cases, it is not desirable to have the `src` attribute generated and you may wish to override it using the `overrideSrc` prop.

For example, when upgrading an existing website from `<img>` to `<Image>`, you may wish to maintain the same `src` attribute for SEO purposes such as image ranking or avoiding recrawl.

```
<span><span>&lt;</span><span>Image</span><span> </span><span>src</span><span>=</span><span>"/me.jpg"</span><span> </span><span>overrideSrc</span><span>=</span><span>"/override.jpg"</span><span> /&gt;</span></span>
```

```
<span><span>&lt;</span><span>img</span></span>
<span><span>  </span><span>srcset</span><span>=</span><span>"</span></span>
<span><span>    /_next/image?url=%2Fme.jpg&amp;w=640&amp;q=75 1x,</span></span>
<span><span>    /_next/image?url=%2Fme.jpg&amp;w=828&amp;q=75 2x</span></span>
<span><span>  "</span></span>
<span><span>  </span><span>src</span><span>=</span><span>"/override.jpg"</span></span>
<span><span>/&gt;</span></span>
```

### [decoding](https://nextjs.org/docs/app/api-reference/components/image#decoding)

A hint to the browser indicating if it should wait for the image to be decoded before presenting other content updates or not. Defaults to `async`.

Possible values are the following:

-   `async` - Asynchronously decode the image and allow other content to be rendered before it completes.
-   `sync` - Synchronously decode the image for atomic presentation with other content.
-   `auto` - No preference for the decoding mode; the browser decides what's best.

Learn more about the [`decoding` attribute](https://developer.mozilla.org/docs/Web/HTML/Element/img#decoding).

### [Other Props](https://nextjs.org/docs/app/api-reference/components/image#other-props)

Other properties on the `<Image />` component will be passed to the underlying `img` element with the exception of the following:

-   `srcSet`. Use [Device Sizes](https://nextjs.org/docs/app/api-reference/components/image#devicesizes) instead.

## [Configuration Options](https://nextjs.org/docs/app/api-reference/components/image#configuration-options)

In addition to props, you can configure the Image Component in `next.config.js`. The following options are available:

### [`localPatterns`](https://nextjs.org/docs/app/api-reference/components/image#localpatterns)

You can optionally configure `localPatterns` in your `next.config.js` file in order to allow specific paths to be optimized and block all others paths.

```
<span><span>module</span><span>.</span><span>exports</span><span> </span><span>=</span><span> {</span></span>
<span><span>  images</span><span>:</span><span> {</span></span>
<span><span>    localPatterns</span><span>:</span><span> [</span></span>
<span><span>      {</span></span>
<span><span>        pathname</span><span>:</span><span> </span><span>'/assets/images/**'</span><span>,</span></span>
<span><span>        search</span><span>:</span><span> </span><span>''</span><span>,</span></span>
<span><span>      }</span><span>,</span></span>
<span><span>    ]</span><span>,</span></span>
<span><span>  }</span><span>,</span></span>
<span><span>}</span></span>
```

> **Good to know**: The example above will ensure the `src` property of `next/image` must start with `/assets/images/` and must not have a query string. Attempting to optimize any other path will respond with 400 Bad Request.

### [`remotePatterns`](https://nextjs.org/docs/app/api-reference/components/image#remotepatterns)

To protect your application from malicious users, configuration is required in order to use external images. This ensures that only external images from your account can be served from the Next.js Image Optimization API. These external images can be configured with the `remotePatterns` property in your `next.config.js` file, as shown below:

```
<span><span>module</span><span>.</span><span>exports</span><span> </span><span>=</span><span> {</span></span>
<span><span>  images</span><span>:</span><span> {</span></span>
<span><span>    remotePatterns</span><span>:</span><span> [</span><span>new</span><span> </span><span>URL</span><span>(</span><span>'https://example.com/account123/**'</span><span>)]</span><span>,</span></span>
<span><span>  }</span><span>,</span></span>
<span><span>}</span></span>
```

Versions of Next.js prior to 15.3.0 can configure `remotePatterns` using the object:

```
<span><span>module</span><span>.</span><span>exports</span><span> </span><span>=</span><span> {</span></span>
<span><span>  images</span><span>:</span><span> {</span></span>
<span><span>    remotePatterns</span><span>:</span><span> [</span></span>
<span><span>      {</span></span>
<span><span>        protocol</span><span>:</span><span> </span><span>'https'</span><span>,</span></span>
<span><span>        hostname</span><span>:</span><span> </span><span>'example.com'</span><span>,</span></span>
<span><span>        port</span><span>:</span><span> </span><span>''</span><span>,</span></span>
<span><span>        pathname</span><span>:</span><span> </span><span>'/account123/**'</span><span>,</span></span>
<span><span>        search</span><span>:</span><span> </span><span>''</span><span>,</span></span>
<span><span>      }</span><span>,</span></span>
<span><span>    ]</span><span>,</span></span>
<span><span>  }</span><span>,</span></span>
<span><span>}</span></span>
```

> **Good to know**: The example above will ensure the `src` property of `next/image` must start with `https://example.com/account123/` and must not have a query string. Any other protocol, hostname, port, or unmatched path will respond with 400 Bad Request.

Below is an example of the `remotePatterns` property in the `next.config.js` file using a wildcard pattern in the `hostname`:

```
<span><span>module</span><span>.</span><span>exports</span><span> </span><span>=</span><span> {</span></span>
<span><span>  images</span><span>:</span><span> {</span></span>
<span><span>    remotePatterns</span><span>:</span><span> [</span></span>
<span><span>      {</span></span>
<span><span>        protocol</span><span>:</span><span> </span><span>'https'</span><span>,</span></span>
<span><span>        hostname</span><span>:</span><span> </span><span>'**.example.com'</span><span>,</span></span>
<span><span>        port</span><span>:</span><span> </span><span>''</span><span>,</span></span>
<span><span>        search</span><span>:</span><span> </span><span>''</span><span>,</span></span>
<span><span>      }</span><span>,</span></span>
<span><span>    ]</span><span>,</span></span>
<span><span>  }</span><span>,</span></span>
<span><span>}</span></span>
```

> **Good to know**: The example above will ensure the `src` property of `next/image` must start with `https://img1.example.com` or `https://me.avatar.example.com` or any number of subdomains. It cannot have a port or query string. Any other protocol or unmatched hostname will respond with 400 Bad Request.

Wildcard patterns can be used for both `pathname` and `hostname` and have the following syntax:

-   `*` match a single path segment or subdomain
-   `**` match any number of path segments at the end or subdomains at the beginning

The `**` syntax does not work in the middle of the pattern.

> **Good to know**: When omitting `protocol`, `port`, `pathname`, or `search` then the wildcard `**` is implied. This is not recommended because it may allow malicious actors to optimize urls you did not intend.

Below is an example of the `remotePatterns` property in the `next.config.js` file using `search`:

```
<span><span>module</span><span>.</span><span>exports</span><span> </span><span>=</span><span> {</span></span>
<span><span>  images</span><span>:</span><span> {</span></span>
<span><span>    remotePatterns</span><span>:</span><span> [</span></span>
<span><span>      {</span></span>
<span><span>        protocol</span><span>:</span><span> </span><span>'https'</span><span>,</span></span>
<span><span>        hostname</span><span>:</span><span> </span><span>'assets.example.com'</span><span>,</span></span>
<span><span>        search</span><span>:</span><span> </span><span>'?v=1727111025337'</span><span>,</span></span>
<span><span>      }</span><span>,</span></span>
<span><span>    ]</span><span>,</span></span>
<span><span>  }</span><span>,</span></span>
<span><span>}</span></span>
```

> **Good to know**: The example above will ensure the `src` property of `next/image` must start with `https://assets.example.com` and must have the exact query string `?v=1727111025337`. Any other protocol or query string will respond with 400 Bad Request.

### [`domains`](https://nextjs.org/docs/app/api-reference/components/image#domains)

> **Warning**: Deprecated since Next.js 14 in favor of strict [`remotePatterns`](https://nextjs.org/docs/app/api-reference/components/image#remotepatterns) in order to protect your application from malicious users. Only use `domains` if you own all the content served from the domain.

Similar to [`remotePatterns`](https://nextjs.org/docs/app/api-reference/components/image#remotepatterns), the `domains` configuration can be used to provide a list of allowed hostnames for external images.

However, the `domains` configuration does not support wildcard pattern matching and it cannot restrict protocol, port, or pathname.

Below is an example of the `domains` property in the `next.config.js` file:

```
<span><span>module</span><span>.</span><span>exports</span><span> </span><span>=</span><span> {</span></span>
<span><span>  images</span><span>:</span><span> {</span></span>
<span><span>    domains</span><span>:</span><span> [</span><span>'assets.acme.com'</span><span>]</span><span>,</span></span>
<span><span>  }</span><span>,</span></span>
<span><span>}</span></span>
```

### [`loaderFile`](https://nextjs.org/docs/app/api-reference/components/image#loaderfile)

If you want to use a cloud provider to optimize images instead of using the Next.js built-in Image Optimization API, you can configure the `loaderFile` in your `next.config.js` like the following:

```
<span><span>module</span><span>.</span><span>exports</span><span> </span><span>=</span><span> {</span></span>
<span><span>  images</span><span>:</span><span> {</span></span>
<span><span>    loader</span><span>:</span><span> </span><span>'custom'</span><span>,</span></span>
<span><span>    loaderFile</span><span>:</span><span> </span><span>'./my/image/loader.js'</span><span>,</span></span>
<span><span>  }</span><span>,</span></span>
<span><span>}</span></span>
```

This must point to a file relative to the root of your Next.js application. The file must export a default function that returns a string, for example:

```
<span><span>'use client'</span></span>
<span> </span>
<span><span>export</span><span> </span><span>default</span><span> </span><span>function</span><span> </span><span>myImageLoader</span><span>({ src</span><span>,</span><span> width</span><span>,</span><span> quality }) {</span></span>
<span><span>  </span><span>return</span><span> </span><span>`https://example.com/</span><span>${</span><span>src</span><span>}</span><span>?w=</span><span>${</span><span>width</span><span>}</span><span>&amp;q=</span><span>${</span><span>quality </span><span>||</span><span> </span><span>75</span><span>}</span><span>`</span></span>
<span><span>}</span></span>
```

Alternatively, you can use the [`loader` prop](https://nextjs.org/docs/app/api-reference/components/image#loader) to configure each instance of `next/image`.

Examples:

-   [Custom Image Loader Configuration](https://nextjs.org/docs/app/api-reference/config/next-config-js/images#example-loader-configuration)

> **Good to know**: Customizing the image loader file, which accepts a function, requires using [Client Components](https://nextjs.org/docs/app/building-your-application/rendering/client-components) to serialize the provided function.

## [Advanced](https://nextjs.org/docs/app/api-reference/components/image#advanced)

The following configuration is for advanced use cases and is usually not necessary. If you choose to configure the properties below, you will override any changes to the Next.js defaults in future updates.

### [`deviceSizes`](https://nextjs.org/docs/app/api-reference/components/image#devicesizes)

If you know the expected device widths of your users, you can specify a list of device width breakpoints using the `deviceSizes` property in `next.config.js`. These widths are used when the `next/image` component uses [`sizes`](https://nextjs.org/docs/app/api-reference/components/image#sizes) prop to ensure the correct image is served for user's device.

If no configuration is provided, the default below is used.

```
<span><span>module</span><span>.</span><span>exports</span><span> </span><span>=</span><span> {</span></span>
<span><span>  images</span><span>:</span><span> {</span></span>
<span><span>    deviceSizes</span><span>:</span><span> [</span><span>640</span><span>,</span><span> </span><span>750</span><span>,</span><span> </span><span>828</span><span>,</span><span> </span><span>1080</span><span>,</span><span> </span><span>1200</span><span>,</span><span> </span><span>1920</span><span>,</span><span> </span><span>2048</span><span>,</span><span> </span><span>3840</span><span>]</span><span>,</span></span>
<span><span>  }</span><span>,</span></span>
<span><span>}</span></span>
```

### [`imageSizes`](https://nextjs.org/docs/app/api-reference/components/image#imagesizes)

You can specify a list of image widths using the `images.imageSizes` property in your `next.config.js` file. These widths are concatenated with the array of [device sizes](https://nextjs.org/docs/app/api-reference/components/image#devicesizes) to form the full array of sizes used to generate image [srcset](https://developer.mozilla.org/docs/Web/API/HTMLImageElement/srcset)s.

The reason there are two separate lists is that imageSizes is only used for images which provide a [`sizes`](https://nextjs.org/docs/app/api-reference/components/image#sizes) prop, which indicates that the image is less than the full width of the screen. **Therefore, the sizes in imageSizes should all be smaller than the smallest size in deviceSizes.**

If no configuration is provided, the default below is used.

```
<span><span>module</span><span>.</span><span>exports</span><span> </span><span>=</span><span> {</span></span>
<span><span>  images</span><span>:</span><span> {</span></span>
<span><span>    imageSizes</span><span>:</span><span> [</span><span>16</span><span>,</span><span> </span><span>32</span><span>,</span><span> </span><span>48</span><span>,</span><span> </span><span>64</span><span>,</span><span> </span><span>96</span><span>,</span><span> </span><span>128</span><span>,</span><span> </span><span>256</span><span>,</span><span> </span><span>384</span><span>]</span><span>,</span></span>
<span><span>  }</span><span>,</span></span>
<span><span>}</span></span>
```

### [`qualities`](https://nextjs.org/docs/app/api-reference/components/image#qualities)

The default [Image Optimization API](https://nextjs.org/docs/app/api-reference/components/image#loader) will automatically allow all qualities from 1 to 100. If you wish to restrict the allowed qualities, you can add configuration to `next.config.js`.

```
<span><span>module</span><span>.</span><span>exports</span><span> </span><span>=</span><span> {</span></span>
<span><span>  images</span><span>:</span><span> {</span></span>
<span><span>    qualities</span><span>:</span><span> [</span><span>25</span><span>,</span><span> </span><span>50</span><span>,</span><span> </span><span>75</span><span>]</span><span>,</span></span>
<span><span>  }</span><span>,</span></span>
<span><span>}</span></span>
```

In this example above, only three qualities are allowed: 25, 50, and 75. If the [`quality`](https://nextjs.org/docs/app/api-reference/components/image#quality) prop does not match a value in this array, the image will fail with 400 Bad Request.

### [`formats`](https://nextjs.org/docs/app/api-reference/components/image#formats)

The default [Image Optimization API](https://nextjs.org/docs/app/api-reference/components/image#loader) will automatically detect the browser's supported image formats via the request's `Accept` header in order to determine the best output format.

If the `Accept` header matches more than one of the configured formats, the first match in the array is used. Therefore, the array order matters. If there is no match (or the source image is [animated](https://nextjs.org/docs/app/api-reference/components/image#animated-images)), the Image Optimization API will fallback to the original image's format.

If no configuration is provided, the default below is used.

```
<span><span>module</span><span>.</span><span>exports</span><span> </span><span>=</span><span> {</span></span>
<span><span>  images</span><span>:</span><span> {</span></span>
<span><span>    formats</span><span>:</span><span> [</span><span>'image/webp'</span><span>]</span><span>,</span></span>
<span><span>  }</span><span>,</span></span>
<span><span>}</span></span>
```

You can enable AVIF support, which will fallback to the original format of the src image if the browser [does not support AVIF](https://caniuse.com/avif):

```
<span><span>module</span><span>.</span><span>exports</span><span> </span><span>=</span><span> {</span></span>
<span><span>  images</span><span>:</span><span> {</span></span>
<span><span>    formats</span><span>:</span><span> [</span><span>'image/avif'</span><span>]</span><span>,</span></span>
<span><span>  }</span><span>,</span></span>
<span><span>}</span></span>
```

> **Good to know**:
> 
> -   We still recommend using WebP for most use cases.
> -   AVIF generally takes 50% longer to encode but it compresses 20% smaller compared to WebP. This means that the first time an image is requested, it will typically be slower and then subsequent requests that are cached will be faster.
> -   If you self-host with a Proxy/CDN in front of Next.js, you must configure the Proxy to forward the `Accept` header.

## [Caching Behavior](https://nextjs.org/docs/app/api-reference/components/image#caching-behavior)

The following describes the caching algorithm for the default [loader](https://nextjs.org/docs/app/api-reference/components/image#loader). For all other loaders, please refer to your cloud provider's documentation.

Images are optimized dynamically upon request and stored in the `<distDir>/cache/images` directory. The optimized image file will be served for subsequent requests until the expiration is reached. When a request is made that matches a cached but expired file, the expired image is served stale immediately. Then the image is optimized again in the background (also called revalidation) and saved to the cache with the new expiration date.

The cache status of an image can be determined by reading the value of the `x-nextjs-cache` response header. The possible values are the following:

-   `MISS` - the path is not in the cache (occurs at most once, on the first visit)
-   `STALE` - the path is in the cache but exceeded the revalidate time so it will be updated in the background
-   `HIT` - the path is in the cache and has not exceeded the revalidate time

The expiration (or rather Max Age) is defined by either the [`minimumCacheTTL`](https://nextjs.org/docs/app/api-reference/components/image#minimumcachettl) configuration or the upstream image `Cache-Control` header, whichever is larger. Specifically, the `max-age` value of the `Cache-Control` header is used. If both `s-maxage` and `max-age` are found, then `s-maxage` is preferred. The `max-age` is also passed-through to any downstream clients including CDNs and browsers.

-   You can configure [`minimumCacheTTL`](https://nextjs.org/docs/app/api-reference/components/image#minimumcachettl) to increase the cache duration when the upstream image does not include `Cache-Control` header or the value is very low.
-   You can configure [`deviceSizes`](https://nextjs.org/docs/app/api-reference/components/image#devicesizes) and [`imageSizes`](https://nextjs.org/docs/app/api-reference/components/image#imagesizes) to reduce the total number of possible generated images.
-   You can configure [formats](https://nextjs.org/docs/app/api-reference/components/image#formats) to disable multiple formats in favor of a single image format.

### [`minimumCacheTTL`](https://nextjs.org/docs/app/api-reference/components/image#minimumcachettl)

You can configure the Time to Live (TTL) in seconds for cached optimized images. In many cases, it's better to use a [Static Image Import](https://nextjs.org/docs/app/building-your-application/optimizing/images#local-images) which will automatically hash the file contents and cache the image forever with a `Cache-Control` header of `immutable`.

If no configuration is provided, the default below is used.

```
<span><span>module</span><span>.</span><span>exports</span><span> </span><span>=</span><span> {</span></span>
<span><span>  images</span><span>:</span><span> {</span></span>
<span><span>    minimumCacheTTL</span><span>:</span><span> </span><span>60</span><span>,</span><span> </span><span>// 1 minute</span></span>
<span><span>  }</span><span>,</span></span>
<span><span>}</span></span>
```

You can increase the TTL to reduce the number of revalidations and potentionally lower cost:

```
<span><span>module</span><span>.</span><span>exports</span><span> </span><span>=</span><span> {</span></span>
<span><span>  images</span><span>:</span><span> {</span></span>
<span><span>    minimumCacheTTL</span><span>:</span><span> </span><span>2678400</span><span>,</span><span> </span><span>// 31 days</span></span>
<span><span>  }</span><span>,</span></span>
<span><span>}</span></span>
```

The expiration (or rather Max Age) of the optimized image is defined by either the `minimumCacheTTL` or the upstream image `Cache-Control` header, whichever is larger.

If you need to change the caching behavior per image, you can configure [`headers`](https://nextjs.org/docs/app/api-reference/config/next-config-js/headers) to set the `Cache-Control` header on the upstream image (e.g. `/some-asset.jpg`, not `/_next/image` itself).

There is no mechanism to invalidate the cache at this time, so its best to keep `minimumCacheTTL` low. Otherwise you may need to manually change the [`src`](https://nextjs.org/docs/app/api-reference/components/image#src) prop or delete `<distDir>/cache/images`.

### [`disableStaticImages`](https://nextjs.org/docs/app/api-reference/components/image#disablestaticimages)

The default behavior allows you to import static files such as `import icon from './icon.png'` and then pass that to the `src` property.

In some cases, you may wish to disable this feature if it conflicts with other plugins that expect the import to behave differently.

You can disable static image imports inside your `next.config.js`:

```
<span><span>module</span><span>.</span><span>exports</span><span> </span><span>=</span><span> {</span></span>
<span><span>  images</span><span>:</span><span> {</span></span>
<span><span>    disableStaticImages</span><span>:</span><span> </span><span>true</span><span>,</span></span>
<span><span>  }</span><span>,</span></span>
<span><span>}</span></span>
```

### [`dangerouslyAllowSVG`](https://nextjs.org/docs/app/api-reference/components/image#dangerouslyallowsvg)

The default [loader](https://nextjs.org/docs/app/api-reference/components/image#loader) does not optimize SVG images for a few reasons. First, SVG is a vector format meaning it can be resized losslessly. Second, SVG has many of the same features as HTML/CSS, which can lead to vulnerabilities without proper [Content Security Policy (CSP) headers](https://nextjs.org/docs/app/api-reference/config/next-config-js/headers#content-security-policy).

Therefore, we recommended using the [`unoptimized`](https://nextjs.org/docs/app/api-reference/components/image#unoptimized) prop when the [`src`](https://nextjs.org/docs/app/api-reference/components/image#src) prop is known to be SVG. This happens automatically when `src` ends with `".svg"`.

However, if you need to serve SVG images with the default Image Optimization API, you can set `dangerouslyAllowSVG` inside your `next.config.js`:

```
<span><span>module</span><span>.</span><span>exports</span><span> </span><span>=</span><span> {</span></span>
<span><span>  images</span><span>:</span><span> {</span></span>
<span><span>    dangerouslyAllowSVG</span><span>:</span><span> </span><span>true</span><span>,</span></span>
<span><span>    contentDispositionType</span><span>:</span><span> </span><span>'attachment'</span><span>,</span></span>
<span><span>    contentSecurityPolicy</span><span>:</span><span> </span><span>"default-src 'self'; script-src 'none'; sandbox;"</span><span>,</span></span>
<span><span>  }</span><span>,</span></span>
<span><span>}</span></span>
```

In addition, it is strongly recommended to also set `contentDispositionType` to force the browser to download the image, as well as `contentSecurityPolicy` to prevent scripts embedded in the image from executing.

### [`contentDispositionType`](https://nextjs.org/docs/app/api-reference/components/image#contentdispositiontype)

The default [loader](https://nextjs.org/docs/app/api-reference/components/image#loader) sets the [`Content-Disposition`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Disposition#as_a_response_header_for_the_main_body) header to `attachment` for added protection since the API can serve arbitrary remote images.

The default value is `attachment` which forces the browser to download the image when visiting directly. This is particularly important when [`dangerouslyAllowSVG`](https://nextjs.org/docs/app/api-reference/components/image#dangerouslyallowsvg) is true.

You can optionally configure `inline` to allow the browser to render the image when visiting directly, without downloading it.

```
<span><span>module</span><span>.</span><span>exports</span><span> </span><span>=</span><span> {</span></span>
<span><span>  images</span><span>:</span><span> {</span></span>
<span><span>    contentDispositionType</span><span>:</span><span> </span><span>'inline'</span><span>,</span></span>
<span><span>  }</span><span>,</span></span>
<span><span>}</span></span>
```

## [Animated Images](https://nextjs.org/docs/app/api-reference/components/image#animated-images)

The default [loader](https://nextjs.org/docs/app/api-reference/components/image#loader) will automatically bypass Image Optimization for animated images and serve the image as-is.

Auto-detection for animated files is best-effort and supports GIF, APNG, and WebP. If you want to explicitly bypass Image Optimization for a given animated image, use the [unoptimized](https://nextjs.org/docs/app/api-reference/components/image#unoptimized) prop.

## [Responsive Images](https://nextjs.org/docs/app/api-reference/components/image#responsive-images)

The default generated `srcset` contains `1x` and `2x` images in order to support different device pixel ratios. However, you may wish to render a responsive image that stretches with the viewport. In that case, you'll need to set [`sizes`](https://nextjs.org/docs/app/api-reference/components/image#sizes) as well as `style` (or `className`).

You can render a responsive image using one of the following methods below.

### [Responsive image using a static import](https://nextjs.org/docs/app/api-reference/components/image#responsive-image-using-a-static-import)

If the source image is not dynamic, you can statically import to create a responsive image:

```
<span><span>import</span><span> Image </span><span>from</span><span> </span><span>'next/image'</span></span>
<span><span>import</span><span> me </span><span>from</span><span> </span><span>'../photos/me.jpg'</span></span>
<span> </span>
<span><span>export</span><span> </span><span>default</span><span> </span><span>function</span><span> </span><span>Author</span><span>() {</span></span>
<span><span>  </span><span>return</span><span> (</span></span>
<span><span>    &lt;</span><span>Image</span></span>
<span><span>      </span><span>src</span><span>=</span><span>{me}</span></span>
<span><span>      </span><span>alt</span><span>=</span><span>"Picture of the author"</span></span>
<span><span>      </span><span>sizes</span><span>=</span><span>"100vw"</span></span>
<span><span>      </span><span>style</span><span>=</span><span>{{</span></span>
<span><span>        width</span><span>:</span><span> </span><span>'100%'</span><span>,</span></span>
<span><span>        height</span><span>:</span><span> </span><span>'auto'</span><span>,</span></span>
<span><span>      }}</span></span>
<span><span>    /&gt;</span></span>
<span><span>  )</span></span>
<span><span>}</span></span>
```

Try it out:

-   [Demo the image responsive to viewport](https://image-component.nextjs.gallery/responsive)

### [Responsive image with aspect ratio](https://nextjs.org/docs/app/api-reference/components/image#responsive-image-with-aspect-ratio)

If the source image is a dynamic or a remote url, you will also need to provide `width` and `height` to set the correct aspect ratio of the responsive image:

```
<span><span>import</span><span> Image </span><span>from</span><span> </span><span>'next/image'</span></span>
<span> </span>
<span><span>export</span><span> </span><span>default</span><span> </span><span>function</span><span> </span><span>Page</span><span>({ photoUrl }) {</span></span>
<span><span>  </span><span>return</span><span> (</span></span>
<span><span>    &lt;</span><span>Image</span></span>
<span><span>      </span><span>src</span><span>=</span><span>{photoUrl}</span></span>
<span><span>      </span><span>alt</span><span>=</span><span>"Picture of the author"</span></span>
<span><span>      </span><span>sizes</span><span>=</span><span>"100vw"</span></span>
<span><span>      </span><span>style</span><span>=</span><span>{{</span></span>
<span><span>        width</span><span>:</span><span> </span><span>'100%'</span><span>,</span></span>
<span><span>        height</span><span>:</span><span> </span><span>'auto'</span><span>,</span></span>
<span><span>      }}</span></span>
<span><span>      </span><span>width</span><span>=</span><span>{</span><span>500</span><span>}</span></span>
<span><span>      </span><span>height</span><span>=</span><span>{</span><span>300</span><span>}</span></span>
<span><span>    /&gt;</span></span>
<span><span>  )</span></span>
<span><span>}</span></span>
```

Try it out:

-   [Demo the image responsive to viewport](https://image-component.nextjs.gallery/responsive)

### [Responsive image with `fill`](https://nextjs.org/docs/app/api-reference/components/image#responsive-image-with-fill)

If you don't know the aspect ratio, you will need to set the [`fill`](https://nextjs.org/docs/app/api-reference/components/image#fill) prop and set `position: relative` on the parent. Optionally, you can set `object-fit` style depending on the desired stretch vs crop behavior:

```
<span><span>import</span><span> Image </span><span>from</span><span> </span><span>'next/image'</span></span>
<span> </span>
<span><span>export</span><span> </span><span>default</span><span> </span><span>function</span><span> </span><span>Page</span><span>({ photoUrl }) {</span></span>
<span><span>  </span><span>return</span><span> (</span></span>
<span><span>    &lt;</span><span>div</span><span> </span><span>style</span><span>=</span><span>{{ position</span><span>:</span><span> </span><span>'relative'</span><span>,</span><span> width</span><span>:</span><span> </span><span>'300px'</span><span>,</span><span> height</span><span>:</span><span> </span><span>'500px'</span><span> }}&gt;</span></span>
<span><span>      &lt;</span><span>Image</span></span>
<span><span>        </span><span>src</span><span>=</span><span>{photoUrl}</span></span>
<span><span>        </span><span>alt</span><span>=</span><span>"Picture of the author"</span></span>
<span><span>        </span><span>sizes</span><span>=</span><span>"300px"</span></span>
<span><span>        </span><span>fill</span></span>
<span><span>        </span><span>style</span><span>=</span><span>{{</span></span>
<span><span>          objectFit</span><span>:</span><span> </span><span>'contain'</span><span>,</span></span>
<span><span>        }}</span></span>
<span><span>      /&gt;</span></span>
<span><span>    &lt;/</span><span>div</span><span>&gt;</span></span>
<span><span>  )</span></span>
<span><span>}</span></span>
```

Try it out:

-   [Demo the `fill` prop](https://image-component.nextjs.gallery/fill)

## [Theme Detection CSS](https://nextjs.org/docs/app/api-reference/components/image#theme-detection-css)

If you want to display a different image for light and dark mode, you can create a new component that wraps two `<Image>` components and reveals the correct one based on a CSS media query.

```
<span><span>.imgDark</span><span> {</span></span>
<span><span>  </span><span>display</span><span>:</span><span> </span><span>none</span><span>;</span></span>
<span><span>}</span></span>
<span> </span>
<span><span>@media</span><span> (prefers-color-scheme</span><span>:</span><span> dark) {</span></span>
<span><span>  </span><span>.imgLight</span><span> {</span></span>
<span><span>    </span><span>display</span><span>:</span><span> </span><span>none</span><span>;</span></span>
<span><span>  }</span></span>
<span><span>  </span><span>.imgDark</span><span> {</span></span>
<span><span>    </span><span>display</span><span>:</span><span> </span><span>unset</span><span>;</span></span>
<span><span>  }</span></span>
<span><span>}</span></span>
```

```
<span><span>import</span><span> styles </span><span>from</span><span> </span><span>'./theme-image.module.css'</span></span>
<span><span>import</span><span> Image</span><span>,</span><span> { ImageProps } </span><span>from</span><span> </span><span>'next/image'</span></span>
<span> </span>
<span><span>type</span><span> </span><span>Props</span><span> </span><span>=</span><span> </span><span>Omit</span><span>&lt;</span><span>ImageProps</span><span>,</span><span> </span><span>'src'</span><span> </span><span>|</span><span> </span><span>'priority'</span><span> </span><span>|</span><span> </span><span>'loading'</span><span>&gt; </span><span>&amp;</span><span> {</span></span>
<span><span>  srcLight</span><span>:</span><span> </span><span>string</span></span>
<span><span>  srcDark</span><span>:</span><span> </span><span>string</span></span>
<span><span>}</span></span>
<span> </span>
<span><span>const</span><span> </span><span>ThemeImage</span><span> </span><span>=</span><span> (props</span><span>:</span><span> </span><span>Props</span><span>) </span><span>=&gt;</span><span> {</span></span>
<span><span>  </span><span>const</span><span> { </span><span>srcLight</span><span>,</span><span> </span><span>srcDark</span><span>,</span><span> </span><span>...</span><span>rest</span><span> } </span><span>=</span><span> props</span></span>
<span> </span>
<span><span>  </span><span>return</span><span> (</span></span>
<span><span>    &lt;&gt;</span></span>
<span><span>      &lt;</span><span>Image</span><span> {</span><span>...</span><span>rest} </span><span>src</span><span>=</span><span>{srcLight} </span><span>className</span><span>=</span><span>{</span><span>styles</span><span>.imgLight} /&gt;</span></span>
<span><span>      &lt;</span><span>Image</span><span> {</span><span>...</span><span>rest} </span><span>src</span><span>=</span><span>{srcDark} </span><span>className</span><span>=</span><span>{</span><span>styles</span><span>.imgDark} /&gt;</span></span>
<span><span>    &lt;/&gt;</span></span>
<span><span>  )</span></span>
<span><span>}</span></span>
```

> **Good to know**: The default behavior of `loading="lazy"` ensures that only the correct image is loaded. You cannot use `priority` or `loading="eager"` because that would cause both images to load. Instead, you can use [`fetchPriority="high"`](https://developer.mozilla.org/docs/Web/API/HTMLImageElement/fetchPriority).

Try it out:

-   [Demo light/dark mode theme detection](https://image-component.nextjs.gallery/theme)

## [getImageProps](https://nextjs.org/docs/app/api-reference/components/image#getimageprops)

For more advanced use cases, you can call `getImageProps()` to get the props that would be passed to the underlying `<img>` element, and instead pass to them to another component, style, canvas, etc.

This also avoid calling React `useState()` so it can lead to better performance, but it cannot be used with the [`placeholder`](https://nextjs.org/docs/app/api-reference/components/image#placeholder) prop because the placeholder will never be removed.

### [Theme Detection Picture](https://nextjs.org/docs/app/api-reference/components/image#theme-detection-picture)

If you want to display a different image for light and dark mode, you can use the [`<picture>`](https://developer.mozilla.org/docs/Web/HTML/Element/picture) element to display a different image based on the user's [preferred color scheme](https://developer.mozilla.org/en-US/docs/Web/CSS/@media/prefers-color-scheme).

```
<span><span>import</span><span> { getImageProps } </span><span>from</span><span> </span><span>'next/image'</span></span>
<span> </span>
<span><span>export</span><span> </span><span>default</span><span> </span><span>function</span><span> </span><span>Page</span><span>() {</span></span>
<span><span>  </span><span>const</span><span> </span><span>common</span><span> </span><span>=</span><span> { alt</span><span>:</span><span> </span><span>'Theme Example'</span><span>,</span><span> width</span><span>:</span><span> </span><span>800</span><span>,</span><span> height</span><span>:</span><span> </span><span>400</span><span> }</span></span>
<span><span>  </span><span>const</span><span> {</span></span>
<span><span>    props: { srcSet: </span><span>dark</span><span> }</span><span>,</span></span>
<span><span>  } </span><span>=</span><span> </span><span>getImageProps</span><span>({ </span><span>...</span><span>common</span><span>,</span><span> src</span><span>:</span><span> </span><span>'/dark.png'</span><span> })</span></span>
<span><span>  </span><span>const</span><span> {</span></span>
<span><span>    props: { srcSet: </span><span>light</span><span>,</span><span> </span><span>...</span><span>rest</span><span> }</span><span>,</span></span>
<span><span>  } </span><span>=</span><span> </span><span>getImageProps</span><span>({ </span><span>...</span><span>common</span><span>,</span><span> src</span><span>:</span><span> </span><span>'/light.png'</span><span> })</span></span>
<span> </span>
<span><span>  </span><span>return</span><span> (</span></span>
<span><span>    &lt;</span><span>picture</span><span>&gt;</span></span>
<span><span>      &lt;</span><span>source</span><span> </span><span>media</span><span>=</span><span>"(prefers-color-scheme: dark)"</span><span> </span><span>srcSet</span><span>=</span><span>{dark} /&gt;</span></span>
<span><span>      &lt;</span><span>source</span><span> </span><span>media</span><span>=</span><span>"(prefers-color-scheme: light)"</span><span> </span><span>srcSet</span><span>=</span><span>{light} /&gt;</span></span>
<span><span>      &lt;</span><span>img</span><span> {</span><span>...</span><span>rest} /&gt;</span></span>
<span><span>    &lt;/</span><span>picture</span><span>&gt;</span></span>
<span><span>  )</span></span>
<span><span>}</span></span>
```

### [Art Direction](https://nextjs.org/docs/app/api-reference/components/image#art-direction)

If you want to display a different image for mobile and desktop, sometimes called [Art Direction](https://developer.mozilla.org/en-US/docs/Learn/HTML/Multimedia_and_embedding/Responsive_images#art_direction), you can provide different `src`, `width`, `height`, and `quality` props to `getImageProps()`.

```
<span><span>import</span><span> { getImageProps } </span><span>from</span><span> </span><span>'next/image'</span></span>
<span> </span>
<span><span>export</span><span> </span><span>default</span><span> </span><span>function</span><span> </span><span>Home</span><span>() {</span></span>
<span><span>  </span><span>const</span><span> </span><span>common</span><span> </span><span>=</span><span> { alt</span><span>:</span><span> </span><span>'Art Direction Example'</span><span>,</span><span> sizes</span><span>:</span><span> </span><span>'100vw'</span><span> }</span></span>
<span><span>  </span><span>const</span><span> {</span></span>
<span><span>    props: { srcSet: </span><span>desktop</span><span> }</span><span>,</span></span>
<span><span>  } </span><span>=</span><span> </span><span>getImageProps</span><span>({</span></span>
<span><span>    </span><span>...</span><span>common</span><span>,</span></span>
<span><span>    width</span><span>:</span><span> </span><span>1440</span><span>,</span></span>
<span><span>    height</span><span>:</span><span> </span><span>875</span><span>,</span></span>
<span><span>    quality</span><span>:</span><span> </span><span>80</span><span>,</span></span>
<span><span>    src</span><span>:</span><span> </span><span>'/desktop.jpg'</span><span>,</span></span>
<span><span>  })</span></span>
<span><span>  </span><span>const</span><span> {</span></span>
<span><span>    props: { srcSet: </span><span>mobile</span><span>,</span><span> </span><span>...</span><span>rest</span><span> }</span><span>,</span></span>
<span><span>  } </span><span>=</span><span> </span><span>getImageProps</span><span>({</span></span>
<span><span>    </span><span>...</span><span>common</span><span>,</span></span>
<span><span>    width</span><span>:</span><span> </span><span>750</span><span>,</span></span>
<span><span>    height</span><span>:</span><span> </span><span>1334</span><span>,</span></span>
<span><span>    quality</span><span>:</span><span> </span><span>70</span><span>,</span></span>
<span><span>    src</span><span>:</span><span> </span><span>'/mobile.jpg'</span><span>,</span></span>
<span><span>  })</span></span>
<span> </span>
<span><span>  </span><span>return</span><span> (</span></span>
<span><span>    &lt;</span><span>picture</span><span>&gt;</span></span>
<span><span>      &lt;</span><span>source</span><span> </span><span>media</span><span>=</span><span>"(min-width: 1000px)"</span><span> </span><span>srcSet</span><span>=</span><span>{desktop} /&gt;</span></span>
<span><span>      &lt;</span><span>source</span><span> </span><span>media</span><span>=</span><span>"(min-width: 500px)"</span><span> </span><span>srcSet</span><span>=</span><span>{mobile} /&gt;</span></span>
<span><span>      &lt;</span><span>img</span><span> {</span><span>...</span><span>rest} </span><span>style</span><span>=</span><span>{{ width</span><span>:</span><span> </span><span>'100%'</span><span>,</span><span> height</span><span>:</span><span> </span><span>'auto'</span><span> }} /&gt;</span></span>
<span><span>    &lt;/</span><span>picture</span><span>&gt;</span></span>
<span><span>  )</span></span>
<span><span>}</span></span>
```

### [Background CSS](https://nextjs.org/docs/app/api-reference/components/image#background-css)

You can even convert the `srcSet` string to the [`image-set()`](https://developer.mozilla.org/en-US/docs/Web/CSS/image/image-set) CSS function to optimize a background image.

```
<span><span>import</span><span> { getImageProps } </span><span>from</span><span> </span><span>'next/image'</span></span>
<span> </span>
<span><span>function</span><span> </span><span>getBackgroundImage</span><span>(srcSet </span><span>=</span><span> </span><span>''</span><span>) {</span></span>
<span><span>  </span><span>const</span><span> </span><span>imageSet</span><span> </span><span>=</span><span> srcSet</span></span>
<span><span>    </span><span>.split</span><span>(</span><span>', '</span><span>)</span></span>
<span><span>    </span><span>.map</span><span>((str) </span><span>=&gt;</span><span> {</span></span>
<span><span>      </span><span>const</span><span> [</span><span>url</span><span>,</span><span> </span><span>dpi</span><span>] </span><span>=</span><span> </span><span>str</span><span>.split</span><span>(</span><span>' '</span><span>)</span></span>
<span><span>      </span><span>return</span><span> </span><span>`url("</span><span>${</span><span>url</span><span>}</span><span>") </span><span>${</span><span>dpi</span><span>}</span><span>`</span></span>
<span><span>    })</span></span>
<span><span>    </span><span>.join</span><span>(</span><span>', '</span><span>)</span></span>
<span><span>  </span><span>return</span><span> </span><span>`image-set(</span><span>${</span><span>imageSet</span><span>}</span><span>)`</span></span>
<span><span>}</span></span>
<span> </span>
<span><span>export</span><span> </span><span>default</span><span> </span><span>function</span><span> </span><span>Home</span><span>() {</span></span>
<span><span>  </span><span>const</span><span> {</span></span>
<span><span>    props: { </span><span>srcSet</span><span> }</span><span>,</span></span>
<span><span>  } </span><span>=</span><span> </span><span>getImageProps</span><span>({ alt</span><span>:</span><span> </span><span>''</span><span>,</span><span> width</span><span>:</span><span> </span><span>128</span><span>,</span><span> height</span><span>:</span><span> </span><span>128</span><span>,</span><span> src</span><span>:</span><span> </span><span>'/img.png'</span><span> })</span></span>
<span><span>  </span><span>const</span><span> </span><span>backgroundImage</span><span> </span><span>=</span><span> </span><span>getBackgroundImage</span><span>(srcSet)</span></span>
<span><span>  </span><span>const</span><span> </span><span>style</span><span> </span><span>=</span><span> { height</span><span>:</span><span> </span><span>'100vh'</span><span>,</span><span> width</span><span>:</span><span> </span><span>'100vw'</span><span>,</span><span> backgroundImage }</span></span>
<span> </span>
<span><span>  </span><span>return</span><span> (</span></span>
<span><span>    &lt;</span><span>main</span><span> </span><span>style</span><span>=</span><span>{style}&gt;</span></span>
<span><span>      &lt;</span><span>h1</span><span>&gt;Hello World&lt;/</span><span>h1</span><span>&gt;</span></span>
<span><span>    &lt;/</span><span>main</span><span>&gt;</span></span>
<span><span>  )</span></span>
<span><span>}</span></span>
```

## [Known Browser Bugs](https://nextjs.org/docs/app/api-reference/components/image#known-browser-bugs)

This `next/image` component uses browser native [lazy loading](https://caniuse.com/loading-lazy-attr), which may fallback to eager loading for older browsers before Safari 15.4. When using the blur-up placeholder, older browsers before Safari 12 will fallback to empty placeholder. When using styles with `width`/`height` of `auto`, it is possible to cause [Layout Shift](https://web.dev/cls/) on older browsers before Safari 15 that don't [preserve the aspect ratio](https://caniuse.com/mdn-html_elements_img_aspect_ratio_computed_from_attributes). For more details, see [this MDN video](https://www.youtube.com/watch?v=4-d_SoCHeWE).

-   [Safari 15 - 16.3](https://bugs.webkit.org/show_bug.cgi?id=243601) display a gray border while loading. Safari 16.4 [fixed this issue](https://webkit.org/blog/13966/webkit-features-in-safari-16-4/#:~:text=Now%20in%20Safari%2016.4%2C%20a%20gray%20line%20no%20longer%20appears%20to%20mark%20the%20space%20where%20a%20lazy%2Dloaded%20image%20will%20appear%20once%20it%E2%80%99s%20been%20loaded.). Possible solutions:
    -   Use CSS `@supports (font: -apple-system-body) and (-webkit-appearance: none) { img[loading="lazy"] { clip-path: inset(0.6px) } }`
    -   Use [`priority`](https://nextjs.org/docs/app/api-reference/components/image#priority) if the image is above the fold
-   [Firefox 67+](https://bugzilla.mozilla.org/show_bug.cgi?id=1556156) displays a white background while loading. Possible solutions:
    -   Enable [AVIF `formats`](https://nextjs.org/docs/app/api-reference/components/image#formats)
    -   Use [`placeholder`](https://nextjs.org/docs/app/api-reference/components/image#placeholder)

## [Version History](https://nextjs.org/docs/app/api-reference/components/image#version-history)

| Version | Changes |
| --- | --- |
| `v15.3.0` | `remotePatterns` added support for array of `URL` objects. |
| `v15.0.0` | `contentDispositionType` configuration default changed to `attachment`. |
| `v14.2.23` | `qualities` configuration added. |
| `v14.2.15` | `decoding` prop added and `localPatterns` configuration added. |
| `v14.2.14` | `remotePatterns.search` prop added. |
| `v14.2.0` | `overrideSrc` prop added. |
| `v14.1.0` | `getImageProps()` is stable. |
| `v14.0.0` | `onLoadingComplete` prop and `domains` config deprecated. |
| `v13.4.14` | `placeholder` prop support for `data:/image...` |
| `v13.2.0` | `contentDispositionType` configuration added. |
| `v13.0.6` | `ref` prop added. |
| `v13.0.0` | The `next/image` import was renamed to `next/legacy/image`. The `next/future/image` import was renamed to `next/image`. A [codemod is available](https://nextjs.org/docs/app/guides/upgrading/codemods#next-image-to-legacy-image) to safely and automatically rename your imports. `<span>` wrapper removed. `layout`, `objectFit`, `objectPosition`, `lazyBoundary`, `lazyRoot` props removed. `alt` is required. `onLoadingComplete` receives reference to `img` element. Built-in loader config removed. |
| `v12.3.0` | `remotePatterns` and `unoptimized` configuration is stable. |
| `v12.2.0` | Experimental `remotePatterns` and experimental `unoptimized` configuration added. `layout="raw"` removed. |
| `v12.1.1` | `style` prop added. Experimental support for `layout="raw"` added. |
| `v12.1.0` | `dangerouslyAllowSVG` and `contentSecurityPolicy` configuration added. |
| `v12.0.9` | `lazyRoot` prop added. |
| `v12.0.0` | `formats` configuration added.  
AVIF support added.  
Wrapper `<div>` changed to `<span>`. |
| `v11.1.0` | `onLoadingComplete` and `lazyBoundary` props added. |
| `v11.0.0` | `src` prop support for static import.  
`placeholder` prop added.  
`blurDataURL` prop added. |
| `v10.0.5` | `loader` prop added. |
| `v10.0.1` | `layout` prop added. |
| `v10.0.0` | `next/image` introduced. |