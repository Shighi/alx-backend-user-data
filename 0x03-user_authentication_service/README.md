# User Authentication Service

A Flask-based user authentication service built with SQLAlchemy, implementing user registration, login/logout, session management, and password reset functionality.

## Table of Contents

- [Requirements](#requirements)
- [Setup](#setup)
- [Project Structure](#project-structure)
- [Features](#features)
- [API Endpoints](#api-endpoints)
- [Usage Examples](#usage-examples)
- [Testing](#testing)
- [Development Guidelines](#development-guidelines)

## Requirements

- **Python Version**: Python 3.7 (Ubuntu 18.04 LTS)
- **Allowed Editors**: vi, vim, emacs
- **Code Style**: pycodestyle (version 2.5)
- **Database**: SQLAlchemy 1.3.x
- **Password Hashing**: bcrypt
- **Web Framework**: Flask

### Dependencies

```bash
pip3 install bcrypt
pip3 install flask
pip3 install sqlalchemy
```

## Setup

1. Clone the repository:
```bash
git clone https://github.com/your-username/alx-backend-user-data.git
cd alx-backend-user-data/0x03-user_authentication_service
```

2. Install required packages:
```bash
pip3 install bcrypt flask sqlalchemy
```

3. Make all Python files executable:
```bash
chmod +x *.py
```

4. Run the Flask application:
```bash
python3 app.py
```

The server will start on `http://0.0.0.0:5000`

## Project Structure

```
0x03-user_authentication_service/
├── README.md
├── user.py          # User SQLAlchemy model
├── db.py            # Database class with CRUD operations
├── auth.py          # Authentication class with business logic
├── app.py           # Flask application with API endpoints
└── main.py          # End-to-end integration tests
```

## Features

- **User Registration**: Create new user accounts with email and password
- **Password Security**: Secure password hashing using bcrypt
- **User Authentication**: Login validation with credentials
- **Session Management**: UUID-based session tracking
- **Password Reset**: Token-based password reset functionality
- **User Profile**: Authenticated user profile access
- **Logout**: Session destruction and cleanup

## API Endpoints

### Base Route
- **GET** `/` - Welcome message
  - Response: `{"message": "Bienvenue"}`

### User Management
- **POST** `/users` - Register a new user
  - Form data: `email`, `password`
  - Success: `{"email": "<email>", "message": "user created"}`
  - Error: `{"message": "email already registered"}` (400)

### Authentication
- **POST** `/sessions` - User login
  - Form data: `email`, `password`
  - Success: `{"email": "<email>", "message": "logged in"}` + session cookie
  - Error: 401 Unauthorized

- **DELETE** `/sessions` - User logout
  - Cookie: `session_id`
  - Success: Redirect to `/`
  - Error: 403 Forbidden

### User Profile
- **GET** `/profile` - Get user profile
  - Cookie: `session_id`
  - Success: `{"email": "<email>"}`
  - Error: 403 Forbidden

### Password Reset
- **POST** `/reset_password` - Request password reset token
  - Form data: `email`
  - Success: `{"email": "<email>", "reset_token": "<token>"}`
  - Error: 403 Forbidden

- **PUT** `/reset_password` - Update password with reset token
  - Form data: `email`, `reset_token`, `new_password`
  - Success: `{"email": "<email>", "message": "Password updated"}`
  - Error: 403 Forbidden

## Usage Examples

### Register a new user
```bash
curl -XPOST localhost:5000/users -d 'email=user@example.com' -d 'password=securepassword'
```

### Login
```bash
curl -XPOST localhost:5000/sessions -d 'email=user@example.com' -d 'password=securepassword' -v
```

### Access profile (with session cookie)
```bash
curl -XGET localhost:5000/profile -b "session_id=<session-id-from-login>"
```

### Request password reset
```bash
curl -XPOST localhost:5000/reset_password -d 'email=user@example.com'
```

### Update password
```bash
curl -XPUT localhost:5000/reset_password -d 'email=user@example.com' -d 'reset_token=<token>' -d 'new_password=newpassword'
```

### Logout
```bash
curl -XDELETE localhost:5000/sessions -b "session_id=<session-id>" -v
```

## Testing

Run the end-to-end integration tests:

```bash
python3 main.py
```

The test suite covers:
- User registration
- Login with correct/incorrect credentials
- Profile access (authenticated/unauthenticated)
- Session management
- Password reset workflow

If all tests pass, no output will be displayed.

## Development Guidelines

### Code Standards
- All files must start with `#!/usr/bin/env python3`
- Follow pycodestyle (version 2.5)
- All functions must be type annotated
- Comprehensive documentation for modules, classes, and functions
- All files must end with a new line
- All files must be executable

### Architecture Principles
- **Separation of Concerns**: Flask app only interacts with Auth class, never directly with DB
- **Encapsulation**: Only public methods of Auth and DB classes are used externally
- **Security**: Passwords are always hashed, sessions use UUIDs
- **Error Handling**: Proper exception handling and HTTP status codes

### Database Schema
The `users` table contains:
- `id`: Integer primary key
- `email`: Non-nullable string (VARCHAR 250)
- `hashed_password`: Non-nullable string (VARCHAR 250)
- `session_id`: Nullable string (VARCHAR 250)
- `reset_token`: Nullable string (VARCHAR 250)

### Security Features
- Passwords hashed with bcrypt and salt
- Session IDs are UUIDs for unpredictability
- Reset tokens are UUIDs with limited scope
- Proper HTTP status codes for security feedback
- Input validation and error handling

## Contributing

1. Ensure all code follows the project standards
2. Add comprehensive documentation
3. Include type annotations
4. Test all functionality before submitting
5. Follow the established architecture patterns

## License

This project is part of the ALX Backend specialization curriculum.
