# Flask Login Auth
A minimal session-based login system built with **Flask**, **SQLAlchemy** and **SQLite**. It demonstrates how to validate user credentials against a database, keep users signed in with Flask sessions, and give feedback with flash messages.

> **Note:** This is a learning project. Read the [Security Notes](#security-notes) before reusing any part of it in production.

## Features

- Login and logout using Flask sessions
- Credential validation through the SQLAlchemy ORM
- Flash messages for failed login attempts
- Seed script that creates demo accounts
- Clean login page built with HTML and CSS

## Tech Stack

| Layer         | Technology   |
| ------------- | ------------ |
| Language      | Python 3.10+ |
| Web framework | Flask        |
| ORM           | SQLAlchemy   |
| Database      | SQLite       |
| Templating    | Jinja2       |

## Project Structure

```
flask-login-auth/
├── app.py             # Flask app: routes and login/logout logic
├── tabledef.py        # SQLAlchemy User model and table creation
├── dummy.py           # Seed script for demo accounts
├── requirements.txt   # Python dependencies
├── static/
│   └── style.css      # Login page styles
└── templates/
    └── login.html     # Login page (Jinja2 template)
```

## Getting Started

### Prerequisites

- Python 3.10 or newer
- Git

### Installation

```bash
# 1. Clone the repository
git clone https://github.com/MuhammadSakha/flask-login-auth.git
cd flask-login-auth

# 2. Create and activate a virtual environment
python3 -m venv .venv
source .venv/bin/activate        # Windows: .venv\Scripts\activate

# 3. Install dependencies
pip install -r requirements.txt

# 4. Create the database table and seed demo accounts (run once)
python tabledef.py
python dummy.py

# 5. Start the development server
python app.py
```

Then open <http://localhost:4000> in your browser.

> Run `dummy.py` only once. Running it again will insert duplicate users.

### Demo Accounts

| Username    | Password   |
| ----------- | ---------- |
| `admin`     | `password` |
| `python`    | `python`   |
| `JUmpiness` | `Python`   |

Credentials are case-sensitive.

## Routes

| Method | Route     | Description                                         |
| ------ | --------- | --------------------------------------------------- |
| GET    | `/`       | Shows the login form, or a greeting if signed in    |
| POST   | `/login`  | Validates credentials and starts a session          |
| GET    | `/logout` | Ends the session and redirects to the home page    |

## How It Works

1. A visitor without an active session sees the login form at `/`.
2. The form sends a `POST` request to `/login`.
3. The server queries the `users` table with SQLAlchemy using the submitted username and password.
4. If a matching user exists, `session['logged_in']` is set to `True`. Otherwise an error is flashed.
5. The user is redirected back to `/`, and `/logout` clears the session flag.

## Security Notes

This project is intended for learning and is **not production-ready**:

- Passwords are stored and compared as **plain text**.
- The secret key is regenerated on every start, so all sessions are invalidated after a restart.
- There is no CSRF protection or rate limiting on the login form.
- The server runs with `debug=True`. Never enable debug mode on a public server.


