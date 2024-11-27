# django-auth-backend

# Django JWT Authentication App

This is a simple authentication application built using **Django** and **Django REST Framework**. It supports user registration, authentication via **JWT (JSON Web Tokens)**, and includes an authenticated dashboard API.

## Features
- **User Registration**: Create a new user account.
- **JWT Authentication**: Obtain and refresh tokens.
- **Authenticated Dashboard**: Access protected endpoints for authenticated users.

---

## Installation

Follow these steps to set up the project locally:

### Prerequisites
- Python 3.8+
- pip (Python package manager)
- Virtual environment tool (e.g., `venv` or `virtualenv`)

### Steps
1. Clone the repository:
   ```bash
   https://github.com/umer066/django-auth-backend.git
   cd django-auth-backend
   cd backend
   ```

2. Create a virtual environment and activate it:
   ```bash
   python -m venv env
   source env/bin/activate   # On Linux/macOS
   env\Scripts\activate      # On Windows
   ```

3. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```

4. Run migrations:
   ```bash
   python manage.py migrate
   ```

5. Create a superuser (optional, for admin access):
   ```bash
   python manage.py createsuperuser
   ```

6. Start the development server:
   ```bash
   python manage.py runserver
   ```

---

## API Endpoints

### 1. **Register User**
**Endpoint**: `/api/register/`  
**Method**: `POST`  
**Payload**:
```json
{
    "username": "admin",
    "password": "admin"
}
```
**Response**: 
- `201 Created`: User successfully registered.
- Example:
  ```json
  {
      "id": 1,
      "username": "admin",
      "email": "admin@gmail.com"
  }
  ```

---

### 2. **Obtain JWT Token**
**Endpoint**: `/api/token/`  
**Method**: `POST`  
**Payload**:
```json
{
    "username": "admin",
    "password": "admin"
}
```
**Response**:
- `200 OK`: Returns access and refresh tokens.
- Example:
  ```json
  {
      "refresh": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ0b2tlbl90eXBlIjoicmVmcmVzaCIsImV4cCI6MTczNzA0OTgzMSwiaWF0IjoxNzMyNzI5ODMxLCJqdGkiOiI2ZjQzZWYyMGViNWI0MWEzODA4NzI5YzAwZjZmOTY4ZiIsInVzZXJfaWQiOjQsImZ1bGxfbmFtZSI6IiIsInVzZXJuYW1lIjoiYWRtaW4zIiwiZW1haWwiOiJhZG1pbjNAZ21haWwuY29tIiwiYmlvIjoiIiwiaW1hZ2UiOiJkZWZhdWx0LmpwZyIsInZlcmlmaWVkIjpmYWxzZX0.JNZgezPzUNd1jfBGja71iUqgCG4mIEf8Ta2qgP2vMj8",
      "access": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ0b2tlbl90eXBlIjoiYWNjZXNzIiwiZXhwIjoxNzMyNzMwMTMxLCJpYXQiOjE3MzI3Mjk4MzEsImp0aSI6IjA0NTE2ZmM3MzhkOTQ4MjhiZTI4MjdjOTZiZjNlMzcxIiwidXNlcl9pZCI6NCwiZnVsbF9uYW1lIjoiIiwidXNlcm5hbWUiOiJhZG1pbjMiLCJlbWFpbCI6ImFkbWluM0BnbWFpbC5jb20iLCJiaW8iOiIiLCJpbWFnZSI6ImRlZmF1bHQuanBnIiwidmVyaWZpZWQiOmZhbHNlfQ.LEvJV2E4c6ChZoNpA-Eek151EYeHIum7ywrAyjq_Ez8"
  }
  ```

---

### 3. **Refresh JWT Token**
**Endpoint**: `/api/token/refresh/`  
**Method**: `POST`  
**Payload**:
```json
{
    "refresh": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ0b2tlbl90eXBlIjoicmVmcmVzaCIsImV4cCI6MTczNzA0OTgzMSwiaWF0IjoxNzMyNzI5ODMxLCJqdGkiOiI2ZjQzZWYyMGViNWI0MWEzODA4NzI5YzAwZjZmOTY4ZiIsInVzZXJfaWQiOjQsImZ1bGxfbmFtZSI6IiIsInVzZXJuYW1lIjoiYWRtaW4zIiwiZW1haWwiOiJhZG1pbjNAZ21haWwuY29tIiwiYmlvIjoiIiwiaW1hZ2UiOiJkZWZhdWx0LmpwZyIsInZlcmlmaWVkIjpmYWxzZX0.JNZgezPzUNd1jfBGja71iUqgCG4mIEf8Ta2qgP2vMj8"
}
```
**Response**:
- `200 OK`: Returns a new access token.
- Example:
  ```json
  {
      "access": "new_eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ0b2tlbl90eXBlIjoiYWNjZXNzIiwiZXhwIjoxNzMyNzMwMTMxLCJpYXQiOjE3MzI3Mjk4MzEsImp0aSI6IjA0NTE2ZmM3MzhkOTQ4MjhiZTI4MjdjOTZiZjNlMzcxIiwidXNlcl9pZCI6NCwiZnVsbF9uYW1lIjoiIiwidXNlcm5hbWUiOiJhZG1pbjMiLCJlbWFpbCI6ImFkbWluM0BnbWFpbC5jb20iLCJiaW8iOiIiLCJpbWFnZSI6ImRlZmF1bHQuanBnIiwidmVyaWZpZWQiOmZhbHNlfQ.LEvJV2E4c6ChZoNpA-Eek151EYeHIum7ywrAyjq_Ez8"
  }
  ```

---

### 4. **Authenticated Dashboard**
**Endpoint**: `/api/dashboard/`  
**Methods**:
- **GET**: Returns a personalized message.
  - **Headers**: Include the `Authorization` header with your access token.
    ```bash
    Authorization: Bearer <access_token>
    ```
  - **Response**:
    ```json
    {
        "response": "Hey admin, You are seeing a GET response"
    }
    ```
- **POST**: Returns a personalized message with submitted text.
  - **Headers**: Include the `Authorization` header with your access token.
    ```bash
    Authorization: Bearer <access_token>
    ```
  - **Payload**:
    ```json
    {
        "text": "This is my Text"
    }
    ```
  - **Response**:
    ```json
    {
        "response": "Hey admin, your text is This is my Text"
    }
    ```

---

## Folder Structure
```
.
├── api/                  # Main app for APIs
│   ├── models.py         # Contains User and Profile models
│   ├── serializer.py     # Serializers for User and JWT
│   ├── views.py          # API view functions and classes
│   ├── urls.py           # App-specific URL mappings
├── project_name/         # Main Django project folder
│   ├── settings.py       # Project settings
│   ├── urls.py           # Project-wide URL mappings
│   ├── wsgi.py           # WSGI entry point
├── requirements.txt      # Python dependencies
├── manage.py             # Django management script
```

---

## Dependencies
- **Django**: Backend framework.
- **Django REST Framework (DRF)**: API framework.
- **SimpleJWT**: For token-based authentication.

Install all dependencies using:
```bash
pip install -r requirements.txt
```

---

## License
This project is licensed under the MIT License. See the `LICENSE` file for details.

---
