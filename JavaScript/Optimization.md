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
