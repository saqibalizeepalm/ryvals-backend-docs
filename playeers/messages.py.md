# Documentation for `messages.py` 📜

**Overview**: 

The `messages.py` is a module in a Django project that provides a centralized location for storing user-facing messages. These messages are typically used for notifications, validations, error messages, or other informational responses within the application. They utilize Django's translation system to support internationalization, allowing the application to display messages in different languages.

---

## Table of Contents 📚

1. [Introduction](#introduction)
2. [Purpose](#purpose)
3. [Message Variables](#message-variables)
4. [Internationalization](#internationalization)
5. [Conclusion](#conclusion)

---

## Introduction 🚀

In a Django application, presenting standardized messages to users is crucial for maintaining consistency and clarity. The `messages.py` file serves as a repository for these messages, making it easier to manage and update them across the application. This file leverages Django's `gettext_lazy` for lazy evaluation of translation, ensuring that messages are translated at runtime according to the user's language preferences.

---

## Purpose 🎯

The main purpose of `messages.py` is:

- **Centralized Message Management**: Store all user-facing messages in one place to simplify maintenance and updates.
- **Internationalization Support**: Utilize Django's translation features to support multiple languages.
- **Consistency**: Ensure consistent messaging throughout the application.

---

## Message Variables 📜

Below is a list of key message variables defined in the file along with their purposes:

| **Variable Name** | **Description** |
|-------------------|-----------------|
| `TEAM_NOT_FOUND_MSSG` | Message displayed when a team cannot be found. |
| `USERNAME_UNAVAILABLE` | Indicates that a username is unavailable. |
| `USERNAME_AVAILABLE` | Indicates that a username is available. |
| `COMPLAINT_FILING_ERROR` | Error message for failed complaint filing. |
| `FULL_LOBBY` | Notification when a lobby is full. |
| `ADD_FUNDS` | Message indicating insufficient wallet funds. |
| `OTP_MSG` | Template for OTP message sent to users. |
| `NUMBER_ALREADY_EXISTS` | Error when a phone number is already registered. |
| `INVALID_OTP` | Indicates an invalid OTP. |
| `GAME_ACCOUNT_NOT_FOUND` | Error message when a game account cannot be found. |
| `FRIEND_REQUEST_SEND` | Confirms a friend request has been sent. |
| `ADD_FAVOURITE` | Confirms a player has been added as a friend. |
| `PROFILE_DEACTIAVED_ADMIN` | Notification when an account is deactivated by an admin. |

These messages also support dynamic content insertion using Python's string formatting, allowing the message to include specific details like usernames, team names, or game titles. 

---

## Internationalization 🌍

The messages in this file use Django's `gettext_lazy` to support internationalization. This function marks strings for translation but delays the actual translation until the string is accessed, which is useful for loading messages in the appropriate language context.

For example:
```python
from django.utils.translation import gettext_lazy as _

TEAM_NOT_FOUND_MSSG = _('Team not found.')
```

This allows the application to dynamically present messages in the user's preferred language, enhancing the user experience for a global audience.

---

## Conclusion 🏁

The `messages.py` file is an essential component for managing user-facing messages in a Django application. By centralizing these messages and supporting internationalization, developers can ensure that their application is both maintainable and accessible to a broader audience. This approach not only simplifies updates but also promotes a consistent and professional user interface.