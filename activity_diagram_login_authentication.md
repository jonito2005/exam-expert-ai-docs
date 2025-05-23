# Activity Diagram - Login and Authentication Process

This activity diagram illustrates the complete login and authentication process in the ExamExpert-AI system, which is a common functionality for all users (Admin, Teacher, and Student).

```
+-------------+          +-------------------+          +-------------------+
|             |          |                   |          |                   |
|    User     |          |       System      |          |   Database        |
|             |          |                   |          |                   |
+-------------+          +-------------------+          +-------------------+
       |                           |                            |
       | Access Login Page         |                            |
       |-------------------------->|                            |
       |                           |                            |
       |  Display Login Form       |                            |
       |<--------------------------|                            |
       |                           |                            |
       | Enter Credentials         |                            |
       | (Email & Password)        |                            |
       |-------------------------->|                            |
       |                           |                            |
       |                           | Validate Input Format      |
       |                           |------------+               |
       |                           |            |               |
       |                           |<-----------+               |
       |                           |                            |
       |                           | If Invalid Format          |
       |                           |------------+               |
       |                           |            |               |
       |                           |<-----------+               |
       |                           |                            |
       |  Display Error Message    |                            |
       |<--------------------------|                            |
       |                           |                            |
       |                           | If Valid Format            |
       |                           |------------+               |
       |                           |            |               |
       |                           |<-----------+               |
       |                           |                            |
       |                           | Check Credentials          |
       |                           |--------------------------->|
       |                           |                            |
       |                           |     Authentication Result  |
       |                           |<---------------------------|
       |                           |                            |
       |                           | If Invalid Credentials     |
       |                           |------------+               |
       |                           |            |               |
       |                           |<-----------+               |
       |                           |                            |
       |  Display Authentication   |                            |
       |  Error                    |                            |
       |<--------------------------|                            |
       |                           |                            |
       |                           | If Valid Credentials       |
       |                           |------------+               |
       |                           |            |               |
       |                           |<-----------+               |
       |                           |                            |
       |                           | Generate JWT Token         |
       |                           |------------+               |
       |                           |            |               |
       |                           |<-----------+               |
       |                           |                            |
       |                           | Log User Login Activity    |
       |                           |--------------------------->|
       |                           |                            |
       |                           |     Confirmation           |
       |                           |<---------------------------|
       |                           |                            |
       |                           | Get User Role & Permissions|
       |                           |--------------------------->|
       |                           |                            |
       |                           |     User Data              |
       |                           |<---------------------------|
       |                           |                            |
       |  Set JWT Token in         |                            |
       |  HTTP-only Cookie or      |                            |
       |  Local Storage            |                            |
       |<--------------------------|                            |
       |                           |                            |
       |  Redirect to Role-Based   |                            |
       |  Dashboard                |                            |
       |<--------------------------|                            |
       |                           |                            |
       | Access Protected Resource |                            |
       |-------------------------->|                            |
       |                           |                            |
       |                           | Verify JWT Token           |
       |                           |------------+               |
       |                           |            |               |
       |                           |<-----------+               |
       |                           |                            |
       |                           | If Token Invalid/Expired   |
       |                           |------------+               |
       |                           |            |               |
       |                           |<-----------+               |
       |                           |                            |
       |  Redirect to Login Page   |                            |
       |<--------------------------|                            |
       |                           |                            |
       |                           | If Token Valid             |
       |                           |------------+               |
       |                           |            |               |
       |                           |<-----------+               |
       |                           |                            |
       |                           | Check Role-Based           |
       |                           | Authorization              |
       |                           |------------+               |
       |                           |            |               |
       |                           |<-----------+               |
       |                           |                            |
       |                           | If Not Authorized          |
       |                           |------------+               |
       |                           |            |               |
       |                           |<-----------+               |
       |                           |                            |
       |  Display Access Denied    |                            |
       |<--------------------------|                            |
       |                           |                            |
       |                           | If Authorized              |
       |                           |------------+               |
       |                           |            |               |
       |                           |<-----------+               |
       |                           |                            |
       |  Return Requested         |                            |
       |  Resource                 |                            |
       |<--------------------------|                            |
       |                           |                            |
       | Select Logout             |                            |
       |-------------------------->|                            |
       |                           |                            |
       |                           | Invalidate Token           |
       |                           |------------+               |
       |                           |            |               |
       |                           |<-----------+               |
       |                           |                            |
       |                           | Log User Logout            |
       |                           |--------------------------->|
       |                           |                            |
       |                           |     Confirmation           |
       |                           |<---------------------------|
       |                           |                            |
       |  Clear Token from Client  |                            |
       |<--------------------------|                            |
       |                           |                            |
       |  Redirect to Login Page   |                            |
       |<--------------------------|                            |
       |                           |                            |
       v                           v                            v
```

## Authentication Process Explanation

### 1. Login Process
1. **User** accesses the login page of the ExamExpert-AI system.
2. **System** displays the login form.
3. **User** enters their credentials (email and password).
4. **System** performs input validation on the client-side:
   - Checks if email format is valid
   - Ensures password field is not empty
5. If the input format is invalid, the **System** displays appropriate error messages.
6. If the input format is valid, the **System** sends the credentials to the server for authentication.
7. **System** checks the credentials against the database.
8. If credentials are invalid, the **System** displays an authentication error message.

### 2. Authentication and Authorization
1. If credentials are valid, the **System** generates a JSON Web Token (JWT) containing:
   - User ID
   - User role (admin, teacher, or student)
   - Expiration time
   - Other necessary claims
2. **System** logs the user login activity in the database for audit purposes.
3. **System** retrieves the user's role and permissions from the database.
4. **System** sets the JWT token in an HTTP-only cookie or local storage (based on security configuration).
5. **System** redirects the user to their role-specific dashboard:
   - Admin dashboard for admin users
   - Teacher dashboard for teacher users
   - Student dashboard for student users

### 3. Accessing Protected Resources
1. When the **User** attempts to access a protected resource or API endpoint.
2. **System** verifies the JWT token:
   - Checks token signature
   - Verifies token has not expired
   - Validates token claims
3. If the token is invalid or expired, the **System** redirects the user to the login page.
4. If the token is valid, the **System** checks if the user's role has permission to access the requested resource.
5. If the user is not authorized, the **System** displays an access denied message.
6. If the user is authorized, the **System** returns the requested resource.

### 4. Logout Process
1. **User** selects the logout option.
2. **System** invalidates the JWT token.
3. **System** logs the user logout activity in the database.
4. **System** clears the token from the client (cookie or local storage).
5. **System** redirects the user to the login page.

## Security Considerations
- JWT tokens are signed with a secure secret key
- Passwords are stored using bcrypt hashing
- HTTP-only cookies are used to prevent XSS attacks
- CSRF protection is implemented for form submissions
- Rate limiting is applied to prevent brute force attacks
- Token expiration ensures sessions don't remain valid indefinitely
