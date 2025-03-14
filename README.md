# User Management API

This is a simple RESTful API built with **FastAPI** for managing users. It allows you to create, retrieve, and delete user records stored in a SQLite database. The API includes password hashing for security and uses SQLAlchemy for database interactions and Pydantic for data validation.

## Features
- **Create User**: Add a new user with a name, email, and securely hashed password.
- **Retrieve Users**: Fetch a list of all users (name and email only).
- **Delete User**: Remove a user by their ID.
- Passwords are encrypted using **bcrypt** for security.
- SQLite database for lightweight storage.

## Tech Stack
- **FastAPI**: A modern, fast (high-performance) web framework for building APIs.
- **SQLAlchemy**: ORM for database management.
- **Pydantic**: Data validation and serialization.
- **Passlib**: For password hashing with bcrypt.
- **SQLite**: Lightweight database.

## Prerequisites
- Python 3.8+
- Git (to clone the repository)

## Installation

1. **Clone the Repository**:
   ```bash
   git clone https://github.com/yourusername/user-management-api.git
   cd user-management-api
Set Up a Virtual Environment (optional but recommended):
bash

Collapse

Wrap

Copy
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
Install Dependencies:
bash

Collapse

Wrap

Copy
pip install -r requirements.txt
Note: You’ll need to create a requirements.txt file with the following:
text

Collapse

Wrap

Copy
fastapi
uvicorn
sqlalchemy
passlib[bcrypt]
Run the Application:
bash

Collapse

Wrap

Copy
uvicorn main:app --reload
The API will be available at http://127.0.0.1:8000.
Database Setup
The project uses SQLite as the database, stored in data.db.
The database and tables are automatically created when you run the app for the first time (thanks to Base.metadata.create_all).
API Endpoints
Method	Endpoint	Description	Request Body (if applicable)
GET	/user/show_users	Retrieve all users	None
POST	/user/new_user	Create a new user	{"name": "string", "email": "string", "password": "string"}
DELETE	/user/del_user/{id}	Delete a user by ID	None
Example Requests
Get All Users:
bash

Collapse

Wrap

Copy
curl http://127.0.0.1:8000/user/show_users
Response:
json

Collapse

Wrap

Copy
[{"name": "John Doe", "email": "john@example.com"}]
Create a New User:
bash

Collapse

Wrap

Copy
curl -X POST http://127.0.0.1:8000/user/new_user -H "Content-Type: application/json" -d '{"name": "Jane", "email": "jane@example.com", "password": "mypassword"}'
Response:
json

Collapse

Wrap

Copy
{"id": 1, "name": "Jane", "email": "jane@example.com", "password": "<hashed_password>"}
Delete a User:
bash

Collapse

Wrap

Copy
curl -X DELETE http://127.0.0.1:8000/user/del_user/1
Response:
json

Collapse

Wrap

Copy
{"detail": "Removed Done"}
Project Structure
text

Collapse

Wrap

Copy
user-management-api/
├── database.py      # Database configuration and session management
├── hashing.py       # Password hashing utility
├── main.py          # FastAPI app initialization
├── modelus.py       # SQLAlchemy model for Users table
├── routes/          # API route definitions
│   └── user.py
├── schemas.py       # Pydantic schemas for request/response validation
└── data.db          # SQLite database file (created on first run)
Notes
The API uses dependency injection (Depends) to manage database sessions.
Error handling is minimal; feel free to extend it for production use.
The password is hashed before storing, but the response includes it (you might want to exclude it in a real app).
Contributing
Feel free to fork this repository, submit issues, or send pull requests. Contributions are welcome!

License
This project is licensed under the MIT License. See the LICENSE file for details.
