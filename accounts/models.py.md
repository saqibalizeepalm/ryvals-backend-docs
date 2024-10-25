# Documentation for `models.py` File 📄

Welcome to the comprehensive documentation of the `models.py` file. This file defines the database models and structures used in your Django application related to user management, profiles, and security tokens. Below, you'll find a detailed breakdown of the code, its purpose, and how it fits into the broader application. Let's dive in! 🌊

## Table of Contents 📚

1. [Introduction](#introduction)
2. [User Management](#user-management)
   - [UserManager Class](#usermanager-class)
   - [User Class](#user-class)
   - [RyvalsAdmin Class](#ryvalsadmin-class)
   - [Player Class](#player-class)
3. [Profile Management](#profile-management)
   - [Profile Class](#profile-class)
   - [ReferralReport Class](#referralreport-class)
4. [Social Media Integration](#social-media-integration)
   - [SocialMediaModel Class](#socialmediamodel-class)
   - [UserSocialMediaAccountModel Class](#usersocialmediaaccountmodel-class)
5. [Security Tokens](#security-tokens)
   - [UserSecurityToken Class](#usersecuritytoken-class)
6. [Conclusion](#conclusion)

## Introduction

This file is a crucial component of your Django application, connecting your application logic to the database through Django's ORM (Object-Relational Mapping). It defines several models that represent the structure of your database tables, user roles, status, and various functionalities like email verification and password reset.

## User Management

### UserManager Class

The **UserManager** class is a custom manager for handling user creation with specific requirements such as email normalization and password setup.

- **Methods**:
  - `create_user`: Used to create a regular user with email verification and password hashing.
  - `create_superuser`: Used to create a superuser with elevated privileges.

```python
class UserManager(BaseUserManager):
    def create_user(self, **kwargs):
        # Code for user creation
```

### User Class

The **User** class extends `AbstractBaseUser` and `PermissionsMixin`, providing a flexible user model with fields like `first_name`, `last_name`, `email`, `username`, and more. It includes roles and statuses as inner classes for better management.

- **Roles**:
  - Django Super Admin
  - Ryvals Super Admin
  - Ryvals Admin Levels 1-3
  - Player

- **Status**:
  - Activated
  - Deactivated

```python
class User(AbstractBaseUser, PermissionsMixin, TimeStampModel):
    class Role(models.IntegerChoices):
        # Role definitions
```

### RyvalsAdmin Class

The **RyvalsAdmin** class is a proxy model that filters users who have administrative roles within the Ryvals platform.

```python
class RyvalsAdmin(User):
    objects = RyvalsAdminManager()
    # Meta and other configurations
```

### Player Class

The **Player** class is another proxy model catering to users with a player role. It is managed by the **PlayerManager**.

```python
class Player(User):
    objects = PlayerManager()
    # Meta and other configurations
```

## Profile Management

### Profile Class

The **Profile** class is linked to the `User` model using a one-to-one relationship. It includes fields for verification, social media IDs, wallet balances, and various settings.

```python
class Profile(TimeStampModel):
    user = models.OneToOneField(settings.AUTH_USER_MODEL, on_delete=models.CASCADE, related_name='profile')
    # Other fields and configurations
```

### ReferralReport Class

The **ReferralReport** class tracks referral activities and earnings between users.

```python
class ReferralReport(TimeStampModel):
    referee = models.ForeignKey(settings.AUTH_USER_MODEL, on_delete=models.CASCADE, null=True, blank=True, related_name='referee_by')
    # Other fields and configurations
```

## Social Media Integration

### SocialMediaModel Class

This class represents various social media platforms integrated into the application, storing client IDs and secrets.

```python
class SocialMediaModel(TimeStampModel):
    name = models.CharField(_('Name'), max_length=20)
    # Other fields and configurations
```

### UserSocialMediaAccountModel Class

This model acts as a junction table between users and their social media accounts.

```python
class UserSocialMediaAccountModel(TimeStampModel):
    user = models.ForeignKey(settings.AUTH_USER_MODEL, on_delete=models.CASCADE, related_name='user_social_account')
    # Other fields and configurations
```

## Security Tokens

### UserSecurityToken Class

The **UserSecurityToken** model manages security tokens related to password resets, account activations, and other secure actions.

- **Methods**:
  - `create_token`: Generates a new token with an expiration date.
  - `send_verify_token_email`: Sends an email with a verification link.
  - `send_forgot_auth_email`: Sends emails for password or username recovery.

```python
class UserSecurityToken(TimeStampModel):
    user = models.ForeignKey(User, on_delete=models.CASCADE, null=True, blank=True, related_name='tokens')
    # Other fields and configurations

    def send_verify_token_email(self, request, resend=None):
        # Email sending logic
```

## Conclusion

This `models.py` file serves as a backbone for user management and authentication in your Django application. It provides structured data representation for users, profiles, and security mechanisms, ensuring robust and scalable functionality. Each model is meticulously designed to handle specific aspects of the application, making it an integral part of the overall system architecture. 🌟

Feel free to refer to this documentation as you navigate and expand the functionalities of your application! 🛠️