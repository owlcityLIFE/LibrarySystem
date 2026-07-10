# 381project-31

 `server.js`:
- Dependencies: Imports required packages like `express`, `cookie-parser`, `body-parser`, `dotenv`, and others. Also imports custom modules like `header` middleware and `connectDB`.

- Configuration**:
  - Uses environment variables with `dotenv` for settings like the port.
  - Sets up the view engine as `EJS` for rendering templates.
  - Uses `cookie-parser` for handling cookies.
  - Uses `body-parser` to parse incoming request bodies in JSON format.
  - Serves static files from the `public` folder.
  - Adds custom headers with `setHeaders` middleware.

- Database Connection: The `connectDB` function (imported from `./db/db`) is called to establish a database connection before starting the server.

- Routes Initialization: Initializes all the routes by requiring and invoking `initRoutes` from `./routes/routes`.

- Server Start: The server listens on the specified port (from environment variables or defaulting to `8080`) after the database connection is successful.


`package.json`:
- axios (`^1.7.7`): A promise-based HTTP client for making requests, commonly used for API interactions.
- bcryptjs (`^2.4.3`): A library for hashing passwords using bcrypt, useful for authentication and securing user data.
- body-parser (`^1.20.3`): Middleware to parse incoming request bodies, particularly JSON and URL-encoded data.
- cookie-parser (`^1.4.7`): Middleware to parse `Cookie` header and populate `req.cookies`, enabling cookie management.
- dotenv (`^16.4.5`): Loads environment variables from a `.env` file into `process.env` for configuration purposes.
- ejs (`^3.1.10`): A template engine used for rendering HTML views with embedded JavaScript.
- express (`^4.21.1`): A popular Node.js web framework for building web applications and APIs.
- jsonwebtoken (`^9.0.2`): Implements JSON Web Tokens (JWT) for handling authentication and secure data exchange.
- method-override (`^3.0.0`): Lets you use HTTP verbs like `PUT` or `DELETE` in places where the client doesn't support it (e.g., HTML forms).
- mongoose (`^8.8.0`): An ODM (Object Document Mapper) for MongoDB, used to interact with MongoDB in an object-oriented way.
- multer (`^1.4.5-lts.1`): Middleware for handling file uploads in `multipart/form-data` forms, typically used for uploading images or documents.

`public folder` :
- style.css: This file defines the styles for your website, providing layout, colors, and general formatting for elements such as containers, login forms, buttons, and links. It includes a general reset for consistent styling, custom styles for a login page, form elements, buttons, and more.

`views folder`:
1. add-book.ejs
2. add-user.ejs
3. book-list.ejs
4. login.ejs
5. main.ejs
6. management-user.ejs


Here's a concise user flow and operational guide for your server, focusing on login/logout functionality, CRUD operations, and RESTful services:

 1. Login/Logout Pages
   - Valid Login Information: Ensure you have a set of valid credentials email:`admin@hkmu.com` and password:`admin`. These might be hard-coded for testing or saved in a database.
   - Sign-In Steps:
     1. Access the Login Page: Open the `/login` route to access the login form.
     2. Input Credentials: Enter the valid email and password in the respective fields.
     3. Click 'Submit': This triggers a POST request to authenticate the user.
     4. Login Success: If credentials are correct, the user is redirected to the main page (`/main`).
   - **Logout**: Use the logout button , which removes authentication cookies and redirects the user to the login page(`/login`).

  2. CRUD Operations on Web Pages
   - Create:
     - **add-book.ejs**: `/add-book` – Click the 'Add Book' button to open a form for adding a new book.
     - **add-user.ejs**: `/add-user` – Click the 'Add User' button to open a form for adding new user details.
   - Read:
     - **book-list.ejs**: `/book-list` – Shows the list of books and all book details. 
     - **management-user.ejs**: `/management-user` – Displays the list of users and all users details.
   - Update**:
     - **Edit Buttons on Book List Page**: Clicking the 'Edit' button next to a book in `/book-list` opens an edit form, allowing users to update book details (e.g. title, author).
     - **Edit Buttons on User Management Page**: Clicking the 'Edit' button next to a user in `/management-user` opens a form for editing user details (e.g., name, email).
   - Delete:
     - **Delete Buttons on Book List Page**: Clicking the 'Delete' button next to a book in `/book-list` removes that book from the list after confirmation.
     - **Delete Buttons on User Management Page**: Clicking the 'Delete' button next to a user in `/management-user` deletes that user from the list after confirmation.

  3. RESTful CRUD Services
   - API List:
     - **Create**:
       - HTTP Method: `POST`
       - Path URI: `/create`
       - Description: Creates a new book/user entry in the MongeDB.
     - **Read**:
       - HTTP Method: `GET`
       - Path URI: `/:id` or `/user` 
       - Description: Fetches a list of books/users or a specific book/user by ID or get user data.
     - **Update**:
       - HTTP Method: `PUT`
       - Path URI: `/edit/:id` or `/update/:id`
       - Description: Updates details of an existing book/user identified by ID.
     - **Delete**:
       - HTTP Method: `DELETE`
       - Path URI: `/delete/:id`
       - Description: Deletes an existing book/user identified by ID.
   
   - **Testing the APIs with CURL**: