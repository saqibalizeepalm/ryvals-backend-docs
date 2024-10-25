# File Documentation: `account_helpers.py`

## Overview
The `account_helpers.py` file is a utility module designed to facilitate account-related operations, specifically focusing on sending account activation tokens via email. This file contains a class with a method to generate and send verification emails to users during the account activation process.

## Table of Contents
1. [Classes](#classes)
    - [AccountHelper](#accounthelper)
2. [Functions](#functions)
    - [send_activation_token](#send_activation_token)

## Classes

### AccountHelper
The `AccountHelper` class serves as a collection of static helper methods related to account operations. It currently provides functionality to handle the creation and sending of account activation tokens.

## Functions

### send_activation_token

```python
@staticmethod
def send_activation_token(request, user):
    token_link = UserSecurityToken.create_activation_token(user.email, user)
    token_link.send_verify_token_email(request, True)
```

#### Description
- **Purpose**: The `send_activation_token` static method is responsible for generating an activation token for a user and sending it via email to verify the user's account.
- **Arguments**:
  - `request`: The HTTP request object that contains metadata about the request.
  - `user`: The user object for whom the activation token is to be generated and sent.
- **Functionality**:
  - Calls `UserSecurityToken.create_activation_token` to generate a unique activation token associated with the user's email.
  - Utilizes the `send_verify_token_email` method of the `UserSecurityToken` class to send the activation email to the user, including the generated token in the email.
  
#### Usage
This function is typically called during the user registration process to ensure that the email provided by the user is valid and belongs to them. It helps in confirming the user's email address before granting full access to the application. 

## Summary
The `account_helpers.py` file simplifies the process of sending account activation emails by abstracting the logic into a reusable static method. It leverages the `UserSecurityToken` model and its associated methods to handle the creation and dispatching of verification emails. This utility is crucial for maintaining a secure and reliable user registration process.