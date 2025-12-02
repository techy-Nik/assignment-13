# FastAPI Calculator with JWT Authentication & Frontend

A production-ready REST API calculator with JWT-based authentication, interactive frontend pages, and comprehensive E2E testing using Playwright.

## 🎯 Project Overview

This project demonstrates full-stack web development with authentication:

- **JWT Authentication** - Secure token-based user authentication
- **Frontend Pages** - Interactive HTML/CSS/JS registration and login pages
- **Playwright E2E Testing** - Automated browser testing for user flows
- **CI/CD Pipeline** - Automated testing and Docker Hub deployment
- **Password Security** - Bcrypt hashing with validation
- **Token Management** - JWT storage and refresh token support
- **Redis Integration** - Token blacklisting for logout functionality

## ✨ New Features in Module 13

### Authentication System
✅ JWT-based authentication with access and refresh tokens  
✅ Secure password hashing with bcrypt  
✅ Token refresh mechanism  
✅ Token blacklisting with Redis  
✅ Protected endpoints with authentication middleware

### Frontend Pages
✅ Modern, responsive registration page with validation  
✅ Interactive login page with error handling  
✅ Client-side validation (email format, password strength)  
✅ JWT token storage in localStorage  
✅ Success/error message display

### E2E Testing with Playwright
✅ Positive test: Register with valid credentials  
✅ Positive test: Login with correct credentials  
✅ Negative test: Register with weak password  
✅ Negative test: Login with wrong password  
✅ UI validation and error message verification

### CI/CD Enhancements
✅ Automated Playwright tests in GitHub Actions  
✅ Redis service for token management  
✅ Multi-stage testing (unit, integration, e2e)  
✅ Automatic Docker Hub deployment on success

## 🏗️ Architecture

### API Endpoints

#### Authentication Endpoints
- `POST /register` - Register new user with JWT response
- `POST /login` - Login user and receive JWT tokens
- `POST /token/refresh` - Refresh access token
- `POST /logout` - Logout and blacklist token

#### Calculation Endpoints (Protected)
- `GET /calculations` - Browse all calculations (requires JWT)
- `GET /calculations/{id}` - Read specific calculation (requires JWT)
- `POST /calculations` - Create calculation (requires JWT)
- `PUT /calculations/{id}` - Update calculation (requires JWT)
- `DELETE /calculations/{id}` - Delete calculation (requires JWT)

### Frontend Pages

- **`/register.html`** - User registration with validation
- **`/login.html`** - User login with error handling
- **`/index.html`** - Main calculator interface (Module 14)

### Project Structure

```
./
├── app/
│   ├── auth/
│   │   ├── __init__.py
│   │   ├── dependencies.py
│   │   ├── jwt.py
│   │   └── redis.py
│   ├── core/
│   │   ├── __init__.py
│   │   └── config.py
│   ├── models/
│   │   ├── __init__.py
│   │   ├── calculation.py
│   │   └── user.py
│   ├── operations/
│   │   └── __init__.py
│   ├── schemas/
│   │   ├── __init__.py
│   │   ├── base.py
│   │   ├── calculation.py
│   │   ├── token.py
│   │   └── user.py
│   ├── __init__.py
│   ├── database.py
│   ├── database_init.py
│   └── main.py
├── static/
│   ├── css/
│   │   └── style.css
│   └── js/
│       └── script.js
├── templates/
│   ├── dashboard.html
│   ├── index.html
│   ├── layout.html
│   ├── login.html
│   └── register.html
├── tests/
│   ├── e2e/
│   │   ├── __init__.py
│   │   ├── test_e2e.bk
│   │   └── test_fastapi_calculator.py
│   ├── integration/
│   │   ├── __init__.py
│   │   ├── test_calculation.py
│   │   ├── test_calculation_schema.py
│   │   ├── test_database.py
│   │   ├── test_dependencies.py
│   │   ├── test_schema_base.py
│   │   ├── test_user.py
│   │   └── test_user_auth.py
│   ├── unit/
│   │   ├── __init__.py
│   │   └── test_calculator.py
│   ├── __init__.py
│   └── conftest.py
├── Dockerfile
├── LICENSE
├── README.md
├── docker-compose.yml
├── init-db.sh
├── pytest.ini
└── requirements.txt
```

## 🚀 Getting Started

### Prerequisites

- Python 3.10 or higher
- Docker Desktop
- Node.js 18+ (for Playwright)
- Git

### Installation

#### Option 1: Docker Setup (Recommended)

1. **Clone the repository**
   ```bash
   git clone https://github.com/techy-Nik/assignment-13.git
   cd assignment-13
   ```

