# 📚 Library Management System 🚀

## Description

A comprehensive web application for managing library resources, including books and users. This system allows for user authentication, book and user CRUD operations, and secure handling of images and data.

## Features ✨

- **User Authentication:** Secure login and logout functionality using JWT. 🔐
- **Role-Based Access Control:** Differentiates between `user` and `admin` roles for accessing specific features and APIs. 👑
- **Book Management:** Create, Read, Update, and Delete (CRUD) operations for books. 📖
- **User Management:** CRUD operations for managing user accounts, with administrative privileges. 👥
- **Image Uploads:** Supports uploading book cover images using Multer and storing them in MongoDB GridFS. 🖼️
- **RESTful API:** Provides a set of APIs for interacting with the library data programmatically. 🌐
- **Secure Data Handling:** Uses `bcryptjs` for password hashing and `jsonwebtoken` for authentication tokens. 🔒
- **Environment Configuration:** Manages sensitive information and configurations via environment variables using `dotenv`. ⚙️
- **Static File Serving:** Serves static assets like CSS from the `public` directory. 🎨

## Tech Stack 💻

- **Languages:** JavaScript (EJS)
- **Frameworks:** Express.js, Node.js
- **Database:** MongoDB (with Mongoose ODM and GridFS for file storage)
- **Templating Engine:** EJS
- **Authentication:** JSON Web Tokens (JWT), bcryptjs
- **File Uploads:** Multer
- **HTTP Client:** Axios
- **Utilities:** `body-parser`, `cookie-parser`, `dotenv`, `method-override`

## Installation 🍽️

1.  **Clone the repository:**
    ```bash
    git clone https://github.com/owlcityLIFE/LibrarySystem.git
    cd LibrarySystem
    ```

2.  **Install dependencies:**
    ```bash
    npm install
    ```

3.  **Set up environment variables:**
    Create a `.env` file in the root directory and add the following variables:

    ```env
    PORT=8080
    MONGODB_URI=your_mongodb_connection_string
    SESSION_SECRET=your_session_secret
    SECRET_KEY=your_jwt_secret_key
    ```
    *Replace `your_mongodb_connection_string`, `your_session_secret`, and `your_jwt_secret_key` with your actual credentials.*

4.  **Run the application:**
    ```bash
    npm start
    ```

## Usage 💡

This application serves as a Library Management System, enabling users and administrators to manage books and user data efficiently.

**1. Login and Authentication:**
   - Access the login page at `/login`.
   - Use the default credentials: `email: admin@hkmu.com`, `password: admin`.
   - Upon successful login, you will be redirected to the main dashboard (`/main`).
   - **Logout:** Click the logout button to end your session and return to the login page.

**2. Web Page Operations (CRUD):**
   - **Add Book:** Navigate to `/add-book` to add new books to the system. This page allows input for title, author, etc., and image uploads.
   - **Add User:** Navigate to `/add-user` to create new user accounts. Requires administrative privileges.
   - **Book List:** Access `/book-list` to view all available books, including details and options to edit or delete.
   - **User Management:** Access `/management-user` to view, edit, or delete user accounts. Requires administrative privileges.

**3. RESTful API Endpoints:**
   The system exposes several API endpoints for programmatic data management:

   | Method | Path                | Description                                       |
   | :----- | :------------------ | :------------------------------------------------ |
   | `POST` | `/api/auth/login`   | Authenticate a user and return a JWT token.       |
   | `POST` | `/api/auth/logout`  | Log out the current user and blacklist the token. |
   | `POST` | `/api/book/create`  | Create a new book entry.                          |
   | `GET`  | `/api/book`         | Get a list of all books.                          |
   | `GET`  | `/api/book/:id`     | Get details of a specific book by ID.             |
   | `PUT`  | `/api/book/edit/:id`| Update an existing book by ID.                    |
   | `DELETE`| `/api/book/delete/:id`| Delete a book by ID.                            |
   | `GET`  | `/api/user`         | Get a list of all users (admin only).             |
   | `GET`  | `/api/user/user`    | Get details of the currently logged-in user.      |
   | `GET`  | `/api/user/:id`     | Get details of a specific user by ID (admin only).|
   | `POST` | `/api/user/create`  | Create a new user account (admin only).           |
   | `PUT`  | `/api/user/update/:id`| Update a user account by ID (admin only).         |
   | `DELETE`| `/api/user/delete/:id`| Delete a user account by ID (admin only).       |
   | `GET`  | `/bookImg/:bookId`  | Retrieve a book image by its ID.                |

*Note: Most API endpoints require authentication and role verification.*

## Project Structure 📁

