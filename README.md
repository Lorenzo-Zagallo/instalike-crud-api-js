# Node.js Post API with MongoDB & Gemini AI

## ✨ Overview

This project is a back-end API developed during the **Alura Back-end Immersion**. The main goal is to build a robust API for managing posts, featuring a unique integration with Google's Artificial Intelligence (Gemini) to automatically generate descriptions for uploaded images.

The API connects to a **local MongoDB** database and handles all CRUD (Create, Read, Update, Delete) operations for the posts collection.

## 🛠️ Technologies

* **Node.js**: JavaScript runtime environment.
* **Express**: Web framework for building the API.
* **MongoDB**: NoSQL database used for data persistence.
* **MongoDB Driver / Mongoose**: Library to interact with MongoDB.
* **Multer**: Middleware for handling `multipart/form-data` (image uploads).
* **dotenv**: For environment variable management.
* **CORS**: To handle security policies and allow frontend access.
* **Google Gemini API**: AI service used to generate text descriptions from images.

## ⚙️ Setup and Installation

Follow the steps below to configure and run the project locally.

### Prerequisites

1. **Node.js and npm** installed.
2. **MongoDB Server** installed and running locally (on the default port `27017`).
3. A **Google Gemini API Key** (for the image description feature).

### 1. Clone the Repository

```bash
git clone https://github.com/Lorenzo-Zagallo/instalike-crud-api-js.git
cd instalike-crud-api-js
```

### 2. Install Dependencies

```bash
npm install
```

### 3. Configure Environment Variables

Create a file named **`.env`** in the root of the project and add the following variables:

```env
# Connection string for Local MongoDB
STRING_CONEXAO="mongodb://localhost:27017/server_imersao_alura"

# Your Google Gemini API Key
GEMINI_API_KEY="YOUR_API_KEY_HERE"

# Express server port (e.g., 3000)
PORT=3000
```

### 4. Start the Server

```bash
npm start
# or
node server.js
```

The server will be running at `http://localhost:3000` (or the port defined in your `.env` file).

---

## 🚀 API Endpoints

You can test the endpoints using tools like Thunder Client (VS Code) or Postman.

| Method | Endpoint | Description |
| :--- | :--- | :--- |
| **`GET`** | `/posts` | Lists all posts stored in the database. |
| **`POST`**| `/posts` | Creates a new post with JSON data (useful for text-only posts). |
| **`POST`**| `/upload` | Receives an image (`multipart/form-data`) and creates an initial post. |
| **`PUT`** | `/upload/:id` | Updates an existing post. This endpoint triggers **Gemini** to analyze the image and generate a description. |

### Request Example

To **create the database and the first post** (and verify your local connection):

```http
POST http://localhost:3000/posts
Content-Type: application/json

{
    "descricao": "Initial test post",
    "imgUrl": "https://via.placeholder.com/150",
    "alt": "placeholder"
}
```

---

## 🔗 Project Structure

The structure follows an adapted MVC (Model-View-Controller) pattern:

```plaintext
/
├── src/
│   ├── config/
│   │   └── dbconfig.js       # Manages the MongoDB connection
│   ├── controllers/
│   │   └── postsController.js # Business logic and request handling
│   ├── models/
│   │   └── postsModel.js     # Direct database interaction (CRUD functions)
│   ├── routes/
│   │   └── postsRoutes.js    # Route definitions and middlewares (Multer, CORS)
│   ├── services/
│   │   └── geminiService.js  # Logic for communicating with the Gemini API
│   └── server.js             # Main file that initializes Express
├── uploads/                  # Directory for temporary and final image storage
├── .env                      # Environment variables (ignored by git)
├── package.json              # Project dependencies and scripts
└── README.md                 # Project documentation
```
