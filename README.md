---


---

<h2 id="responsive-images">Responsive Images</h2>
<p>This is a referesher on responsive images in general, feel free to jump ahead to the next section on the image component.</p>
<p>Before responsive design and retina displays, images were a one-size-fits-all solution.</p>
<pre><code>&lt;img src="cat.jpg" width="100" height="100" /&gt;
</code></pre>
<p>Today, requesting one image for every customer, on every display or breakpoint, is non-ideal for both performance and image quality. Therefore, responsive images are the answer and they are fundamentally dependent on two attributes: <code>scrset</code> and <code>sizes</code>.</p>
<p>Responsive images use the power of <code>srcset</code> and <code>sizes</code> to hint to the browser which asset we’ve provided in our <code>srcset</code> to download, based on the user’s display resolution and the value of <code>sizes</code>.</p>
<pre class=" language-html"><code class="prism  language-html">/* Fixed Image */
<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>img</span> <span class="token attr-name">src</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>cat.jpg<span class="token punctuation">"</span></span> <span class="token attr-name">srcset</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>cat.jpg 100w, cat-large.jpg 200w<span class="token punctuation">"</span></span> <span class="token attr-name">sizes</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>100px<span class="token punctuation">"</span></span> <span class="token punctuation">/&gt;</span></span>

/* Responsive Image */
<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>img</span> <span class="token attr-name">src</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>cat.jpg<span class="token punctuation">"</span></span> <span class="token attr-name">srcset</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>cat.jpg 100w, cat-large 200w, cat-xl.jpg 800w<span class="token punctuation">"</span></span> <span class="token attr-name">sizes</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>(min-width: 1024px) 800px, 100px<span class="token punctuation">"</span></span> <span class="token punctuation">/&gt;</span></span>
</code></pre>
<p>We use the <code>w</code> descriptor after each source in the <code>srcset</code> to tell the browser how wide that asset is.</p>
<p>The <code>sizes</code> attribute can take media queries and use units such as <code>px</code>, <code>vw</code>, and <code>em</code>. The example above hints to the browser, that this image will display as 800px wide on a screen larger than 1024px, otherwise it is 100px wide everywhere else.</p>
<blockquote>
<p>Gotcha: We must always continue to provide the <code>src</code>, as <code>srcset</code> is not supported in IE.</p>
</blockquote>
<p><strong>The browser already knows the resolution or pixel density of the screen via <code>window.devicePixelRatio</code> and will always take into account when selecting the proper image to request.</strong> However, what the browser doesn’t know is the display size of the image at every breakpoint. So every time we provide a <code>srcset</code>, we also need a <code>sizes</code> attribute, or else the browser assumes <code>sizes="100vw"</code>, i.e. the image takes up the full width of the display.</p>
<h2 id="the-image-component-pl_image">The Image Component (pl_image)</h2>
<p>The image component provides a lot of features to create responsive images, including but not limited to: lazy loading, placeholders, space allocation, on-the-fly image crunching.</p>
<p>By default, all we need to provide the component is a <code>width</code>, <code>height</code>, and <code>imageId</code>.</p>
<pre class=" language-js"><code class="prism  language-js"><span class="token operator">&lt;</span>Image
  width<span class="token operator">=</span><span class="token punctuation">{</span><span class="token number">100</span><span class="token punctuation">}</span>
  height<span class="token operator">=</span><span class="token punctuation">{</span><span class="token number">100</span><span class="token punctuation">}</span>
  <span class="token comment">// IreID of our cat photo that we uploaded via Image Loader</span>
  imageId<span class="token operator">=</span><span class="token punctuation">{</span><span class="token number">12345678</span><span class="token punctuation">}</span>