```
LibrarySystem/
├── CLI/
│   ├── createAdmin.js
│   ├── delete.js
│   └── get.js
├── controllers/
│   ├── authController.js
│   ├── bookController.js
│   ├── bookImgController.js
│   ├── imageController.js
│   └── userController.js
├── db/
│   └── db.js
├── middleware/
│   ├── header.js
│   └── verify.js
├── models/
│   ├── blacklistedToken.js
│   ├── book.js
│   └── user.js
├── public/
│   └── style.css
├── routes/
│   ├── api/
│   │   ├── authRoutes.js
│   │   ├── bookImgRoutes.js
│   │   ├── bookRoutes.js
│   │   └── userRoutes.js
│   ├── pages/
│   │   └── pages.js
│   └── routes.js
├── views/
│   ├── add-book.ejs
│   ├── add-user.ejs
│   ├── book-list.ejs
│   ├── login.ejs
│   ├── main.ejs
│   └── management-user.ejs
├── .env.example
├── package-lock.json
├── package.json
└── server.js
```

## API Reference 🌐

This section details the available API endpoints for interacting with the Library Management System.

**Authentication Routes (`/api/auth`)**

-   **`POST /api/auth/login`**
    -   **Description:** Authenticates a user with email and password.
    -   **Request Body:**
        ```json
        {
          "email": "user@example.com",
          "password": "password123"
        }
        ```
    -   **Response:**
        -   `200 OK`: `{ message: 'Login success', role: 'user|admin' }`
        -   `404 Not Found`: `{ message: 'Wrong email or password' }`
        -   `500 Internal Server Error`: `{ message: 'Login fail' }`

-   **`POST /api/auth/logout`**
    -   **Description:** Logs out the currently authenticated user by invalidating their token.
    -   **Response:**
        -   `200 OK`: `{ message: 'Logout success' }`
        -   `400 Bad Request`: `{ message: 'No token found' }`
        -   `500 Internal Server Error`: `{ message: 'Logout failed' }`

**Book Routes (`/api/book`)**

-   **`POST /api/book/create`**
    -   **Description:** Creates a new book.
    -   **Requires:** `user` role.
    -   **`image` (optional):** Multer file upload for the book cover.
    -   **Request Body:** Book details (e.g., `title`, `author`, `genre`).
    -   **Response:** Book object or error message.

-   **`GET /api/book`**
    -   **Description:** Retrieves a list of all books.
    -   **Requires:** `user` role.
    -   **Response:** An array of book objects.

-   **`GET /api/book/:id`**
    -   **Description:** Retrieves a single book by its ID.
    -   **Requires:** `user` role.
    -   **Response:** A book object or `404` if not found.

-   **`PUT /api/book/edit/:id`**
    -   **Description:** Updates an existing book by its ID.
    -   **Requires:** `user` role.
    -   **`image` (optional):** Multer file upload for the book cover.
    -   **Request Body:** Updated book details.
    -   **Response:** Updated book object or error message.

-   **`DELETE /api/book/delete/:id`**
    -   **Description:** Deletes a book by its ID.
    -   **Requires:** `user` role.
    -   **Response:** Success message or `404` if not found.

**User Routes (`/api/user`)**

-   **`GET /api/user`**
    -   **Description:** Retrieves a list of all users.
    -   **Requires:** `admin` role.
    -   **Response:** An array of user objects (excluding passwords).

-   **`GET /api/user/user`**
    -   **Description:** Retrieves the currently authenticated user's details.
    -   **Requires:** `user` role.
    -   **Response:** User object (excluding password).

-   **`GET /api/user/:id`**
    -   **Description:** Retrieves a specific user by their ID.
    -   **Requires:** `admin` role.
    -   **Response:** User object (excluding password) or `404` if not found.

-   **`POST /api/user/create`**
    -   **Description:** Creates a new user.
    -   **Requires:** `admin` role.
    -   **Request Body:** User details (`email`, `username`, `password`, `phone`, `hkid`).
    -   **Response:** Success message and the created user object or error.

-   **`PUT /api/user/update/:id`**
    -   **Description:** Updates a user's details by ID.
    -   **Requires:** `admin` role.
    -   **Request Body:** Updated user details.
    -   **Response:** Success message and the updated user object or error.

-   **`DELETE /api/user/delete/:id`**
    -   **Description:** Deletes a user by their ID.
    -   **Requires:** `admin` role.
    -   **Response:** Success message or `404` if not found.

**Book Image Routes (`/bookImg`)**

-   **`GET /bookImg/:bookId`**
    -   **Description:** Retrieves the image associated with a book ID.
    -   **Requires:** `user` role.
    -   **Response:** The image file stream or `404` if not found.

---
**<p align="center">Generated by [ReadmeCodeGen](https://www.readmecodegen.com/)</p>**
