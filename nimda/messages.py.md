# 📜 `messages.py` Documentation

This file serves as a centralized location for storing all the user-facing messages that the application might return, especially in scenarios involving success, error, or validation feedback. It leverages Django's translation utilities to support internationalization, ensuring that messages can be translated into different languages as needed.

## 🌐 Import Section
```python
from django.utils.translation import gettext_lazy as _
```
- **gettext_lazy (_)**: This is a Django utility function that marks strings for translation but doesn't immediately translate them. This is particularly useful in Django models and forms where the translation will occur later.

## 💬 Message Constants

This file contains a comprehensive list of message constants used throughout the application. These messages cover a wide range of scenarios from user management to game operations, and they are crucial for providing feedback to users. Below is an organized breakdown of these constants:

### User Management Messages
- **`USER_DELETED`**: Indicates successful deletion of a user.
- **`USER_DELETED_ERROR`**: Indicates failure in the deletion of a user.
- **`USER_NOT_FOUND`**: Denotes that a user could not be found.
- **`USER_ALREADY_DEACTIVATED`**: Feedback when an already deactivated user's account is attempted to be deactivated again.
- **`USER_ALREADY_ACTIVATED`**: Feedback when an already activated user's account is attempted to be activated again.
- **`ACCOUNT_NOT_DEACTIVATED`**: Error when failing to deactivate an account.

### Game Management Messages
- **`DUPLICATE_GAME_ERROR`**: Error when a game with the same title already exists.
- **`GAME_DELETED`**: Indicates successful deletion of a game.
- **`GAME_DELETED_ERROR`**: Error while attempting to delete a game.
- **`GAME_DEMO_CREATION_ERROR`**: Error in creating a game demo.
- **`GAME_DEMO_DELETED`**: Indicates successful deletion of a game demo.
- **`GAME_DEMO_DELETED_ERROR`**: Error while attempting to delete a game demo.
- **`GAME_DEMO_NOT_FOUND`**: Denotes that a game demo was not found.

### Lobby Management Messages
- **`PLAYER_LOBBY_NOT_FOUND`**: Error when a player lobby combination is not found.
- **`TEAM_LOBBY_NOT_FOUND`**: Error when a team lobby combination is not found.
- **`LOBBY_CREATION_ERROR`**: Error in creating a lobby.
- **`LOBBY_DELETED`**: Indicates successful deletion of a lobby.
- **`LOBBY_DELETED_ERROR`**: Error while attempting to delete a lobby.
- **`LOBBY_UPDATE_ERROR`**: Error in updating a lobby.
- **`ACTIVE_LOBBY_ERROR`**: Feedback when trying to update an active lobby.
- **`ENDED_LOBBY_ERROR`**: Feedback when trying to update a lobby that has ended.

### Transaction Messages
- **`TRANSCATION_NOT_FOUND`**: Error when a transaction cannot be found.
- **`AMOUNT_REFUND`**: Indicates a successful refund of an amount.

### General Error Messages
- **`INVALID_HTML`**: Error when there are issues with HTML tags.
- **`STATIC_PAGE_CREATION_ERROR`**: Error creating a static page.
- **`STATIC_PAGE_EDIT_ERROR`**: Error editing a static page.
- **`INVALID_SORT_ORDER`**: Error in sort order input.
- **`ORDERING_ERROR`**: Error occurred while sorting items.

### FAQ and Topic Messages
- **`FAQ_CREATE_ERROR`**: Error adding a question to FAQs.
- **`QUESTION_NOT_FOUND`**: Error when a question cannot be found.
- **`QUESTION_DELETED`**: Indicates successful deletion of a question.
- **`QUESTION_DELETE_ERROR`**: Error while attempting to delete a question.
- **`TOPIC_NOT_FOUND`**: Error when a topic cannot be found.
- **`TOPIC_CREATION_ERROR`**: Error in creating a FAQ topic.
- **`TOPIC_ALREADY_EXISTS`**: Error when a topic already exists.
- **`TOPIC_DELETED`**: Indicates successful deletion of a topic.
- **`TOPIC_DELETE_ERROR`**: Error while attempting to delete a topic.

### 🌟 Additional Notable Messages
- **`WELCOME_TO_RYVALS`**: A welcoming message for new users.
- **`UPDATE_RYVALS_PERMISSIONS`**: Notification of changed permissions by a super admin.
- **`INVALID_STATUS`**: Error when an invalid status is provided.
- **`UNABLE_TO_SEIZE`**: Error when failing to seize the amount.
- **`MONEY_SEIZED_SUCCESSFULLY`**: Indicates successful seizing of money from a user's wallet.

## 🎯 Purpose and Use

This module provides a structured way to handle messaging across the application, ensuring consistency and ease of translation. By centralizing messages, developers can manage text more effectively, and translators can access all translatable strings in one place.

## 🚀 Tips for Developers
- **Use Descriptive Variable Names**: The constants are well-named, summarizing the message's purpose.
- **Leverage Django's Translation Tools**: Ensure messages are wrapped with `_` for translation.
- **Centralized Management**: Modify or add messages in one place, automatically updating them wherever used in the application.

## 🔄 Conclusion

The `messages.py` file is a critical component for maintaining a user-friendly application with meaningful feedback. Its role in supporting internationalization cannot be understated, making it vital for applications aimed at global audiences. By organizing messages logically, this file aids in efficient development and maintenance.