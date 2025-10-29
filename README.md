Node.js Express API with JWT Authentication

This project is a simple Node.js and Express.js backend server demonstrating how to implement JWT (JSON Web Token) authentication to protect API routes.

Project Structure

.
├── controllers
│   └── authController.js   # Logic for login and protected routes
├── middlewares
│   └── authMiddleware.js   # Middleware to verify JWT
├── routes
│   └── authRoutes.js       # Defines the API routes
└── app.js                  # Main server entry point


Features

A public /api/login route to issue a JWT for valid credentials.

A protected /api/protected route that requires a valid JWT.

A JWT verification middleware that checks for a Bearer token in the Authorization header.

Prerequisites

Before you begin, ensure you have the following installed on your machine:

Node.js (which includes npm)

Installation

Clone or create the files:
Create the files as shown in the file structure above and copy the code into them.

Initialize the project:
In your project's root directory, run:

npm init -y


This will create a package.json file.

Install dependencies:
Install Express and jsonwebtoken:

npm install express jsonwebtoken


(Optional) Install Nodemon:
For a better development experience with live reloading:

npm install nodemon --save-dev


Then, update your package.json scripts section:

"scripts": {
  "start": "node app.js",
  "dev": "nodemon app.js"
}


Running the Application

Standard mode:

node app.js


Development mode (if you installed nodemon):

npm run dev


The server will start and be accessible at http://localhost:5000.

API Endpoints

Public Route

POST /api/login

Authenticates a user and returns a JWT.

Body (raw, JSON):

{
  "username": "admin",
  "password": "12345"
}


Success Response (200 OK):

{
  "token": "eyJhbGciOiJIUr..."
}


Failure Response (401 Unauthorized):

{
  "message": "Invalid credentials"
}


Protected Route

GET /api/protected

This route is protected by JWT. You must provide a valid token in the Authorization header.

Header:
Authorization: Bearer <YOUR_JWT_TOKEN>

Success Response (200 OK):

{
  "message": "Access granted to protected route",
  "user": {
    "id": 1,
    "username": "admin",
    "iat": 1678888888,
    "exp": 1678892488
  }
}


Failure Response (403 Forbidden - No Token):

{
  "message": "No token provided"
}


Failure Response (401 Unauthorized - Invalid Token):

{
  "message": "Invalid token"
}


How to Test

You can use a tool like Postman or curl to test the endpoints.

Step 1: Try to access the protected route without a token (Expect failure)

curl http://localhost:5000/api/protected


Response: {"message":"No token provided"}

Step 2: Log in to get a token

curl -X POST http://localhost:5000/api/login \
     -H "Content-Type: application/json" \
     -d '{"username": "admin", "password": "12345"}'


Response: {"token":"eyJhbGciOiJIU..."} (Copy this token!)

Step Next: Access the protected route with the token (Expect success)

Replace <YOUR_JWT_TOKEN> with the token you copied from Step 2.

curl http://localhost:5000/api/protected \
     -H "Authorization: Bearer <YOUR_JWT_TOKEN>"


Response: {"message":"Access granted to protected route", "user":{...}}
