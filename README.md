# RBAC Authentication Mini-App

Simple demonstration of authentication and role-based access control.

**Author:** Paul Sommers  
**Course:** SDEV245

## What This Does

This is a basic Flask app that shows:
- Login with username/password
- Different user roles (admin vs user)
- Role-based access control

## CIA Triad - Confidentiality

This app demonstrates **Confidentiality** by requiring users to log in before accessing the dashboard. Only authenticated users can see protected content.

## How to Run

**Option 1: With Docker (recommended)**
```bash
docker-compose up --build
```

**Option 2: Without Docker**
```bash
pip install -r requirements.txt
python app.py
```

Then go to http://localhost:5000

## Test Users

- Username: `admin` / Password: `admin123` (admin role)
- Username: `user` / Password: `user123` (user role)

## Files

- `app.py` - Main application with routes and logic
- `templates/` - HTML templates
- `requirements.txt` - Dependencies (just Flask)

## GitHub

https://github.com/psommers1/RBAC-Authentication-Mini-App