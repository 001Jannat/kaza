
# User Authentication API
 
This project is a RESTful API built with **Node.js**, **Express.js**, and **MySQL**, providing secure user authentication functionalities including Signup, Signin, and Profile Update.
 
## 🔧 Technologies Used
 
- **Node.js**
- **Express.js**
- **MySQL** (via `mysql2` module or `sequelize` if using ORM)
- **bcrypt** for password hashing
- **jsonwebtoken (JWT)** for authentication
- **dotenv** for managing environment variables
 
---
 
## 📦 API Features
 
### 1. 📝 Signup Endpoint
 
- **URL:** `/api/auth/signup`
- **Method:** `POST`
- **Description:** Create a new user account.
- **Request Body:**
  ```json
  {
    "username": "uniqueuser123",
    "email": "user@example.com",
    "password": "yourpassword"
  }
  ```
- **Validations:**
  - Username must be unique.
  - Email format must be valid.
  - Password must be provided.
 
- **Responses:**
  - `201 Created`: Account successfully created.
  - `400 Bad Request`: Missing fields or validation failed.
  - `409 Conflict`: Username or email already exists.
 
---
 
### 2. 🔐 Signin Endpoint
 
- **URL:** `/api/auth/signin`
- **Method:** `POST`
- **Description:** Log in with username or email and password.
- **Request Body:**
  ```json
  {
    "username": "uniqueuser123 or user@example.com",
    "password": "yourpassword"
  }
  ```
 
- **Responses:**
  - `200 OK`: Successfully authenticated, returns JWT token.
  - `400 Bad Request`: Missing parameters.
  - `401 Unauthorized`: Invalid credentials.
 
---
 
### 3. ✏️ Profile Update Endpoint
 
- **URL:** `/api/user/profile`
- **Method:** `PUT`
- **Description:** Update profile details of a logged-in user (username is immutable).
- **Headers:**
  ```http
  Authorization: Bearer <your_jwt_token>
  ```
 
- **Request Body:**
  ```json
  {
    "email": "newemail@example.com",
    "name": "New Name"
  }
  ```
 
- **Validations:**
  - JWT token must be provided.
  - Username cannot be changed.
  - Only valid fields are accepted.
 
- **Responses:**
  - `200 OK`: Profile successfully updated.
  - `400 Bad Request`: Validation errors.
  - `401 Unauthorized`: Missing or invalid token.
 
---
 
## 🔒 Security Considerations
 
- **Password Hashing:** All passwords are hashed using `bcrypt` before storage.
- **Authentication:** JWT tokens are used for session management and protecting routes.
- **Validation & Error Handling:**
  - Proper input validation is implemented using `express-validator` or custom middleware.
  - All endpoints return proper HTTP status codes and descriptive error messages.
 
---
 
## 🚀 Getting Started
 
### 1. Clone the Repository
```bash
git clone https://github.com/yourusername/user-auth-api.git
cd user-auth-api
```
 
### 2. Install Dependencies
```bash
npm install
```
 
### 3. Set Up Environment Variables
 
Create a `.env` file in the root directory:
```
PORT=5000
DB_HOST=localhost
DB_USER=root
DB_PASSWORD=yourpassword
DB_NAME=your_database_name
JWT_SECRET=your_jwt_secret
```
 
### 4. Create the Database and Users Table
 
Here’s a basic SQL schema:
```sql
CREATE DATABASE IF NOT EXISTS your_database_name;
 
USE your_database_name;
 
CREATE TABLE users (
  id INT AUTO_INCREMENT PRIMARY KEY,
  username VARCHAR(50) NOT NULL UNIQUE,
  email VARCHAR(100) NOT NULL UNIQUE,
  password VARCHAR(255) NOT NULL,
  name VARCHAR(100),
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```
 
### 5. Run the Application
```bash
npm start
```
 
---
 
## 🗂 Project Structure
 
```
├── controllers/
│   ├── authController.js
│   └── userController.js
├── routes/
│   ├── authRoutes.js
│   └── userRoutes.js
├── middleware/
│   ├── authMiddleware.js
│   └── errorHandler.js
├── config/
│   └── db.js
├── models/
│   └── userModel.js
├── app.js
├── server.js
└── .env
```
 
---
 
## ✅ Best Practices Followed
 
- Modular code structure
- Centralized error handling
- Input validation
- Secure password storage with bcrypt
- Protected routes with JWT
- Clear API responses with HTTP status codes
 
 
