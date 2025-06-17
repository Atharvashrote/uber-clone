# User Registration Endpoint Documentation

## POST `/user/register`

### Description

Registers a new user in the system. Validates the input data, hashes the password, creates the user, and returns an authentication token along with the user object.

### Request Body

The endpoint expects a JSON object with the following structure:

```json
{
  "fullname": {
    "firstname": "string (min 3 chars, required)",
    "lastname": "string (optional, min 3 chars if provided)"
  },
  "email": "string (valid email, required)",
  "password": "string (min 6 chars, required)"
}
```

#### Example

```json
{
  "fullname": {
    "firstname": "John",
    "lastname": "Doe"
  },
  "email": "john.doe@example.com",
  "password": "securePassword123"
}
```

### Responses

- **201 Created**

  - User registered successfully.
  - Returns: `{ "token": "jwt_token", "user": { ...userObject } }`
  - **Example:**
    ```json
    {
      "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
      "user": {
        "_id": "665f1c8b2f8b2a0012345678",
        "fullname": {
          "firstname": "John",
          "lastname": "Doe"
        },
        "email": "john.doe@example.com"
        // ...other user fields
      }
    }
    ```

- **400 Bad Request**

  - Validation failed (e.g., invalid email, missing fields, password too short).
  - Returns: `{ "errors": [ { "msg": "error message", ... } ] }`

- **500 Internal Server Error**
  - Unexpected server error.

### Notes

- The password is securely hashed before storage.
- The response includes a JWT token for authentication.
