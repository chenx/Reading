# Optimization

## Speed up page loading

### Network

- Reduce requests.
  - Lazy loading of image; load images in the viewport only
  - Cache
  - CDN
- Resource loading
  - Loading script: async, defer
  - Webpack splitchunk js code
  - Compression: css, js, html, image (use sprite)
  - Use more SSR (Server Side Rendering)
- Rendering
  - Use skeleton screen (https://www.nngroup.com/articles/skeleton-screens/)
  - Use loading icon animation
 
- Front loading of resources
  - inline css
  - preload font: <link rel="preload" ...>
  - async / defer JavaScript
  - Cache
- Simplify modules
  - Split JS code
  - load resources as needed
  - Optimize 3rd part lib and modules
  - Compress files

## Html5 page loading optimization

### page loading

- Container start (Client)
- Resource loading
  - Network connection:
    - DNS: reduce number of DNS lookup, pre-lookup
    - HTTP: HTTP2 (https://en.wikipedia.org/wiki/HTTP/2)
   
  - HTML loading
    - Content optimization: compression, simplify code and rendering
    - Flow optimization: SSR, pre-rendering
  - Static resource loading
    - Content optimization: compression, tree-shaking, image resizing,
    - Flow optimization: Cache, CDN, laze-loading, pre-loading, offline-loading
- Code execution
  - Reduce amount of execution: 防抖 (debounce)，节流 (throttle)
  - speed up: worker multi-threaded, wasm
  - flow optimization: deferred execution
- Data loading
  - content
  - flow
- Rendering: less reflow and repaint, deferred rendering, pre-loading, snapshot-loading

### Resources

CPU, RAM, Local I/O, Networking

### Collaboration sides

Frontend, Client side (Android/iOS), Data backend, Image service, Browser engine 

### Flow optimization

Preload, Simplification, Split

### Multiple levels