2. **Start the application with Docker Compose**
   ```bash
   docker-compose up --build
   ```

3. **Access the application**
   - Registration Page: http://localhost:8000/register.html
   - Login Page: http://localhost:8000/login.html
   - API Documentation: http://localhost:8000/docs
   - Alternative Docs: http://localhost:8000/redoc

#### Option 2: Local Setup

1. **Clone the repository**
   ```bash
   git clone https://github.com/techy-Nik/assignment-13.git
   cd assignment-13
   ```

2. **Create and activate virtual environment**
   ```bash
   # Mac/Linux
   python3 -m venv venv
   source venv/bin/activate

   # Windows
   python -m venv venv
   venv\Scripts\activate
   ```

3. **Install Python dependencies**
   ```bash
   pip install -r requirements.txt
   ```

4. **Install Playwright browsers**
   ```bash
   playwright install
   ```

5. **Set up environment variables**
   ```bash
   cp .env.example .env
   # Edit .env with your credentials:
   # DATABASE_URL=postgresql://user:password@localhost:5432/calculator_db
   # REDIS_URL=redis://localhost:6379/0
   # JWT_SECRET_KEY=your-secret-key
   # JWT_REFRESH_SECRET_KEY=your-refresh-secret-key
   ```

6. **Start PostgreSQL and Redis**
   ```bash
   # Using Docker for services only
   docker-compose up postgres redis -d
   ```

7. **Run the application**
   ```bash
   uvicorn app.main:app --reload
   ```

## 🧪 Running Tests

### Run All Tests

```bash
# Install dependencies including Playwright
pip install -r requirements.txt
playwright install

# Run all tests with coverage
pytest --cov=app --cov-report=html -v
```

### Run Specific Test Suites

```bash
# Unit tests
pytest tests/unit/ -v

# Integration tests
pytest tests/integration/ -v

# E2E tests with Playwright
pytest tests/e2e/ -v --headed  # Show browser during tests
```

### Run Playwright Tests Only

```bash
# Run E2E tests
pytest tests/e2e/test_register.py -v
pytest tests/e2e/test_login.py -v

# Run with browser visible (headed mode)
pytest tests/e2e/ -v --headed

# Run in specific browser
pytest tests/e2e/ -v --browser chromium
pytest tests/e2e/ -v --browser firefox
pytest tests/e2e/ -v --browser webkit
```

### View Test Coverage Report

```bash
pytest --cov=app --cov-report=html
# Open htmlcov/index.html in your browser
```

## 🎭 Playwright E2E Test Coverage

### Positive Tests

#### Registration Flow
1. ✅ Navigate to registration page
2. ✅ Fill form with valid data:
   - Valid email format (user@example.com)
   - Strong password (min 8 chars with uppercase, lowercase, and numbers)
   - Matching password confirmation
3. ✅ Submit form
4. ✅ Verify success message displayed
5. ✅ Verify JWT token received/stored

#### Login Flow
1. ✅ Navigate to login page
2. ✅ Enter correct credentials
3. ✅ Submit form
4. ✅ Verify successful login message
5. ✅ Verify JWT token stored in localStorage
6. ✅ Verify redirect to calculator page

### Negative Tests

#### Registration Errors
1. ✅ Submit with weak password (< 8 chars)
   - Verify client-side error message
   - Verify form doesn't submit
2. ✅ Submit with password missing uppercase
   - Verify "Password must be at least 8 characters long and contain uppercase, lowercase, and numbers"
3. ✅ Submit with password missing lowercase
   - Verify password validation error
4. ✅ Submit with password missing numbers
   - Verify password validation error
5. ✅ Submit with invalid email format
   - Verify email validation error
6. ✅ Submit with mismatched passwords
   - Verify password confirmation error
7. ✅ Submit with existing username/email
   - Verify server returns 400
   - Verify "User already exists" message

#### Login Errors
1. ✅ Submit with wrong password
   - Verify server returns 401
   - Verify "Invalid credentials" message displayed
2. ✅ Submit with non-existent user
   - Verify 401 Unauthorized
   - Verify error message shown
3. ✅ Submit with empty fields
   - Verify client-side validation prevents submit

## 🎨 Frontend Features

### Registration Page (`register.html`)

**Features:**
- Email validation (proper format)
- Password strength requirements:
  - Minimum 8 characters
  - At least one uppercase letter (A-Z)
  - At least one lowercase letter (a-z)
  - At least one number (0-9)
- Password confirmation matching
- Real-time validation feedback
- Success/error message display
- Responsive design

