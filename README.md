# Flask API with Token-Based Authentication

## Description

This is a simple Flask application that demonstrates how to implement **token-based authentication** using the `flask_httpauth` library. The application includes one protected endpoint (`/protected_endpoint`) that requires a valid token to access. 

The code uses HTTP token authentication to verify requests before granting access to protected resources. If the request does not provide a valid token, the server will deny access and respond with an authentication error.

### Key Features:

- **Token Authentication**: The application uses a custom token verification function to validate the token sent in the HTTP request.
- **Protected Endpoint**: The `/protected_endpoint` route is protected and only accessible to clients who provide a valid token.
- **Flask HTTPAuth**: The app uses the `flask_httpauth` extension to manage the authentication process.

## Requirements

To run this application, you will need to have the following dependencies installed:

- **Flask**: A micro web framework for Python.
- **Flask-HTTPAuth**: An extension for Flask that simplifies token authentication.

### Install dependencies:

```bash
pip install Flask flask-httpauth
```

## How It Works

1. **Token Verification Logic**:
   - The `verify_token` function checks if the provided token matches a predefined valid token (`your_secret_token`).
   - This function is used by the `@auth.verify_token` decorator to authenticate requests.

2. **Protected Endpoint**:
   - The `/protected_endpoint` route is decorated with `@auth.login_required`, which ensures that only requests with a valid token can access this route.
   - If the token is valid, the server will respond with a message confirming access. If the token is invalid or missing, the client will receive a 401 Unauthorized response.

3. **Running the Server**:
   - The application runs the Flask development server in debug mode on `localhost:5000` by default.

## Example Usage

### Step 1: Start the Flask Application

Run the app using:

```bash
python app.py
```

By default, the Flask application will be hosted at `http://127.0.0.1:5000`.

### Step 2: Making Requests

You can interact with the API using tools like `curl`, `Postman`, or directly from a Python script.

#### Example Request with Valid Token:

```bash
curl -H "Authorization: Bearer your_secret_token" http://127.0.0.1:5000/protected_endpoint
```

Response:

```json
{
  "message": "This is a protected endpoint!"
}
```

#### Example Request with Invalid Token:

```bash
curl -H "Authorization: Bearer invalid_token" http://127.0.0.1:5000/protected_endpoint
```

Response:

```json
{
  "message": "Unauthorized"
}
```

## Customizing Token Validation

To adapt the token validation logic for your own application, modify the `verify_token` function to:

- Integrate with a database or external service for token management.
- Use more complex token formats (e.g., JWTs).
- Implement token expiration or other validation logic as needed.

## Running the App in Production

This app is designed for development and testing purposes. For production deployment, consider using a production-ready WSGI server like **Gunicorn** or **uWSGI**.

## License

This project is open source and released under the MIT License. See the LICENSE file for more details.

---

This Flask application demonstrates a basic token authentication setup and can serve as a starting point for building secure APIs that require token-based authentication.
