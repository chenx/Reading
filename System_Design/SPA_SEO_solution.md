# SPA SEO solutions

Standard React and Vue have the exact same SEO limitations.

By default, both build Single Page Applications (SPAs) that rely entirely on Client-Side Rendering (CSR). When a search engine spider or bot visits a standard Vue or React site, it initially receives a virtually empty HTML file containing just a generic container div and a massive bundle of JavaScript files.

The Core Problem: Client-Side Rendering (CSR)Search engine bots must download, parse, and execute that JavaScript before they can see or index your text, images, and links. While search engines like Google can crawl JavaScript, it is a two-step process that is severely limited by a "render budget". This delayed rendering often results in lower rankings, missing content, and poorly formatted snippets in search results.
