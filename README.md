# AuthService Documentation

## Overview

The `AuthService` is a core service in our Angular application responsible for managing user authentication and authorization processes. It provides a set of methods for logging in, registering, resetting passwords, changing passwords, fetching user details, and more. This service interacts with the backend API to perform these operations and manages the user session state locally.

## Dependencies

- Angular Core
- RxJS
- Angular Common HTTP Client
- jwt-decode

## Interfaces Used

- `LoginRequest`
- `RegisterRequest`
- `ResetPasswordRequest`
- `ChangePasswordRequest`
- `AuthResponse`
- `UserDetail`

## Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/felixojiambo/AuthenticationAuthorisationAngular.git
   ```
2. Navigate to the project directory:
   ```bash
   cd AuthenticationAuthorisationAngular
   ```
3. Install the dependencies:
   ```bash
   npm install
   ```

## Configuration

Ensure the `environment.ts` file is correctly configured with the API URL:
```typescript
export const environment = {
  production: false,
  apiUrl: 'http://localhost:5000/api/'
};
```

## Usage

### Constructor Injection

Inject `AuthService` into any component or service that requires authentication functionality.

```typescript
constructor(private authService: AuthService) {}
```

### Authentication Methods

#### Login

Logs in a user with provided credentials.

```typescript
const loginData: LoginRequest = { email: 'user@example.com', password: 'password123' };
this.authService.login(loginData).subscribe(response => {
  // Handle successful login
});
```

#### Register

Registers a new user with provided details.

```typescript
const registerData: RegisterRequest = { email: 'user@example.com', password: 'password123', fullName: 'John Doe' };
this.authService.register(registerData).subscribe(response => {
  // Handle successful registration
});
```

#### Forgot Password

Sends a password reset link to the specified email.

```typescript
const email = 'user@example.com';
this.authService.forgotPassword(email).subscribe(response => {
  // Handle password reset request
});
```

#### Reset Password

Resets the user's password based on the received token.

```typescript
const resetData: ResetPasswordRequest = { token: 'reset-token', password: 'newpassword123' };
this.authService.resetPassword(resetData).subscribe(response => {
  // Handle password reset
});
```

#### Change Password

Allows the authenticated user to change their password.

```typescript
const changeData: ChangePasswordRequest = { currentPassword: 'oldpassword123', newPassword: 'newpassword123' };
this.authService.changePassword(changeData).subscribe(response => {
  // Handle password change
});
```

### Session Management

#### Get User Detail

Retrieves detailed information about the currently logged-in user.

```typescript
const userDetails = this.authService.getUserDetail();
```

#### Is Logged In

Checks if the user is currently logged in.

```typescript
const loggedIn = this.authService.isLoggedIn();
```

#### Logout

Logs out the current user, clearing the local storage.

```typescript
this.authService.logout();
```

#### Refresh Token

Refreshes the user's authentication token.

```typescript
const refreshData = { email: 'user@example.com', token: 'current-token', refreshToken: 'refresh-token' };
this.authService.refreshToken(refreshData).subscribe(response => {
  // Handle token refresh
});
```

### Utility Methods

#### Get Token

Retrieves the current user's authentication token.

```typescript
const token = this.authService.getToken();
```

#### Get Refresh Token

Retrieves the current user's refresh token.

```typescript
const refreshToken = this.authService.getRefreshToken();
```

## Security Considerations

- Tokens are stored in `localStorage`, which may have security implications. Consider using HttpOnly cookies for production environments.
- Always validate tokens on the server side before trusting them.
- Implement proper error handling to manage failed authentication attempts gracefully.

## Contributing

Contributions to the `AuthService` are welcome. Please review the existing codebase and submit pull requests for enhancements or bug fixes.
