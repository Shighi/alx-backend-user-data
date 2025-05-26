# 0x01. Basic Authentication

## Description

This project introduces a basic user authentication system for an API using Flask. The application provides simple endpoints to check the server status and handles unauthorized and forbidden access using custom error messages. It includes an `Auth` class template for future enhancements of the authentication logic.

## Project Structure

```
0x01-Basic_authentication/
├── api/
│   └── v1/
│       ├── __init__.py
│       ├── app.py
│       ├── views/
│       │   ├── __init__.py
│       │   └── index.py
│       └── auth/
│           ├── __init__.py
│           └── auth.py
├── main_0.py
├── main_1.py
├── requirements.txt
└── README.md
```

## Features

* API status check endpoint: `GET /api/v1/status`
* Unauthorized access simulation: `GET /api/v1/unauthorized`
* Forbidden access simulation: `GET /api/v1/forbidden`
* Basic Auth class with method stubs for:

  * `require_auth`
  * `authorization_header`
  * `current_user`

## Setup

```bash
# Install dependencies
pip3 install -r requirements.txt

# Start the server
API_HOST=0.0.0.0 API_PORT=5000 python3 -m api.v1.app
```

## Usage

Check status:

```bash
curl "http://0.0.0.0:5000/api/v1/status"
# Output: {"status":"OK"}
```

Unauthorized route:

```bash
curl "http://0.0.0.0:5000/api/v1/unauthorized"
# Output: {"error": "Unauthorized"}
```

Forbidden route:

```bash
curl "http://0.0.0.0:5000/api/v1/forbidden"
# Output: {"error": "Forbidden"}
```

## Coding Requirements

* Python 3.7
* Ubuntu 18.04 LTS
* PEP8 compliant (pycodestyle v2.5)
* Each file is executable and ends with a newline
* Modules, classes, and functions include docstrings with clear explanations
* The first line of all Python files: `#!/usr/bin/env python3`

## Running Tests

Example:

```bash
API_HOST=0.0.0.0 API_PORT=5000 ./main_0.py
API_HOST=0.0.0.0 API_PORT=5000 ./main_1.py
```

## Author

Daisy Mwambi

## License

This project is part of the ALX Software Engineering Program.

