# LMS-Library-Management-System

This project is a backend for a library management system built using FastAPI. It includes role-based access control for Librarians and Members, with JWT authentication. The backend allows librarians to manage books and members to borrow and return books.


## Tech Stack

**Programming Language:** Python

**Framework:** FastAPI

**Authentication:** JWT (JSON Web Tokens)

**Database:** MySQL Database

**Environment Management:** Python venv

**API Documentation:** FastAPI Swagger UI (auto-generated)
## Setup Instruction

Clone the Repository:
```bash
  git clone <repository-url>
```

Navigate to the Project Directory:
```bash
  cd <project-directory>
```

Create a Virtual Environment (optional but recommended):
```bash
  python -m venv venv
  source venv/bin/activate  # On Linux and MacOS
  venv\Scripts\activate     # On Windows
```

Install Dependencies:
```bash
  pip install -r requirements.txt
```

Set Up Environment Variables: Create a .env file in the root directory and define the following:
```bash
  SECRET_KEY = "your-256-bit-secret"
  ALGORITHM = "HS256 or RS256"
  ACCESS_TOKEN_EXPIRE_MINUTES = 10 # it refers to token expiration minutes
```

Run the Application:
```bash
  uvicorn app:app --reload
```

Access API Documentation:
Open your browser and go to http://127.0.0.1:8000/docs for Swagger UI.
## API Endpoints Documentation
List the main API routes and what they do. You can mention the request and response formats as shown below.

### Authentication

#### POST "/signup"
- Description: Register a new user (Librarian or Member).
- Request Body:
```bash
    {
        "username": "example",
        "password": "password",
        "role": "LIBRARIAN or MEMBER"
    }
```

#### POST "/login"
- Description: Login for existing users and token generation.
- Request Body:
```bash
    {
        "username": "example",
        "password": "password"
    }
```


### Librarian Routes
These routes require JWT authentication with the Librarian role.

#### GET "/view/members"
- Description:  To view the all members.

#### GET "/book"
- Description:  To view the all books.

#### POST "/book"
- Description:  Add a new book to the library.
- Request Body:
```bash
    {
        "title": "string",
        "author": "string"
    }   
```

#### PATCH "/book/update/{book_id}"
- Description:  Update book detail.
- Request Body:
```bash
    {
        "title": "string",
        "author": "string",
        "status": "string"
    } 
```

#### DELETE "/book/delete/{book_id}"
- Description:  Delete a book from the library.

#### POST "/add/member"
- Description:  To add the new user as member.
- Request Body:
```bash
    {
        "username": "string",
        "password": "string"
    } 
```

#### DELETE "/member/delete/{member_id}"
- Description:  To add the new user as member.



### Member Routes

#### GET "/books"
- Description: To view all the books.

#### POST "/book/borrow/{book_id}"
- Description: To borrow a book from the library.

#### POST "/book/return/{book_id}"
- Description: To return a book from the library.



## Database Structure

You can describe the tables and relationships here:

- Users Table: Contains details for both Librarians and Members.
- Books Table: Stores book information.
- Borrowed Books Table: Tracks which books are borrowed by which members.
- Activity Log Table: To Tracks the activities in the library.

### Example Tables
- Users Table

id | username  | password | role      | created_at
---|-----------|----------|-----------|-------------
 1 | librarian1| hashed_pw| LIBRARIAN | 2024-01-01
 2 | member1   | hashed_pw| MEMBER    | 2024-01-02


- Books Table

id | title        | author      | status
---|--------------|-------------|-----------
 1 | Python 101   | John Doe    | AVAILABLE
 2 | FastAPI Guide| Jane Smith  | BORROWED


- Borrowed Books Table

id | book_id | user_id | borrowed_at         | returned_at
---|---------|---------|---------------------|-------------
 1 |    2    |    2    | 2024-01-05 10:00:00 | 2024-01-10 14:00:00

## Testing the API


### Swagger UI
FastAPI automatically generates Swagger UI at /docs. You can test each endpoint directly from the browser.
