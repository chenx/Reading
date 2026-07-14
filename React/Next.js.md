# Next.js

- https://nextjs.org/learn/react-foundations
- https://nextjs.org/learn
- https://nextjs.org/docs

## Next.js FE/BE run on the same port

Next.js runs on a single port (like 3000) because it is a full-stack framework that natively handles both frontend rendering and backend API routing within the same server instance.

### Why Next.js Natively Uses One Port

*   **Unified Server Architecture:** Next.js uses a single Node.js runtime process (often powered by a built-in HTTP server or custom Express server). This server handles incoming traffic and routes it internally based on file directory structures.
*   **File-Based Routing:**
    *   Paths like `pages/index.js` or `app/page.tsx` serve your frontend HTML/React components.
    *   Paths like `pages/api/users.js` or `app/api/users/route.ts` serve your backend API endpoints.
*   **Shared Request Pipeline:** Because a single process manages both paths, a request to `http://localhost:3000/` (frontend) and `http://localhost:3000/api/users` (backend) hits the exact same listening port.

### Normalality

Normally, a Next.js application runs on the same port for both the frontend and the backend. This unified behavior is the default design of the framework, setting it apart from traditional setups like standard React.

#### Why the Same Port is Standard

*   **Zero Configuration:** When you run `npm run dev` or `next start`, Next.js spins up a single Node.js server instance (by default on port 3000).
*   **Built-in Handling:** That single server process automatically splits traffic based on the folder path. Requests to page routes (like `/dashboard`) yield frontend UI components, while requests to API routes (like `/api/users`) trigger backend functions.
*   **No CORS Issues:** Because the frontend and backend share the exact same origin, domain, and port, you never have to configure Cross-Origin Resource Sharing (CORS) headers.
*   **Simpler Infrastructure:** In your Nginx configuration, you only need to manage a single `proxy_pass` directive directing traffic to that one Next.js port.

#### Exceptions to the Rule

Developers will only split a Next.js app onto different ports if they have very specific infrastructural needs:

*   **Microservices:** They want to isolate backend resources so heavy API computation doesn't slow down the frontend rendering process.
*   **Independent Deployment Timelines:** The backend logic changes frequently and needs to be deployed separately without rebuilding the frontend user interface.

Unless you have complex scaling requirements, you should leverage the framework's native behavior and run both on the same port.


## React FE/BE run on different ports

In a traditional React application setup, the frontend and backend almost always run on different internal ports during development and production. This happens because React is purely a client-side library, meaning it requires a separate backend server architecture to function.

### Why They Run on Different Ports

*   **Two Separate Processes:** You are running two completely different software applications. The React frontend is a collection of static files (HTML, CSS, JS) managed by a development server (like Vite or Create React App) or a web server (like Nginx). The backend is a separate runtime process (like Node.js/Express, Python/Django, or Java/Spring Boot) handling database queries and logic.
*   **Network Isolation:** Two applications cannot bind to the exact same port on the same server at the same time. If your React app takes port 3000, your Express or Django backend must take a different port, such as 5000 or 8000.

### How They Communicate in Production (Two Approaches)

While they use different internal ports on your Ubuntu server, you can choose how they look to the public using Nginx:

#### Approach 1: The Same Public Domain (Using Nginx as a Reverse Proxy)

This is the standard, cleanest approach. Even though they live on different ports internally on your server, Nginx acts as a single gateway so the user only sees one domain (e.g., `example.com`).

*   **Internal Frontend:** React files served by Nginx or running on port 3000.
*   **Internal Backend:** Node/Python running on port 5000.
*   **Nginx Configuration:** Nginx intercepts traffic and hides the ports from the user:

```nginx
# Frontend requests (HTML, JS, Images)
location / {
    proxy_pass http://127.0.0.1:3000; 
}

# Backend API requests
location /api/ {
    proxy_pass http://127.0.0.1:5000;
}
```

*   **Advantage:** Avoids CORS (Cross-Origin Resource Sharing) security issues because the browser thinks everything is coming from the exact same place.

#### Approach 2: Separate Public Domains (Subdomains)

You can completely separate them to the outside world by assigning them distinct URLs.

*   **Frontend:** `example.com` routes to your React server (Port 3000).
*   **Backend:** `api.example.com` routes to your API server (Port 5000).
*   **Requirement:** You must enable and configure CORS on your backend server. If you don't, the user's browser will block React from making requests to the API for security reasons.


## Fundamental structural differences between React and Next.js

That is one of the most fundamental structural differences between a standard React project and a Next.js project. Here is a direct comparison of how they operate under the hood:

### 🔄 The Structural Split

| Feature | Standard React Project | Next.js Project |
| :--- | :--- | :--- |
| **Primary Nature** | Frontend Only (Client-side library) | Full-Stack (Framework for both UI and APIs) |
| **Port Setup** | Different Ports (e.g., React on 3000, API Backend on 8000) | Same Port (Unified server running on 3000) |
| **Server Engine** | Requires you to build and run a separate backend server (Node, Python, PHP) | Includes a built-in Node.js server engine that handles everything natively |
| **CORS Setup** | Required (Because browser requests cross between different ports) | Not Required for its own APIs (Shared origin means zero CORS config) |

### Why this difference exists

#### 1. Standard React is a "Guest" on the Server
A standard React application is just a collection of static files (HTML, CSS, JavaScript). Once compiled, it has no server-side logic. 

To make it do anything dynamic (like talk to a database), you must build a separate backend application. Because they are two separate codebases running two separate processes, they are forced to occupy different ports on your Ubuntu machine.

#### 2. Next.js is the "Host" and the "Server"
Next.js was specifically invented to solve this separation. It wraps React inside a Node.js web server. 

When you write code in Next.js, you can build your React UI components, and in the exact same codebase, write backend code (database queries, authentication, API routes). When you launch the app, Next.js spins up one single server process that listens on one single port (like 3000). It acts as its own router, sending standard web browsers to the frontend React pages and code-based fetch requests to the backend paths.

