# 🎵 Music Streaming Backend API

A RESTful backend application built with **Node.js**, **Express.js**, and **MongoDB** that provides user authentication, role-based authorization, music management, album management, and cloud-based music storage using ImageKit.

The project demonstrates backend fundamentals such as authentication with JWT, password hashing with bcrypt, file uploads using Multer, role-based access control, and integration with third-party cloud storage.

---

# 🚀 Features

### Authentication

* User registration
* User login
* User logout
* Password hashing using bcrypt
* JWT-based authentication
* Cookie-based token storage

### Authorization

* Role-based access control
* Two user roles:

  * User
  * Artist
* Only artists can upload music and create albums
* Users can browse music and albums

### Music Management

* Upload music files
* Store uploaded music on ImageKit
* Create music records
* Retrieve all music

### Album Management

* Create albums
* Retrieve all albums
* Retrieve album by ID

### Cloud Storage

* Upload music files to ImageKit
* Store the generated file URL in MongoDB

---

# 🛠️ Tech Stack

* Node.js
* Express.js
* MongoDB Atlas
* Mongoose
* JWT (jsonwebtoken)
* bcrypt
* Multer
* ImageKit
* Cookie Parser
* dotenv
* Nodemon

---

# 📁 Project Structure


Music-App/
│
├── node_modules/
│
├── src/
│   │
│   ├── controllers/
│   │   ├── auth.controller.js
│   │   └── music.controller.js
│   │
│   ├── db/
│   │   └── db.js
│   │
│   ├── middleware/
│   │   └── auth.middleware.js
│   │
│   ├── models/
│   │   ├── user.model.js
│   │   ├── music.model.js
│   │   └── album.model.js
│   │
│   ├── routes/
│   │   ├── auth.routes.js
│   │   └── music.routes.js
│   │
│   ├── services/
│   │   └── storage.service.js
│   │
│   └── app.js
│
├── .env
├── .gitignore
├── package.json
├── package-lock.json
└── server.js


---

# 🗄️ Database Schema

## User

| Field    | Type                        |
| -------- | --------------------------- |
| username | String                      |
| email    | String                      |
| password | String (hashed)             |
| role     | String (`user` or `artist`) |

---

## Music

| Field  | Type                 |
| ------ | -------------------- |
| uri    | String               |
| title  | String               |
| artist | ObjectId (ref: User) |

---

## Album

| Field  | Type                  |
| ------ | --------------------- |
| title  | String                |
| music  | ObjectId (ref: Music) |
| artist | ObjectId (ref: User)  |

---

# 🔐 Environment Variables

Create a `.env` file in the project root.

env
MONGO_URI=your_mongodb_connection_string

JWT_SECRET=your_jwt_secret

IMAGEKIT_PRIVATE_KEY=your_imagekit_private_key


---

# ⚙️ Installation

### Clone the repository

bash
git clone <repository-url>


### Navigate to the project directory

bash
cd Music-App


### Install dependencies

```bash
npm install
```

---

# ▶️ Running the Project

Start the development server using:

bash
nodemon server.js


---

# 🔑 Authentication Flow

### Register

* Checks if a user already exists using the username and email.
* Hashes the password using bcrypt.
* Creates a new user.
* Generates a JWT containing the user's ID and role.
* Stores the JWT in an HTTP cookie.

---

### Login

* Verifies the username and email.
* Compares the entered password with the hashed password using bcrypt.
* Generates a new JWT.
* Stores the JWT in an HTTP cookie.

---

### Logout

* Clears the authentication cookie.
* Logs the user out successfully.

---

# 🔒 Authorization

The application uses two middleware functions:

### authUser

* Verifies the JWT.
* Authenticates both **User** and **Artist** roles.

### authArtist

* Verifies the JWT.
* Allows access only to users with the **Artist** role.

Protected routes use these middleware functions to restrict access based on user roles.

---

# 🎵 Music API

| Method | Endpoint            | Description   | Access        |
| ------ | ------------------- | ------------- | ------------- |
| POST   | `/api/music/upload` | Upload music  | Artist        |
| GET    | `/api/music`        | Get all music | User / Artist |

---

# 💿 Album API

| Method | Endpoint                | Description     | Access        |
| ------ | ----------------------- | --------------- | ------------- |
| POST   | `/api/music/album`      | Create album    | Artist        |
| GET    | `/api/music/albums`     | Get all albums  | User / Artist |
| GET    | `/api/music/albums/:albumId` | Get album by ID | User / Artist |

---

# ☁️ File Storage

Music files are uploaded using **Multer** and stored securely on **ImageKit**.

The upload service:

* Receives the uploaded file.
* Uploads it to ImageKit.
* Returns the generated file URL.
* Saves the URL in the Music collection.

---

# 🧪 Testing

The API was tested using **Postman**, including:

* User registration
* User login
* User logout
* Artist-only routes
* Music upload
* Album creation
* Fetching music
* Fetching albums
* Fetching album by ID

---

# 📚 What I Learned

Through this project, I gained practical experience with:

* Building RESTful APIs using Express.js
* Designing MongoDB schemas with Mongoose
* JWT authentication and cookie-based sessions
* Password hashing with bcrypt
* Role-based authorization
* Middleware design
* File uploads using Multer
* Cloud storage integration with ImageKit
* Organizing a scalable backend project structure
* Environment variable management using dotenv
* Testing REST APIs with Postman

---



This project is open-source and intended for learning and educational purposes.
