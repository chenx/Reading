# Commands

Check Node.js version
```
node -v
```

Install build tool Vite:
```
npm install -g create-vite
```

## Create a new React project in JS

```
npm create vite@latest my-react-app -- --template react
npm install --force
npm run dev
```

## Install router

```
npm install react-router-dom
```

## React-redux

https://react-redux.js.org/tutorials/typescript-quick-start

Install redux libraries:
```
npm install react-redux
npm install @reduxjs/toolkit
```

## Install Express and start a server

See https://www.w3schools.com/nodejs/nodejs_express.asp

```
npm install express
```

Install CORS support
```
npm install cors
```

Start local server:
```
node server.js
```

A express server:
```
    const express = require('express');
    const app = express();
    const cors = require('cors');
    const PORT = process.env.PORT || 3000; // Use environment variable or default to 3000

    const corsOptions = {
      origin: ['http://localhost:3001', 'http://localhost:5173'], // Allow specific origins
      methods: 'GET,HEAD,PUT,PATCH,POST,DELETE', // Allowed HTTP methods
      credentials: true, // Allow sending cookies/authentication headers
      optionsSuccessStatus: 204 // Status for successful OPTIONS preflight requests
    };

    app.use(cors(corsOptions)); // Enables CORS with specified options

    // Middleware to parse JSON request bodies
    app.use(express.json());

    // Define a GET endpoint
    app.get('/api/data', (req, res) => {
        res.status(200).json({ message: 'This is a GET request response.' });
    });

    app.get('/api/1/data', (req, res) => {
        // const data = '[{id: 0, title: "Title A", description: "Sample Description", display: "none"}]';
        const data = '[{"id":0,"title":"Title from Backend","description":"Message from backend","display":"none"}]';
        res.status(200).json({ message: data });
    });

    // Define a POST endpoint
    app.post('/api/submit', (req, res) => {
        const { name, email } = req.body; // Access data from the request body
        if (!name || !email) {
            return res.status(400).json({ error: 'Name and email are required.' });
        }
        res.status(201).json({ message: 'Data received successfully!', data: { name, email } });
    });

    // Define a PUT endpoint
    app.put('/api/update/:id', (req, res) => {
        const { id } = req.params; // Access data from URL parameters
        const { newStatus } = req.body;
        res.status(200).json({ message: `Item ${id} updated with status: ${newStatus}` });
    });

    // Define a DELETE endpoint
    app.delete('/api/delete/:id', (req, res) => {
        const { id } = req.params;
        res.status(200).json({ message: `Item ${id} deleted.` });
    });
```
