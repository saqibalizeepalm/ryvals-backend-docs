# 📜 `utils.py` Documentation

This document provides an in-depth explanation of the `utils.py` file, which contains utility methods and classes that are essential for various operations within the application. These utilities include validation functions, token management, and data manipulation tools.

---

## 📋 Table of Contents

1. [Overview](#overview)
2. [Classes and Methods](#classes-and-methods)
   - [UserAccessToken](#useraccesstoken)
   - [UtilityMethods](#utilitymethods)
3. [Utility Functions](#utility-functions)
4. [Code Snippets](#code-snippets)
5. [External Libraries](#external-libraries)

---

## Overview

The `utils.py` file is a collection of helper functions and classes that streamline the operations of user authentication, data validation, and utility functions across the application. By centralizing these functions, the codebase becomes cleaner and more maintainable.

---

## Classes and Methods

### UserAccessToken

This class is responsible for handling OAuth2 token management for users. It provides methods to create and revoke access tokens associated with user sessions.

**Methods:**

- **`__init__(self, request, user, app_name)`**: Initializes the UserAccessToken with the request, user, and application name.
- **`create_oauth_token(self)`**: Generates and returns OAuth2 access and refresh tokens for a user.
- **`revoke_oauth_tokens(self)`**: Revokes existing OAuth tokens, effectively logging out the user from all sessions.

### UtilityMethods

A static class offering a variety of utility functions used throughout the application.

**Key Methods:**

- **Validation Methods**: Functions like `is_char_only`, `is_alphanumeric`, `is_valid_email`, `is_valid_password`, etc., are used to validate different types of input data.
- **Token and OTP Methods**: Includes `generate_random_password`, `generate_otp`, and `if_otp_mail_already_sent` to handle secure token generation and OTP validation.
- **Date and Time Methods**: Functions like `get_utc_datetime_from_date_string` and `get_standard_date_time_string_from_datetime_object` for handling datetime operations.
- **Network and Security Methods**: `vpn_is_enabled` and `user_current_location` check if a user is using a VPN and fetches user location based on IP.
- **Messaging and Notification Methods**: Includes `send_message` and `send_email_to_user` for user communication via SMS and email.

---

## Utility Functions

These utility functions provide an array of operations such as generating random values, validating user inputs, and interacting with external APIs like Google reCAPTCHA and Twilio.

- **`generate_random_password()`**: Creates a secure random password for admin users.
- **`generate_otp()`**: Generates a six-digit OTP for user verification.
- **`send_message(user, message, new_number=None)`**: Sends a text message to the user via Twilio.
- **`google_recaptcha_verify(captcha)`**: Verifies Google's reCAPTCHA to ensure the request is human-made.

---

## Code Snippets

Here's a quick example of how one might use the `UserAccessToken` class:

```python
user_access_token = UserAccessToken(request, user, "MyApp")
tokens = user_access_token.create_oauth_token()
print("Access Token:", tokens['access_token'])
print("Refresh Token:", tokens['refresh_token'])
```

And an example of using a utility method:

```python
if UtilityMethods.is_valid_email("example@example.com"):
    print("Valid email address!")
else:
    print("Invalid email address.")
```

---

## External Libraries

The `utils.py` file relies on several external libraries to function:

- **`pytz`**: For timezone-related operations.
- **`boto3`**: For AWS S3 interactions.
- **`requests`**: For making HTTP requests.
- **`twilio`**: For sending SMS messages.
- **`oauth2_provider`**: For handling OAuth2 tokens.

These libraries provide robust tools for handling complex operations like timezone conversions, secure random number generation, and HTTP requests.

---

This documentation should provide a comprehensive understanding of the `utils.py` file, aiding both new and existing developers in navigating and utilizing the utilities effectively. 🎉