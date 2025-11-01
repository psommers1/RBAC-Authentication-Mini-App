# RBAC Authentication Mini-App

Simple demonstration of authentication and role-based access control.

**Author:** Paul Sommers
**Course:** SDEV245

## Live Demo

Public demo available at: https://auth-demo.sommerscloud.com/

## What This Does

This is a basic Flask app that shows:
- Login with username/password
- Different user roles (admin vs user)
- Role-based access control

## CIA Triad Implementation

This application demonstrates all three principles of the CIA triad through its authentication and access control mechanisms.

### Confidentiality

**Definition:** Ensuring that information is accessible only to those authorized to access it.

**How This App Enforces Confidentiality:**

1. **Authentication Requirement** (lines 42-44 in `app.py`)
   - The dashboard route checks if a user is logged in before displaying any content
   - Unauthenticated users are redirected to the login page
   - This prevents unauthorized individuals from viewing user data

2. **Session-Based Access Control** (lines 30-31 in `app.py`)
   - User credentials are verified against the USERS dictionary
   - Only valid username/password combinations grant access
   - Flask sessions store user information securely

3. **Role Information Protection**
   - Each user's role is stored in their session (line 31)
   - Role information is only displayed to authenticated users
   - Different roles could access different data (extensible for future features)

**Example:** When you try to access `/dashboard` without logging in, the code `if 'username' not in session` (line 42) blocks access and redirects you to login, protecting the confidentiality of dashboard data.

### Integrity

**Definition:** Ensuring that information is accurate and has not been modified by unauthorized parties.

**How This App Enforces Integrity:**

1. **Session Data Protection** (line 8 in `app.py`)
   - Flask's `secret_key` cryptographically signs session cookies
   - This prevents users from tampering with their session data
   - If someone tries to modify their session cookie to change their role from 'user' to 'admin', the signature won't match and Flask will reject it

2. **Controlled Data Modification**
   - Only the login route can modify authentication state
   - Session data can only be set through proper authentication (lines 30-31)
   - Logout properly clears all session data (line 53)

3. **Validation of Credentials**
   - User input is validated against the USERS dictionary (line 29)
   - No direct database manipulation or unverified updates
   - Password must match exactly for authentication to succeed

**Example:** The `app.secret_key` (line 8) ensures that if a user tries to edit their browser cookie to change `role: 'user'` to `role: 'admin'`, Flask will detect the tampering because the cryptographic signature won't match, maintaining the integrity of the authorization system.

### Availability

**Definition:** Ensuring that authorized users have reliable and timely access to information and resources.

**How This App Enforces Availability:**

1. **Simple, Reliable Architecture**
   - Minimal dependencies (just Flask)
   - No external database required for basic operation
   - Hardcoded users mean no database downtime can prevent login

2. **Graceful Error Handling**
   - Flash messages provide clear feedback (lines 32, 35, 43, 54)
   - Failed logins don't crash the app, just show an error message
   - Users can retry login immediately

3. **Containerization Support**
   - Docker setup ensures consistent runtime environment
   - Application can be easily deployed and restarted
   - Port 5000 is exposed for reliable access

4. **Session Persistence**
   - Once authenticated, users stay logged in across requests
   - No need to re-authenticate for each page
   - Improves user experience and system availability

**Example:** When the login fails (line 35), instead of crashing or showing a generic error, the app displays `flash('Invalid credentials', 'error')` and keeps the login form available, ensuring the authentication service remains available for retry attempts.

### Summary

This RBAC application demonstrates the CIA triad by:
- **Protecting data confidentiality** through authentication checks
- **Maintaining data integrity** via cryptographically signed sessions
- **Ensuring service availability** with simple architecture and error handling

Together, these mechanisms create a secure system that protects user data while remaining accessible to authorized users.

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

## Links

- **GitHub:** https://github.com/psommers1/RBAC-Authentication-Mini-App
- **Live Demo:** https://auth-demo.sommerscloud.com/