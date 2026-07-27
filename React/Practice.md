# React / Next.JS in Practice

### How to check which react or next.js version is used?

To check which React or Next.js version is being used, look inside your project's `package.json` file or run `npx next info` in your project terminal. The exact method you should use depends on whether you are examining a local codebase or investigating a live website in production.

#### Method 1: Checking inside a local project (Codebase)

If you have access to the source code, use one of these quick options:

* **Check package.json:** Open the root directory and check the `dependencies` block. Look for the `"react"` and `"next"` keys.
* **Run CLI commands:** Open your project terminal and use the following framework-specific commands:
  * **For Next.js and React together:** Run `npx next info`. This will print the precise versions of `next`, `react`, and `react-dom` currently installed.
  * **For Next.js only:** Run `npx next --version` to see the installed framework version.
  * **For React only:** Run `npm ls react` to print your local dependency version tree.

#### Method 2: Checking on a live website (Production)

If you are inspecting a live website through your web browser, choose one of these approaches:

* **Use React Developer Tools:** Install the official React Developer Tools extension for your browser. Once installed, open your browser's inspect panel (F12), switch to the "Components" or "Profiler" tab, and the exact React version will be displayed in the upper-right corner of the pane.
* **Use Chrome Extensions:** Plugins like Wappalyzer can inspect the technology stack of any website and frequently extract framework versions directly from front-end signatures.
* **Check Browser Globals:** Open your browser console (F12 → Console) and check for framework footprint objects. Type `window.next` or look for `__NEXT_DATA__` inside the page source. If they return an object, the site relies on Next.js.

#### Method 3: Checking at runtime inside your code

If you need to output the version dynamically within your application, you can reference the version property from the core library package.

```javascript
import React from 'react';
console.log(React.version); // e.g., "19.0.0"
```