<span class="token operator">/</span><span class="token operator">&gt;</span>
</code></pre>
<p>From these three props, we’ve provided a <code>src</code> with the URL to the image on the CDN, that is <code>RESIZE</code>d to 100x100, compressed to <code>Q85</code> quality and that allocates space for itself using padding on it’s container <code>div</code> (to prevent browser reflows). You can see all of this information within the URL.</p>
<pre class=" language-html"><code class="prism  language-html"><span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>div</span> <span class="token attr-name">class</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>ImageComponent ImageComponent--preventVerticalPopping<span class="token punctuation">"</span></span><span class="token style-attr language-css"><span class="token attr-name"> <span class="token attr-name">style</span></span><span class="token punctuation">="</span><span class="token attr-value"><span class="token property">padding-bottom</span><span class="token punctuation">:</span> <span class="token number">100%</span></span><span class="token punctuation">"</span></span><span class="token punctuation">&gt;</span></span>
  <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>img</span> <span class="token attr-name">class</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>ImageComponent-image<span class="token punctuation">"</span></span> <span class="token attr-name">src</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>https://secure.img1-fg.wfcdn.com/im/09237639/resize-h100-w100%5Ecompr-r85/3630/12345678/default_name.jpg<span class="token punctuation">"</span></span> <span class="token attr-name">srcset</span> <span class="token attr-name">sizes</span> <span class="token punctuation">/&gt;</span></span>
<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>div</span><span class="token punctuation">&gt;</span></span>
</code></pre>
<p>[Insert graphic that points out the different commands in the image URL]</p>
<p>That’s not very responsive though, let’s make it responsive with <code>enableDefaultSrcset</code> and <code>sizes</code> and add a <code>name</code> for the image so that it isn’t <code>default_image</code>.</p>
<pre class=" language-js"><code class="prism  language-js"><span class="token operator">&lt;</span>Image
  width<span class="token operator">=</span><span class="token punctuation">{</span><span class="token number">100</span><span class="token punctuation">}</span>
  height<span class="token operator">=</span><span class="token punctuation">{</span><span class="token number">100</span><span class="token punctuation">}</span>
  imageId<span class="token operator">=</span><span class="token punctuation">{</span><span class="token number">12345678</span><span class="token punctuation">}</span>
  name<span class="token operator">=</span><span class="token string">"cat"</span>
  enableDefaultSrcset
  sizes<span class="token operator">=</span><span class="token string">"100px"</span>
<span class="token operator">/</span><span class="token operator">&gt;</span>
</code></pre>
<p>which renders:</p>
<pre class=" language-html"><code class="prism  language-html"><span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>div</span> <span class="token attr-name">class</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>ImageComponent ImageComponent--preventVerticalPopping<span class="token punctuation">"</span></span><span class="token style-attr language-css"><span class="token attr-name"> <span class="token attr-name">style</span></span><span class="token punctuation">="</span><span class="token attr-value"><span class="token property">padding-bottom</span><span class="token punctuation">:</span> <span class="token number">100%</span></span><span class="token punctuation">"</span></span><span class="token punctuation">&gt;</span></span>
  <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>img</span> <span class="token attr-name">class</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>ImageComponent-image<span class="token punctuation">"</span></span>
       <span class="token attr-name">src</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>https://secure.img1-fg.wfcdn.com/im/09237639/resize-h100-w100%5Ecompr-r85/3630/12345678/default_name.jpg<span class="token punctuation">"</span></span> 
       <span class="token attr-name">srcset</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>https://secure.img1-fg.wfcdn.com/im/09237639/resize-h100-w100%5Ecompr-r85/3630/12345678/cat.jpg 100w, https://secure.img1-fg.wfcdn.com/im/09237639/resize-h200-w200%5Ecompr-r85/3630/12345678/cat.jpg 200w<span class="token punctuation">"</span></span> 
       <span class="token attr-name">sizes</span><span class="token attr-value"><span class="token punctuation">=</span><span class="token punctuation">"</span>100px<span class="token punctuation">"</span></span> 
  <span class="token punctuation">/&gt;</span></span>
<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>div</span><span class="token punctuation">&gt;</span></span>
</code></pre>
<p><code>enableDefaultSrcset</code> takes the provided image size and doubles it, creating a srcset with a 1x and 2x asset. If you need more flexibility than that, you can pass in <code>srcsetCommands</code> instead</p>
<p>[example with srcsetCommands]</p>
<p><a href="asdf">enter link description here</a></p>

