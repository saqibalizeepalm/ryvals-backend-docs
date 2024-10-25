# `admin_serializers.py` Documentation

This file contains serializer classes used within the context of handling administrative tasks for the Ryvals platform. The serializers are part of the Django Rest Framework (DRF) and facilitate the conversion between complex data types, like querysets, and native Python data types, which can then be easily rendered into JSON or other content types.

---

## Table of Contents
1. [Imports](#imports)
2. [Serializer Classes](#serializer-classes)
   - [LoginAdminSerializer](#loginadminserializer)
   - [ForgotPasswordSerializer](#forgotpasswordserializer)
   - [ListAllActivityLogsSerializer](#listallactivitylogsserializer)
   - [ListActivityLogEventSerializer](#listactivitylogeventserializer)

---

## Imports

```python
import pytz
from django.contrib import auth
from app.utils import UtilityMethods
from accounts.models import UserSecurityToken
from rest_framework import serializers, status
from django.contrib.auth import get_user_model
from nimda.models import Logs, ActivityEventLog
from rest_framework.exceptions import APIException
from django.contrib.auth.models import Group, Permission
from accounts.api.serializers import UserDetailSerializer
from django.contrib.contenttypes.models import ContentType
from nimda.api.serializers.user_serializers import PermissionSerializer
from accounts.api.serializers import (LoginSerializer, ForgotAuthFunctionalitySerializer)
from accounts.messages import (DEACTIVATED_USER, EMAIL_USERNAME_REQUIRED, FORGOT_PASSWORD_EMAIL_CONFIRMATION, LOGIN_AUTHENTICATION_INVALID, EMAIL_UNREGISTERED, USER_LOGGEDIN_SUCCESSFULLY, INVALID_EMAIL_FORMAT, VERIFICATION_PENDING, ACCOUNT_DEACTIVATED, INVALID_USERNAME_EMAIL_FORMAT)
```

- **pytz**: For timezone conversions.
- **Django/Auth Imports**: For handling authentication and permissions.
- **Django Rest Framework (DRF) Imports**: For creating API serializers.
- **Custom Imports**: Models, serializers, and utility methods specific to the application.

---

## Serializer Classes

### LoginAdminSerializer

- **Purpose**: Handles the login process for Ryvals admin users.
- **Inherits**: `LoginSerializer`
- **Key Methods**:
  - `get_user(email_username)`: Fetches the user based on email or username.
  - `validate(validated_data)`: Validates the user credentials.
  - `data`: Returns the serialized user data including access and refresh tokens.

```python
class LoginAdminSerializer(LoginSerializer):
    ''' Sign In Serializer for Ryvals Admins '''
    ...
    def get_user(self, email_username):
        ...
    def validate(self, validated_data):
        ...
    @property
    def data(self):
        ...
```

---

### ForgotPasswordSerializer

- **Purpose**: Facilitates the forgot password functionality for Ryvals admin users.
- **Inherits**: `ForgotAuthFunctionalitySerializer`
- **Key Methods**:
  - `validate(validated_data)`: Validates the provided email.
  - `create(validated_data)`: Sends a password reset token to the user's email.
  - `data`: Returns a confirmation message.

```python
class ForgotPasswordSerializer(ForgotAuthFunctionalitySerializer):
    ''' Forgot Password Serializer for Ryvals Admins '''
    ...
    def validate(self, validated_data):
        ...
    def create(self, validated_data):
        ...
    @property
    def data(self):
        ...
```

---

### ListAllActivityLogsSerializer

- **Purpose**: Provides an API view for Ryvals admins to view user activity logs.
- **Inherits**: `serializers.ModelSerializer`
- **Key Methods**:
  - `get_action_name(obj)`: Retrieves the action name from the logs.
  - `get_create_date(obj)`: Converts the creation date to a specific timezone.

```python
class ListAllActivityLogsSerializer(serializers.ModelSerializer):
    ''' Activity Logs API View for Ryvals Admins to view all users activity details '''
    ...
    def get_action_name(self, obj):
        ...
    def get_create_date(self, obj):
        ...
    class Meta:
        ...
```

---

### ListActivityLogEventSerializer

- **Purpose**: Gathers all activity log events.
- **Inherits**: `serializers.ModelSerializer`
- **Key Methods**:
  - `get_type(obj)`: Retrieves the label for the event type.
  - `get_events(obj)`: Compiles a list of events with their respective labels and IDs.

```python
class ListActivityLogEventSerializer(serializers.ModelSerializer):
    ''' API view for gather the all activity logs events '''
    ...
    def get_type(self, obj):
        ...
    def get_events(self, obj):
        ...
    class Meta:
        ...
```

---

This documentation provides an overview of the serializers defined in the `admin_serializers.py` file, highlighting their purpose, key functionalities, and method implementations. These serializers play a critical role in managing the administrative aspects of the Ryvals platform.