**Client-Side Validation:**
```javascript
// Email format check
const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;

// Password strength requirements
// - At least 8 characters
// - Must contain uppercase letter
// - Must contain lowercase letter
// - Must contain number
const passwordRegex = /^(?=.*[a-z])(?=.*[A-Z])(?=.*\d).{8,}$/;

if (!passwordRegex.test(password)) {
    showError("Password must be at least 8 characters long and contain uppercase, lowercase, and numbers");
}

// Password confirmation match
if (password !== confirmPassword) {
    showError("Passwords do not match");
}
```

### Login Page (`login.html`)

**Features:**
- Email/username input
- Password input with visibility toggle
- Remember me option
- Error message display
- JWT token storage
- Redirect on success

**Token Storage:**
```javascript
// Store JWT in localStorage
localStorage.setItem('access_token', data.access_token);
localStorage.setItem('refresh_token', data.refresh_token);

// Redirect to calculator
window.location.href = '/index.html';
```

## 🔐 JWT Authentication Flow

### Registration Flow
```
User fills registration form
    ↓
Client validates input (email, password strength)
    ↓
POST /register with user data
    ↓
Server validates (duplicate check, hash password)
    ↓
Store user in database
    ↓
Generate JWT access + refresh tokens
    ↓
Return tokens to client
    ↓
Client stores tokens in localStorage
```

### Login Flow
```
User enters credentials
    ↓
POST /login with username/password
    ↓
Server verifies hashed password
    ↓
If valid: Generate JWT tokens
    ↓
Return tokens to client
    ↓
Client stores tokens in localStorage
    ↓
Redirect to calculator page
```

### Protected Endpoint Access
```
Client makes request to protected endpoint
    ↓
Include JWT in Authorization header
    ↓
Server validates token (signature, expiration)
    ↓
Check token not blacklisted (Redis)
    ↓
If valid: Process request
    ↓
Return response
```

## 🐳 Docker Hub Repository

