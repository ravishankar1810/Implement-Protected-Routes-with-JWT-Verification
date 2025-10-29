# Node.js Express API with JWT Authentication

This project is a simple Node.js and Express.js backend server demonstrating how to implement JWT (JSON Web Token) authentication to protect API routes.

## 📁 Project Structure

```
.
├── controllers
│   └── authController.js   # Logic for login and protected routes
├── middlewares
│   └── authMiddleware.js   # Middleware to verify JWT
├── routes
│   └── authRoutes.js       # Defines the API routes
└── app.js                  # Main server entry point
```

## ✨ Features

- Public `/api/login` route to issue a JWT for valid credentials
- Protected `/api/protected` route requiring a valid JWT
- JWT verification middleware that checks for a Bearer token in the `Authorization` header

## ✅ Prerequisites

- Node.js (which includes npm)

## ⚙️ Installation

### 1. Initialize the project
```bash
npm init -y
```

### 2. Install dependencies
```bash
npm install express jsonwebtoken
```

### 3. (Optional) Install Nodemon for development
```bash
npm install nodemon --save-dev
```

Add the following to `package.json` scripts:
```json
"scripts": {
  "start": "node app.js",
  "dev": "nodemon app.js"
}
```

## 🚀 Running the Application

### Standard mode
```bash
node app.js
```

### Development mode
```bash
npm run dev
```

Server runs at: `http://localhost:5000`

## 📌 API Endpoints

### 🔓 Public Route — Login
**POST** `/api/login`

**Request Body (JSON)**
```json
{
  "username": "admin",
  "password": "12345"
}
```

**Response (200 OK)**
```json
{
  "token": "eyJhbGciOiJIUr..."
}
```

**Response (401 Unauthorized)**
```json
{
  "message": "Invalid credentials"
}
```

### 🔒 Protected Route
**GET** `/api/protected`

Requires:
```
Authorization: Bearer <YOUR_JWT_TOKEN>
```

**Response (200 OK)**
```json
{
  "message": "Access granted to protected route",
  "user": {
    "id": 1,
    "username": "admin",
    "iat": 1678888888,
    "exp": 1678892488
  }
}
```

**Response (403 Forbidden)**
```json
{
  "message": "No token provided"
}
```

**Response (401 Unauthorized)**
```json
{
  "message": "Invalid token"
}
```

## ✅ Testing the API

### 1. Without Token (Fail)
```bash
curl http://localhost:5000/api/protected
```

### 2. Login to get Token
```bash
curl -X POST http://localhost:5000/api/login \
     -H "Content-Type: application/json" \
     -d '{"username": "admin", "password": "12345"}'
```

### 3. Access Protected Route with Token
```bash
curl http://localhost:5000/api/protected \
     -H "Authorization: Bearer <YOUR_JWT_TOKEN>"
```

---

Happy coding! 🚀
