# Documentation for `profile_views.py` 🚀

This documentation provides a comprehensive breakdown of the `profile_views.py` file, which contains various API views related to user profile management in a Django application. These views enable features such as adding game accounts, updating user profiles, handling social media links, and managing user notifications. 

## Table of Contents
1. [Overview](#overview)
2. [Classes and Their Descriptions](#classes-and-their-descriptions)
3. [Permissions Utilized](#permissions-utilized)
4. [Error Handling](#error-handling)
5. [Logging](#logging)
6. [Conclusion](#conclusion)

---

## Overview

The `profile_views.py` file is primarily responsible for managing user-related functionalities such as CRUD operations on game accounts, profile updates, OTP verification, and social media account linking. It utilizes Django Rest Framework (DRF) to create API views that handle HTTP requests.

---

## Classes and Their Descriptions

Below is a detailed description of each class and its purpose within the `profile_views.py` file.

### 1. `AddGameAccountAPIView`
- **Purpose:** Allows users to add a new game account.
- **Method:** `POST`
- **Serializer:** `AddGameAccountSerializer`
- **Permissions:** Requires the user to be authenticated, a player, and activated.

### 2. `UpdateDestroyGameAccountAPIView`
- **Purpose:** Facilitates editing or deletion of a user's game account.
- **Methods:** `PUT`, `DELETE`
- **Serializer:** `EditGameAccountSerializer`
- **Permissions:** Requires the user to be authenticated, a player, and activated.
- **Error Handling:** Raises an exception if a `GET` request is made.

### 3. `RetrieveUpdatePlayerProfileAPIView`
- **Purpose:** Retrieve or update user profile details.
- **Methods:** `GET`, `PUT`
- **Serializers:** `PlayerProfileDetailsSerializer`, `UpdatePlayerProfileSerializer`
- **Permissions:** Requires the user to be authenticated, a player, and activated.

### 4. `UsernameAvailabilityAPIView`
- **Purpose:** Check if a username is available.
- **Method:** `GET`
- **Description:** Returns a message indicating if a username is available or already taken.

### 5. `OTPConfirmationAPIView`
- **Purpose:** Confirms OTP for phone number verification.
- **Method:** `POST`
- **Permissions:** Requires the user to be authenticated, a player, and activated.
- **Description:** Handles OTP validation and updates the phone number if the OTP is valid.

### 6. `CaptchaConfirmationAPIView`
- **Purpose:** Validates CAPTCHA for security.
- **Method:** `POST`
- **Permissions:** Requires the user to be authenticated, a player, and activated.
- **Description:** Ensures CAPTCHA is correctly solved before proceeding.

### 7. `RequestNewOTPAPIView`
- **Purpose:** Allows users to request a new OTP.
- **Method:** `PUT`
- **Serializer:** `RequestNewOTPSerializer`
- **Permissions:** Requires the user to be authenticated, a player, and activated.

### 8. `RetrieveWalletBalanceAPIVIew`
- **Purpose:** Retrieves the user's wallet balance and payment gateway information.
- **Method:** `GET`
- **Permissions:** Requires the user to be authenticated, a player, and activated.

### 9. `RetrieveKYCStatusAPIView`
- **Purpose:** Checks if the user's KYC (Know Your Customer) verification is completed and valid.
- **Method:** `GET`
- **Permissions:** Requires the user to be authenticated, a player, and activated.

### 10. `UpdateProfileImageAPIView`
- **Purpose:** Allows updating of the user's profile image.
- **Method:** `PUT`
- **Serializer:** `UpdateProfileImageSerializer`
- **Permissions:** Requires the user to be authenticated, a player, and activated.

### 11. `UpdatePaypalIDAPIView`
- **Purpose:** Updates the user's PayPal ID.
- **Method:** `PUT`
- **Serializer:** `UpdatePaypalIDSerializer`
- **Permissions:** Requires the user to be authenticated, a player, and activated.

### 12. `ReferFriendListAPIView`
- **Purpose:** Lists all referrals made by the user.
- **Method:** `GET`
- **Serializer:** `ReferFriendListSerializer`
- **Permissions:** Requires the user to be authenticated, a player, and activated.

### 13. `LinkSocialAccountAPIView`
- **Purpose:** Links social media accounts to the user's profile.
- **Method:** `PUT`
- **Serializer:** `LinkSocialAccountSerializer`
- **Permissions:** Requires the user to be authenticated.

### 14. `DisconnectSocialAccountAPIView`
- **Purpose:** Disconnects social media accounts from the user's profile.
- **Method:** `PUT`
- **Serializer:** `DisconnectSocialAccountSerializer`
- **Permissions:** Requires the user to be authenticated.

### 15. `UpdateProfileNotificationAPIView`
- **Purpose:** Updates the user's notification settings.
- **Method:** `PUT`
- **Serializer:** `UpdateProfileNotificationSerializer`
- **Permissions:** Requires the user to be authenticated, a player, and activated.

---

## Permissions Utilized

The file makes extensive use of custom permission classes to ensure that only authenticated and authorized users can access certain functionalities. Key permissions include:
- `PrivateTokenAccessPermission`: Ensures that the user is authenticated via a private token.
- `IsPlayer`: Confirms that the user has a player role.
- `IsActivated`: Checks that the user's account is activated.

---

## Error Handling

Error handling is efficiently managed using DRF's exception handling mechanisms. Common exceptions include:
- `APIException`: Used to handle specific error messages such as profile not found or game account not found.
- Custom error messages are also defined to provide meaningful feedback to the user.

---

## Logging

The module uses Python's built-in logging library to log errors and important actions within the application. This aids in debugging and tracking user activities.

---

## Conclusion

The `profile_views.py` file is an integral part of the application, managing user-related functionalities with precision and security. Its combination of serializers, permissions, and error handling ensures a robust and user-friendly API service. 

By adhering to Django and RESTful principles, this module provides a scalable and maintainable approach to user profile management in a gaming application context.