**Docker Image**: [techynik/module-13](https://hub.docker.com/repository/docker/techynik/module-13/general)

### Pull and Run from Docker Hub

```bash
# Pull the image
docker pull techynik/module-13:latest

# Run with Docker Compose (includes PostgreSQL and Redis)
docker-compose up
```

### Build and Push (For Maintainers)

```bash
# Build the image
docker build -t techynik/module-13:latest .

# Tag for Docker Hub
docker tag techynik/module-13:latest techynik/module-13:latest

# Push to Docker Hub
docker push techynik/module-13:latest
```

## 💡 Manual Testing Guide

### Testing Registration Page

1. **Open Registration Page**
   ```
   http://localhost:8000/register.html
   ```

2. **Test Valid Registration**
   - Email: `test@example.com`
   - Password: `SecurePass123`
   - Confirm Password: `SecurePass123`
   - Click "Register"
   - ✅ Should see success message
   - ✅ Should receive JWT token

3. **Test Weak Password (No Uppercase)**
   - Email: `test2@example.com`
   - Password: `weakpass123` (no uppercase)
   - ✅ Should see error: "Password must be at least 8 characters long and contain uppercase, lowercase, and numbers"

4. **Test Weak Password (No Numbers)**
   - Email: `test3@example.com`
   - Password: `WeakPass` (no numbers)
   - ✅ Should see error: "Password must be at least 8 characters long and contain uppercase, lowercase, and numbers"

5. **Test Weak Password (Too Short)**
   - Email: `test4@example.com`
   - Password: `Pass1` (too short)
   - ✅ Should see error: "Password must be at least 8 characters long and contain uppercase, lowercase, and numbers"

6. **Test Invalid Email**
   - Email: `notanemail`
   - Password: `SecurePass123!`
   - ✅ Should see error: "Invalid email format"

5. **Test Password Mismatch**
   - Password: `SecurePass123!`
   - Confirm Password: `DifferentPass456!`
   - ✅ Should see error: "Passwords do not match"

### Testing Login Page

1. **Open Login Page**
   ```
   http://localhost:8000/login.html
   ```

2. **Test Valid Login**
   - Email: `test@example.com`
   - Password: `SecurePass123`
   - Click "Login"
   - ✅ Should see success message
   - ✅ Should redirect to calculator
   - ✅ Token stored in localStorage

3. **Test Wrong Password**
   - Email: `test@example.com`
   - Password: `WrongPassword123`
   - Click "Login"
   - ✅ Should see error: "Invalid credentials"

4. **Test Non-existent User**
   - Email: `nobody@example.com`
   - Password: `SomePassword123`
   - ✅ Should see error: "Invalid credentials"

### Verify JWT Token Storage

1. **Open Browser DevTools** (F12)
2. **Go to Application/Storage tab**
3. **Check localStorage:**
   ```javascript
   localStorage.getItem('access_token')
   localStorage.getItem('refresh_token')
   ```
4. **Should see JWT tokens stored**

## 🔧 CI/CD Pipeline

### GitHub Actions Workflow

The CI/CD pipeline runs on every push and pull request:

1. **Test Job**
   - Spins up PostgreSQL and Redis services
   - Runs unit tests
   - Runs integration tests
   - Runs Playwright E2E tests
   - Generates coverage reports

2. **Security Job**
   - Runs Trivy vulnerability scanner
   - Runs Bandit security linter
   - Uploads security reports

3. **Deploy Job** (on main branch only)
   - Builds Docker image
   - Pushes to Docker Hub
   - Creates deployment summary

### Running CI/CD Locally

```bash
# Install act (GitHub Actions local runner)
brew install act  # Mac
# or
choco install act  # Windows

# Run workflow locally
act push
```

## 📦 Dependencies

### Backend Dependencies
- **FastAPI** - Web framework
- **SQLAlchemy** - ORM
- **Pydantic** - Data validation
- **python-jose** - JWT implementation
- **passlib** - Password hashing
- **bcrypt** - Bcrypt hashing
- **redis** - Token blacklisting
- **psycopg2-binary** - PostgreSQL adapter

### Testing Dependencies
- **pytest** - Testing framework
- **pytest-playwright** - Playwright integration
- **playwright** - Browser automation
- **httpx** - HTTP client for testing
- **pytest-cov** - Coverage reporting

### Frontend Dependencies
- **HTML5** - Structure
- **CSS3** - Styling with animations
- **Vanilla JavaScript** - Client-side logic
- **Fetch API** - AJAX requests

See `requirements.txt` for complete list.

## 🐛 Troubleshooting

### Playwright Tests Failing

```bash
# Reinstall Playwright browsers
playwright install --force

# Run with browser visible to debug
pytest tests/e2e/ -v --headed --slowmo=1000

# Check browser logs
pytest tests/e2e/ -v --tracing=on
```

### JWT Token Issues

```bash
# Check Redis connection
docker-compose logs redis

# Verify token is stored
# Open browser console:
console.log(localStorage.getItem('access_token'));

# Check token expiration
# Tokens expire after 30 minutes by default
```

### Database Connection Issues

```bash
# Reset database
docker-compose down -v
docker-compose up -d

# Check PostgreSQL logs
docker-compose logs postgres

# Verify connection
docker-compose exec postgres psql -U user -d calculator_db
```

### Frontend Not Loading

```bash
# Verify templates directory
ls templates/

# Check FastAPI is serving static files
curl http://localhost:8000/register.html

# Check browser console for errors (F12)
```

## 📚 API Schema Examples

### Registration Request
```json
{
  "username": "john_doe",
  "email": "john@example.com",
  "password": "SecurePass123"
}
```

### Registration Response
```json
{
  "access_token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
  "refresh_token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
  "token_type": "bearer"
}
```

### Login Request
```json
{
  "username": "john_doe",
  "password": "SecurePass123"
}
```

### Protected Request
```bash
curl -X GET "http://localhost:8000/calculations" \
  -H "Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
```

## 🎓 Learning Objectives

This project demonstrates:

1. **JWT Authentication** - Token-based authentication system
2. **Frontend Development** - Interactive HTML/CSS/JS pages
3. **E2E Testing** - Browser automation with Playwright
4. **Security Best Practices** - Password hashing, token management
5. **CI/CD Pipeline** - Automated testing and deployment
6. **Redis Integration** - Token blacklisting and caching
7. **Full-Stack Development** - Backend + Frontend + Testing
8. **User Experience** - Form validation and error handling

## 📸 Screenshots

### Registration Page
![Registration Page](screenshots/register.png)

### Login Page
![Login Page](screenshots/login.png)

### Playwright Tests Passing
![Playwright Tests](screenshots/playwright-tests.png)

### GitHub Actions Success
![GitHub Actions](screenshots/github-actions.png)

## 📄 License

This project is licensed under the MIT License.

## 👤 Author

**Nikunj** - [techy-Nik](https://github.com/techy-Nik)

- GitHub: [@techy-Nik](https://github.com/techy-Nik)
- Project Repository: [assignment-13](https://github.com/techy-Nik/assignment-13)
- Docker Hub: [techynik/module-13](https://hub.docker.com/repository/docker/techynik/module-13)

