# Documentation for `messages.py` 📜

The `messages.py` file in a Django project is typically used to store user-facing messages and error notifications that can be utilized throughout the application. This file contains a set of constants that are translated using Django's translation system, making it easier to support multiple languages. Each message is defined with a unique identifier that can be used in the application code to provide feedback to the user.

## Table of Contents 📑

1. [Introduction](#introduction)
2. [Purpose and Usage](#purpose-and-usage)
3. [Message List](#message-list)
4. [Translation](#translation)

---

## Introduction

The `messages.py` file leverages Django's `gettext_lazy` for translation purposes, allowing messages to be marked for translation. This is particularly useful in applications that need to support multiple languages, as it separates the content from the code logic.

## Purpose and Usage 🎯

- **Centralized Management**: All user-facing messages are managed in one place for easy updates and consistency across the application.
- **Localization and Internationalization**: Using `gettext_lazy`, these messages can be translated into different languages, which is crucial for applications aiming for a global audience.
- **Code Readability**: By using descriptive constants, the code becomes more readable and maintainable.

## Message List 📜

Here is a detailed list of messages included in the file with their descriptions:

| **Constant Name**                      | **Message**                                                         | **Description**                                  |
|----------------------------------------|---------------------------------------------------------------------|--------------------------------------------------|
| `LINK_EXPIRED`                         | "Link has expired"                                                  | Indicates that a link has expired.               |
| `LOGIN_SUCCESS`                        | "You are logged in"                                                 | Shown when login is successful.                  |
| `LOGGED_OUT`                           | "Logged out successfully"                                           | Shown when user logs out.                        |
| `LOGOUT_SUCCESS`                       | "Logged out successfully"                                           | Another message for successful logout.           |
| `TEXT_OR_HTML_REQUIRED`                | "Text or HTML required"                                             | Error when text or HTML is needed but missing.   |
| `NAME_ERROR`                           | "Name must contain only alphabets"                                  | Error for invalid name format.                   |
| `USER_LOGGEDIN_SUCCESSFULLY`           | "You are logged in"                                                 | Indicates successful user login.                 |
| `PASSWORD_RESET`                       | "New password set successfully"                                     | Shown after a password reset.                    |
| `SUBJECT_RESET_PASSWORD`               | "Password Reset Request"                                            | Email subject for password reset.                |
| `PASSWORD_MISMATCH`                    | "Both passwords should match"                                       | Error when passwords do not match.               |
| `PROFILE_NOT_FOUND`                    | "User profile does not exists"                                      | Error when a user profile is not found.          |
| `EMAIL_UNREGISTERED`                   | "Could not find your account"                                       | Error when email is not registered.              |
| `EMAIL_ALREADY_REGISTERED`             | "This email is already in use"                                      | Error for duplicate email registration.          |
| `USERNAME_ALREADY_EXISTS`              | "This username is already in use"                                   | Error for duplicate username.                    |
| `USER_ACCOUNT_NOT_ACTIVE`              | "Please complete the sign up process"                               | Notification for inactive account.               |
| `PASSWORD_RESET_SUCCESS`               | "Password has been reset successfully"                              | Shown after a successful password reset.         |
| `USERNAME_RESET_SUCCESS`               | "Username has been reset successfully"                              | Shown after a successful username reset.         |
| `INVALID_EMAIL_FORMAT`                 | "Please enter the email in a valid format"                          | Error for invalid email format.                  |
| `VERIFICATION_MAIL_SENT`               | "Account verification mail has been sent"                           | Notification for sent verification email.        |
| `UNDER_EIGHTEEN`                       | "You are not eligible To Sign Up for Ryvals at this time because you are under 18" | Age restriction message.                      |
| `MIN_MAX_DATE`                         | "The Date of Birth should be greater than or equal to 1990-01-01"   | Date of birth validation message.                |
| `ALREADY_REGISTERED_USER`              | "An account with this email already exists. Try again or Sign in"   | Error for already registered users.              |
| `PHONE_REGEX_ERROR`                    | "Please enter a valid phone number. Only +14444888333 formats are accepted" | Error for invalid phone number format.  |
| `ERROR_PASSWORD_RESET`                 | "An error occurred while trying to reset the password. Please try again" | Error during password reset process.    |
| `ERROR_USERNAME_RESET`                 | "An error occurred while trying to reset the username. Please try again" | Error during username reset process.    |
| `INVALID_REF_CODE`                     | "Entered referral code is invalid"                                  | Error for invalid referral code.                 |
| `SUBJECT_USER_FEEDBACK`                | "User Feedback"                                                     | Subject line for user feedback emails.           |
| `SAME_PASSWORD_MISMATCH`               | "New password cannot be the same as current password. Please try again" | Error when new and old passwords match.   |
| `FORGOT_PASSWORD_RESET_FAIL`           | "Unable to reset password. This link has been expired or not exist" | Error when password reset link is invalid.       |
| `FORGOT_PASSWORD_EMAIL_SENT`           | "You will receive an email with instructions to reset your password" | Notification for sent password reset email.  |
| `ACCOUNT_UNVERIFIED`                   | "Your email is not verified. Please check your email to verify your email" | Message for unverified email accounts.   |
| `INVALID_PASSWORD_FORMAT`              | "Password allows 8-15 alphanumeric characters with at-least one special character" | Password format validation message.   |
| `SIGNUP_SUCCESS`                       | "Thank you for signing up an account with us. Please check the email to verify your account" | Successful signup message.          |
| `DEACTIVATED_USER`                     | "Your account has been deactivated. Please contact Ryvals Support." | Notification for deactivated account.           |
| `LOGIN_AUTHENTICATION_INVALID`         | "The email/username and password combination you entered is not correct. Please try again" | Login error for invalid credentials. |
| `USERNAME_CONTAINS_PROFANITY`          | "This username contains profanity. Please choose another username to continue signing up" | Error for inappropriate username.  |
| `EMAIL_USERNAME_REQUIRED`              | "Please provide an email/username to login"                         | Error when email or username is missing.        |
| `SUPER_ADMIN_NOT_ALLOWED`              | "Super admin access is not allowed. Please contact admin"           | Restriction message for super admin access.     |
| `VERIFICATION_COMPLETE`                | "Your account has been verified. Please proceed to login"           | Successful verification message.                |
| `INVALID_LINK`                         | "The link is invalid"                                               | Error for invalid link.                         |
| `CONFIRM_PASSWORD_REQUIRED`            | "Please confirm password"                                           | Error when password confirmation is missing.    |
| `INVALID_USERNAME_FORMAT`              | "Please enter the username in a valid format"                       | Error for invalid username format.              |
| `UNEXPECTED_ERROR`                     | "We have experienced an unexpected error. Please contact us at support@ryvals.com" | General unexpected error message.   |
| `SOCIAL_ACCOUNT_NOT_FOUND`             | "This %(provider)s account is not linked to a Ryvals account"       | Error when social account is not linked.        |
| `STRIPE_ACCOUNT_NOT_FOUND`             | "Stripe account not found."                                         | Error for missing Stripe account.               |
| `ACCOUNT_DEACTIVATED`                  | "Your account has been locked as you have reached the maximum number of OTPs/mails. Please contact Ryvals Support." | Lockout message for reaching OTP/mail limit.    |
| `INVALID_USERNAME_EMAIL_FORMAT`        | "Please enter the username/email in a valid format"                 | Error for invalid username/email format.        |
| `INVALID_FIRSTNAME_FORMAT`             | "Please enter valid first name"                                     | Error for invalid first name format.            |
| `INVALID_LASTNAME_FORMAT`              | "Please enter valid last name"                                      | Error for invalid last name format.             |

## Translation 🌍

All messages are wrapped in Django's `gettext_lazy` function, which marks them for translation. This allows the application to provide these messages in different languages, depending on the user's locale settings.

```python
from django.utils.translation import gettext_lazy as _

LINK_EXPIRED = _('Link has expired')
```

By using this approach, developers can easily manage translations in Django applications using standard `.po` and `.mo` files. This makes it easier to maintain and update translations as the application grows or changes.

---

This documentation provides an overview and detailed descriptions of the messages defined in `messages.py`. Utilizing such a centralized file for messages ensures consistency and aids in the localization process of a Django application.