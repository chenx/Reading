# FastAPI

FastAPI is a modern, fast (high-performance), web framework for building APIs with Python based on standard Python type hints.

Source code: https://github.com/fastapi

Install fastapi:
- pip install "fastapi[standard]"

Run:
- fastapi dev main.py

Visit:
- Serving at: http://127.0.0.1:8000                  │
- API docs: http://127.0.0.1:8000/docs
- ReDocs: http://127.0.0.1:8000/redoc

Tutorial:
- https://fastapi.tiangolo.com/tutorial/
- https://fastapi.tiangolo.com/learn/

### Question: fastapi is only for API and not for other functions right?

No, FastAPI is not only for APIs; it can be used for other web functions as well, such as serving HTML pages and handling WebSockets
. However, it is primarily designed and optimized for building high-performance, API-first applications, and its built-in features are heavily focused on that purpose. 
FastAPI Capabilities Beyond Standard APIs
While its core strength is API development, FastAPI can perform various general web functions: 

- Serving HTML: You can use template engines like Jinja2 with FastAPI to generate and serve complete HTML web pages, similar to how frameworks like Flask do.
- WebSockets: FastAPI has first-class support for WebSockets, enabling real-time, full-duplex communication between the client and server for applications like chat apps or live dashboards.
- Background Tasks: It can run tasks in the background after sending an HTTP response to the client (e.g., sending emails, processing images), which allows for immediate responses to the user.
- Static Files: It can serve static files (JavaScript, CSS, images) directly.
- Middleware: You can add middleware for various purposes like handling CORS (Cross-Origin Resource Sharing), authentication, or logging, giving you control over the request/response cycle. 

Design Philosophy and Limitations

FastAPI is often described as a "headless" framework because it handles the backend logic and data requirements, leaving the front-end (user interface) to be developed separately using client-side technologies like React or Angular. 

- Focus: It is explicitly designed for building robust, scalable APIs with features like automatic interactive documentation (Swagger UI and ReDoc) and data validation using Pydantic models.
- Comparison: Unlike a full-stack framework like Django, FastAPI does not provide built-in components like an admin interface or extensive form handling utilities, which makes it less ideal for traditional, server-side rendered applications that need complex user interfaces out of the box. 

In essence, while FastAPI is flexible enough for general web tasks, its primary design and benefits are best utilized when building high-performance, API-centric applications.

