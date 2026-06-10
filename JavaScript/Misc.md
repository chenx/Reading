# Misc

## Get vs Post

- Get: URL, has size limit (~2048 B); POST: body, no size limit
- Get URL can be bookmarked; POST not
- Browser will cache Get request; POST not
- Data type: GET accepts ASCII; no limit for POST

## Load 100k items: how to do it fast

- Batch load: loop by setTimeout; use Document Fragment to reduce reflow
- Virtual list: only render what's in viewport

Other performance optimization methods:
- paging
- laze loading
- infinite scrolling
- virtual scrolling
- data compression
- SSR

## Engineering tools: Webpack vs Vite

- Bundle or not: Webpack uses bundle; Vite use node_modules and project source code
- First page loading, lazy loading: not a problem for Webpack; Vite has issues
- Start speed: Webpack is slower due to size; Vite is faster
- Hot reload: Webpack: supports HMR (Hot Module Replacing), still slower; Vite is faster
- Prod packaging: Webpack is more mature; Vite uses Rollup
- Ecosystem: Webpack has a mature ecosystem

Webpack and Vite approach building web applications differently. 
- Webpack is a "bundle-first" tool that reads your entire project and builds it before launching the dev server. 
- Vite is a "run-first" tool that uses native browser ES modules to serve files on demand, instantly launching the server and only bundling during production

### Development Commands

| Task | Webpack Command | Vite Command |
|------|----------------|-------------|
| Start Development Server | `npx webpack serve` | `npx vite` |
| Start Server with Custom Config | `npx webpack serve --config webpack.config.js` | `npx vite --config vite.config.js` |
| Run in Development Mode | `npx webpack --mode development` | `npx vite` *(default is dev mode)* |

### Production Commands

| Task | Webpack Command | Vite Command |
|------|----------------|-------------|
| Build for Production | `npx webpack` | `npx vite build` |
| Preview Production Build Locally | `npx serve dist` *(requires `serve`)* | `npx vite preview` |
| Build with Custom Config | `npx webpack --config webpack.config.js` | `npx vite build --config vite.config.js` |

Behind the Scenes
- Webpack: Crawls the entire dependency graph and glues it all together upfront. When a file changes in development, it reconstructs the bundles, which can be sluggish for larger applications.
- -Vite: Pre-bundles dependencies (using esbuild) and serves raw source files to the browser instantly. When you save, it only updates the single changed module. For production builds, Vite uses Rollup.

