# 📄 `profile_serializers.py` Documentation

This file defines several serializers used for handling user profile-related data, particularly within the context of a gaming application. These serializers are primarily used for validating and processing data related to user profiles, game accounts, social media connections, and more. The serializers are built using Django's REST framework, and they facilitate interactions between the server and client applications, ensuring that data conforms to the expected formats and business logic.

## Table of Contents
1. [Imports](#imports)
2. [Utility Functions](#utility-functions)
3. [Serializers](#serializers)
   - [AddGameAccountSerializer](#addgameaccountserializer)
   - [EditGameAccountSerializer](#editgameaccountserializer)
   - [GameAccountSerializer](#gameaccountserializer)
   - [ProfileSerializer](#profileserializer)
   - [PlayerProfileDetailsSerializer](#playerprofiledetailsserializer)
   - [UpdatePlayerProfileSerializer](#updateplayerprofileserializer)
   - [RequestNewOTPSerializer](#requestnewotpserializer)
   - [UpdateProfileImageSerializer](#updateprofileimageserializer)
   - [UpdateProfileNotificationSerializer](#updateprofilenotificationserializer)
   - [UpdatePaypalIDSerializer](#updatepaypalidserializer)
   - [ReferFriendListSerializer](#referfriendlistserializer)
   - [LinkSocialAccountSerializer](#linksocialaccountserializer)
   - [DisconnectSocialAccountSerializer](#disconnectsocialaccountserializer)

---

## Imports

The file imports necessary modules and classes from Django, REST framework, and other utilities. Key imports include:
- `rest_framework.serializers`: Provides tools to serialize and deserialize data.
- `django.conf.settings`: Access to Django settings.
- `django.utils.translation`: Internationalization tools for translating strings.
- `app.utils.UtilityMethods`: Custom utility methods used throughout the serializers.
- Various models from `players`, `accounts`, `nimda`, and others.

## Utility Functions

### `get_conf_days(referee_user)`
Calculates the number of affiliate days based on the referee user's settings and a default configuration.

## Serializers

### AddGameAccountSerializer
- **Purpose**: Handles the linking of a game account to a user.
- **Fields**:
  - `game_id`: Integer field to specify the game.
  - `gaming_account`: Character field for the gaming account identifier.
- **Validation**: Ensures the gaming account isn't already in use or linked to another user.

### EditGameAccountSerializer
- **Purpose**: Updates an existing game account.
- **Fields**:
  - `gaming_account`: Character field for the new gaming account identifier.
- **Validation**: Checks that the new gaming account isn't used by other users.

### GameAccountSerializer
- **Purpose**: Serializes game account information.
- **Fields**: Includes the game details and the gaming account.

### ProfileSerializer
- **Purpose**: Serializes basic profile information.
- **Fields**: Contains verification status, wallet balance, PayPal/Discord IDs, and more.

### PlayerProfileDetailsSerializer
- **Purpose**: Gathers detailed player profile information.
- **Fields**: Includes profile, address, game accounts, social media providers, and inactivity status.

### UpdatePlayerProfileSerializer
- **Purpose**: Updates player profile details.
- **Fields**: First name, last name, address, contact information, and more.
- **Validation**: Ensures data integrity for phone numbers, age, and name formats.

### RequestNewOTPSerializer
- **Purpose**: Requests a new OTP (One-Time Password) for phone verification.
- **Validation**: Checks CAPTCHA and ensures OTP request limits are respected.

### UpdateProfileImageSerializer
- **Purpose**: Updates a user's profile image.
- **Validation**: Ensures the image format is correct (jpeg, png, jpg).

### UpdateProfileNotificationSerializer
- **Purpose**: Updates a user's notification settings.
- **Fields**: Text message, email, and Discord notifications.

### UpdatePaypalIDSerializer
- **Purpose**: Updates a user's PayPal ID.
- **Validation**: Ensures the PayPal ID isn't already registered to another user.

### ReferFriendListSerializer
- **Purpose**: Provides details on friends referred by the user.
- **Fields**: Includes referral earnings and the status of referrals.

### LinkSocialAccountSerializer
- **Purpose**: Links a social media account to the user's profile.
- **Fields**: `code` for authorization and `provider` specifying the social platform.
- **Methods**: Handles linking for Facebook, Google, Discord, Twitch, and Twitter.

### DisconnectSocialAccountSerializer
- **Purpose**: Disconnects a social media account from the user's profile.
- **Fields**: Specifies the social media provider to disconnect.

---

This module plays a critical role in managing user interactions related to profiles and personal settings within the gaming application, ensuring data integrity and enhancing user experience through validation and structured data handling.