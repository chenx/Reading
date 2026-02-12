# Flask

Flask is a lightweight WSGI web application framework. It is designed to make getting started quick and easy, with the ability to scale up to complex applications.

Install:
- pip install Flask

Run:
- Create app.py
- Run: flask run

```
from flask import Flask
app = Flask(__name__)
@app.route("/")
def hello():
    return "Hello, World!"
```

Tutorial:
- https://flask.palletsprojects.com/en/stable/

