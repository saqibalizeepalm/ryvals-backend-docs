# Documentation for `auth_views.py` 🛡️

## Overview

The `auth_views.py` file contains the implementation of Django REST Framework API views focused on authentication and activity logging for Ryvals Admins. These views facilitate various operations such as sign-in, sign-out, password change, and viewing activity logs. The file leverages Django's class-based generic views to streamline the creation of RESTful API endpoints.

## Index

- **SignIn**: API view for admin sign-in.
- **SignOut**: API view for admin sign-out.
- **ChangePasswordView**: API view for changing admin password.
- **ForgotPassword**: API view for handling forgot password requests.
- **ListAllActivityLogs**: API view for listing all user activity logs.
- **ListAllActivityEvent**: API view for listing all activity event log actions.

## Detailed Descriptions

### SignIn

- **Purpose**: Allows Ryvals Admins to sign in to the system.
- **HTTP Method**: POST
- **Serializer**: `LoginAdminSerializer`
- **Description**: This view handles the authentication process by verifying admin credentials using the `LoginAdminSerializer`. Upon successful authentication, it generates and returns an access token for the session.

### SignOut

- **Purpose**: Allows Ryvals Admins to sign out of the system.
- **HTTP Method**: UPDATE
- **Serializer**: `SignOutUserSerializer`
- **Permissions**: 
  - `PrivateTokenAccessPermission`
  - `IsAnyRyvalsAdmin`
- **Description**: This view facilitates the logout process for admins. It accesses the current authentication token to invalidate it and logs the logout event using the `Logs` model.

### ChangePasswordView

- **Purpose**: Enables Ryvals Admins to change their password.
- **HTTP Method**: UPDATE
- **Serializer**: `ChangePasswordSerializer`
- **Permissions**: 
  - `PrivateTokenAccessPermission`
  - `IsAnyRyvalsAdmin`
  - `IsActivated`
- **Description**: This view allows admins to update their password. It ensures that the admin is authenticated and has the necessary permissions to perform this action.

### ForgotPassword

- **Purpose**: Handles requests for password recovery.
- **HTTP Method**: POST
- **Serializer**: `ForgotPasswordSerializer`
- **Description**: Admins can request a password reset through this view, which processes the request and sends a reset link to the admin's registered email.

### ListAllActivityLogs

- **Purpose**: Provides a list of all user activity logs for admins.
- **HTTP Method**: GET
- **Permissions**:
  - `PrivateTokenAccessPermission`
  - `IsAnyRyvalsAdmin`
  - `IsActivated`
  - `CustomDjangoModelPermissions`
- **Serializer**: `ListAllActivityLogsSerializer`
- **Pagination**: `StandardPagination`
- **Query Parameters**: Filters such as `from_date`, `to_date`, `date`, `event`, `order`, and `type_` can be applied.
- **Description**: This view offers a comprehensive list of user activities, allowing filtering based on various parameters like date range and event type. It uses pagination for efficient data handling.

### ListAllActivityEvent

- **Purpose**: Lists all possible activity log events.
- **HTTP Method**: GET
- **Serializer**: `ListActivityLogEventSerializer`
- **Description**: This view provides a list of all defined activity log events, facilitating an understanding of potential actions logged within the system.

## Usage Example

Here's a sample request to access the sign-in endpoint:

```bash
POST /api_admin_v1/login/
{
    "email": "admin@example.com",
    "password": "adminpassword123"
}
```

## Conclusion

The `auth_views.py` module is essential for managing authentication and activity logging for Ryvals Admins. It ensures secure access and provides valuable insights into user activities through comprehensive logging capabilities.