Recipe App RESTful API
Overview
This project is a RESTful API for a Recipe App built using Node.js, Express, and MongoDB. It provides endpoints to manage recipes, including creating, retrieving, updating, and deleting recipes. The API also includes pagination for efficiently handling large datasets, error handling, input validation, and JWT authentication for secure access.

Table of Contents
Features
Tech Stack
Installation
Configuration
Running the Application
API Endpoints
Error Handling and Validation
Testing the API
JWT Authentication
Features
CRUD Operations: Create, Read, Update, and Delete recipes.
Pagination: Efficiently manage large datasets with pagination.
Error Handling: Graceful handling of errors with informative messages.
Input Validation: Validate input data for required fields and data types.
JWT Authentication: Secure API access with JSON Web Tokens.
Tech Stack
Node.js: JavaScript runtime for server-side programming.
Express: Web framework for building APIs.
MongoDB: NoSQL database for data storage.
Mongoose: ODM (Object Data Modeling) library for MongoDB and Node.js.
JWT: For secure authentication.
Installation
Follow these steps to set up the project locally:

Clone the repository:

git clone https://github.com/eungobs/jwtRecipe-app.git
cd recipe-app
Install dependencies:

npm install
Install Nodemon globally for automatic server restarts:

npm install -g nodemon
Set up your MongoDB database. If you're using MongoDB Atlas, create a cluster and get the connection string. Replace your_mongo_uri in the .env file.

Configuration
Create a .env file in the root directory with the following content:

MONGO_URI=your_mongo_uri
PORT=5000
JWT_SECRET=your_jwt_secret
MONGO_URI: Your MongoDB connection string.
PORT: The port on which the server will run (default is 5000).
JWT_SECRET: A secret key for signing JWT tokens.
Running the Application
To start the server using Nodemon, run:

nodemon server.js
Nodemon will monitor your files for changes and automatically restart the server, allowing for a smoother development experience.

API Endpoints
The API provides the following endpoints:

Create a New Recipe
POST /api/recipes

Request Body:

{
  "title": "Spaghetti Carbonara",
  "ingredients": ["spaghetti", "eggs", "cheese", "bacon"],
  "instructions": "Cook spaghetti, mix with beaten eggs and cheese, add bacon.",
  "cookingTime": 30
}
Response:

201 Created: Recipe created successfully.
400 Bad Request: Validation errors.
Get All Recipes with Pagination
GET /api/recipes?page=1&limit=10

Query Parameters:

page: The page number (default is 1).
limit: Number of recipes per page (default is 10).
Response:

200 OK: List of recipes with pagination details.
Get a Recipe by ID
GET /api/recipes/:id

Response:

200 OK: Recipe details.
404 Not Found: Recipe not found.
Update a Recipe by ID
PUT /api/recipes/:id

Request Body:

{
  "title": "Spaghetti Carbonara with Mushrooms",
  "ingredients": ["spaghetti", "eggs", "cheese", "bacon", "mushrooms"],
  "instructions": "Cook spaghetti, mix with beaten eggs and cheese, add bacon and mushrooms.",
  "cookingTime": 35
}
Response:

200 OK: Updated recipe details.
404 Not Found: Recipe not found.
400 Bad Request: Validation errors.
Delete a Recipe by ID
DELETE /api/recipes/:id

Response:

204 No Content: Recipe deleted successfully.
404 Not Found: Recipe not found.
User Registration
POST /api/auth/register

Request Body:

{
  "email": "elizabeth@gmail.com",
  "password": "passw000"
}
Response:

201 Created: User registered successfully.
400 Bad Request: Validation errors.
User Login
POST /api/auth/login

Request Body:

{
  "email": "elizabeth@gmail.com",
  "password": "passw000"
}
Response:

200 OK: Login successful with a JWT token.
401 Unauthorized: Invalid email or password.
Error Handling and Validation
The API handles errors gracefully and provides informative error messages for validation failures. Input data is validated for:

Required fields (e.g., title, ingredients).
Data types (e.g., strings, numbers).
Custom validation rules (e.g., checking for valid data formats).
Testing the API
You can test the API using Postman or Insomnia:

Start the server:

nodemon server.js
Use the provided endpoints in Postman or Insomnia to send requests.

Verify the responses for each endpoint.

JWT Authentication
To secure the API, JWT (JSON Web Tokens) is implemented. The authentication flow is as follows:

During user registration, the user's email and password are stored in the database, and the password is hashed for security.
Upon successful login, a JWT token is generated and returned to the user. This token contains the user's ID and role and is signed with a secret key.
To access protected endpoints (e.g., creating, updating, or deleting recipes), the user must include the JWT token in the Authorization header as a Bearer token.
Example of Including JWT in Requests
To access a protected route, include the token in your request:


Authorization: Bearer your_jwt_token