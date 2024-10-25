# 📚 API Accounts V1: Django URL Configuration Documentation

Welcome to the documentation for the `urls.py` file, which serves as the URL configuration for the `api_accounts_v1` Django application. This document details each URL pattern, its associated view, and the purpose it serves within the application. This setup is essential for routing HTTP requests to the appropriate views in the Django Rest Framework.

## Index
1. [Overview](#overview)
2. [URL Patterns](#url-patterns)
   - [Sign Up](#sign-up)
   - [Log In](#log-in)
   - [Log Out](#log-out)
   - [Account Verification](#account-verification)
   - [Forgot Password](#forgot-password)
   - [Forgot Password Activation](#forgot-password-activation)
   - [Reset Password](#reset-password)
   - [Change Password](#change-password)
   - [Resend Verification Email](#resend-verification-email)
   - [New Access Token](#new-access-token)
   - [Forgot Username](#forgot-username)
   - [Social Login](#social-login)
   - [Twitter Authorization](#twitter-authorization)

## Overview

The `urls.py` file in Django works as a routing table. It maps URL patterns to view functions, which handle the logic for each route. In this file, we use Django's `path` function to define URL patterns that are linked to their respective class-based views from the `accounts.api.views` module.

## URL Patterns

Below is a table of the URL patterns defined in the `urls.py` file, including descriptions and their associated views:

| URL Pattern                      | View Class                            | Description                                                                 |
|----------------------------------|---------------------------------------|-----------------------------------------------------------------------------|
| `/api/v1/accounts/signup/`       | `SignUp`                              | Endpoint for user registration.                                             |
| `/api/v1/accounts/login/`        | `SignIn`                              | Endpoint for user login.                                                    |
| `/api/v1/accounts/logout/`       | `SignOut`                             | Endpoint for logging out the user.                                          |
| `/api/v1/accounts/verification`  | `AccountVerification`                 | Endpoint for verifying user accounts.                                       |
| `/api/v1/accounts/forgot-password/` | `ForgotPassword`                   | Endpoint for initiating the password reset process.                         |
| `/api/v1/accounts/forgot-password-activation/` | `ForgotPasswordActivation` | Endpoint for validating token for password reset.                           |
| `/api/v1/accounts/reset-password/` | `ResetPassword`                     | Endpoint for resetting the user's password.                                 |
| `/api/v1/accounts/change-password/` | `ChangePasswordView`               | Endpoint for changing the user's password.                                  |
| `/api/v1/accounts/resend-verification-email/` | `ResendAccountVerificationEmailAPIView` | Endpoint to resend account verification email.               |
| `/api/v1/accounts/token/`        | `NewAccessToken`                      | Endpoint for obtaining a new access token using a refresh token.            |
| `/api/v1/accounts/forgot-username/` | `ForgotUsername`                  | Endpoint for retrieving a forgotten username.                               |
| `/api/v1/accounts/social-login/` | `SocialLoginAPIView`                  | Endpoint for logging in via social media accounts.                          |
| `/api/v1/accounts/twitter-auth/` | `TwitterAuthorizationAPIView`         | Endpoint for Twitter account authorization.                                 |

### Sign Up
- **Path**: `/signup/`
- **View**: `SignUp`
- **Description**: Handles the creation of new user accounts.

### Log In
- **Path**: `/login/`
- **View**: `SignIn`
- **Description**: Manages user authentication and session creation.

### Log Out
- **Path**: `/logout/`
- **View**: `SignOut`
- **Description**: Logs out the user by terminating their session.

### Account Verification
- **Path**: `/verification`
- **View**: `AccountVerification`
- **Description**: Validates and confirms user account registration through email verification.

### Forgot Password
- **Path**: `/forgot-password/`
- **View**: `ForgotPassword`
- **Description**: Initiates the password reset process by sending a reset link to the user's email.

### Forgot Password Activation
- **Path**: `/forgot-password-activation/`
- **View**: `ForgotPasswordActivation`
- **Description**: Validates the password reset token to ensure it's not expired or invalid.

### Reset Password
- **Path**: `/reset-password/`
- **View**: `ResetPassword`
- **Description**: Allows users to set a new password using a valid reset token.

### Change Password
- **Path**: `/change-password/`
- **View**: `ChangePasswordView`
- **Description**: Enables logged-in users to change their current password.

### Resend Verification Email
- **Path**: `/resend-verification-email/`
- **View**: `ResendAccountVerificationEmailAPIView`
- **Description**: Resends the email verification link if the user did not receive it or it expired.

### New Access Token
- **Path**: `/token/`
- **View**: `NewAccessToken`
- **Description**: Issues a new access token using a refresh token to maintain the user's session.

### Forgot Username
- **Path**: `/forgot-username/`
- **View**: `ForgotUsername`
- **Description**: Helps users retrieve their forgotten username via email.

### Social Login
- **Path**: `/social-login/`
- **View**: `SocialLoginAPIView`
- **Description**: Facilitates user login through social media providers like Facebook, Google, etc.

### Twitter Authorization
- **Path**: `/twitter-auth/`
- **View**: `TwitterAuthorizationAPIView`
- **Description**: Handles the OAuth process for Twitter integration, allowing users to authenticate via Twitter.

---

This concludes the documentation for the `urls.py` file in the `api_accounts_v1` application. Each URL pattern is strategically mapped to its respective view to handle specific functionalities related to user accounts, enhancing the overall user authentication and authorization workflow.