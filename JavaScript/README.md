# Index

Basics

- Closure
- Event loop
- Promise.all
- Deep copy
- Macro / Micro tasks
- Memmory garbage collection
- async / await
- this binding

Frameworks

- Virtual DOM diff, Hooks dependency, Vue3 responsive optimization
- Performance Optimization: Lighthouse, Webpack, non-invasive event tracking

 Engineering

 - CI/CD
 - Automated testing
 - Module federation
 - Vite, Turbopack

Others

- Design gray release system
- HOC with cache
- Architecture: SSR (Server Side Rendering) / CSR (Client Side Rendering) tradeoff, BFF layer design

## SSR / CSR

The tradeoff between Server-Side Rendering (SSR) and Client-Side Rendering (CSR) involves balancing initial load speed and SEO with user experience and interactivity. SSR provides fast first-load content and better search engine optimization (SEO) by rendering HTML on the server, but it increases server load and can have slower subsequent interactions. CSR delivers rich, app-like interfaces and reduces server strain by offloading rendering to the browser, but it can result in slower initial page loads and may pose SEO challenges. 

### Server-Side Rendering (SSR)

How it Works:
- The server renders the full HTML for a page and sends it to the browser, which displays the content immediately. 

Pros:

- Fast Initial Load: Users see content quickly, improving the perceived performance. 
- Better SEO: Search engines can easily crawl and index the pre-rendered HTML content. 
- Good for Static Content: Ideal for content-heavy sites like blogs or e-commerce sites where content variation is minimal. 

Cons:

- Higher Server Load: Rendering pages on the server consumes more server resources and can be costly, especially under high traffic. 
- Slower Interactivity: After the initial load, client-side interactions might still require server calls, potentially leading to full-page reloads. 

### Client-Side Rendering (CSR)

How it Works:
- The server sends minimal HTML along with a JavaScript bundle, which the browser then executes to build the page's content. 

Pros:
- Rich Interactivity: Enables smooth, app-like experiences and faster responses after the initial load. 
- Reduced Server Load: Offloads rendering to the client, reducing the strain on the web server and making it easier to scale. 
- Ideal for SPAs: Well-suited for single-page applications (SPAs) and dashboards with dynamic, real-time content. 

Cons:
- Slower Initial Load: Users may experience a delay as JavaScript is downloaded and executed to render the content. 
- SEO Challenges: Search engines can have difficulty indexing JavaScript-rendered pages, though this is improving. 
- Device Strain: Can strain older or less powerful devices as they are responsible for much of the processing. 

### Choosing Between SSR and CSR

Use SSR for:
- Sites prioritizing fast first-load content and excellent SEO, such as blogs, news sites, or large e-commerce platforms. 

Use CSR for:
- Applications requiring dynamic, interactive, or real-time features, like dashboards, social media feeds, or chat applications. 

Consider Hybrid Solutions:
- Frameworks like Next.js (for React) and Nuxt.js (for Vue) can support both SSR and CSR, allowing for optimized performance by combining their strengths. 


# References
- https://prismic.io/blog/client-side-vs-server-side-rendering
