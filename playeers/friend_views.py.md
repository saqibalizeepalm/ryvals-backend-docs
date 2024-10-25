# Friend Views Documentation

This document provides a detailed explanation of the `friend_views.py` file, which is responsible for handling various friend-related operations in a Django application. The operations include listing friends, creating new friend requests, managing notifications, handling favorites, and managing friend requests. This file utilizes Django Rest Framework's generic views and custom serializers to achieve these functionalities.

## 📄 Overview

The primary components in this file are:

- **API Views**: These handle HTTP requests and define the logic for various friend-related operations.
- **Serializers**: Used to convert complex data types, such as querysets and model instances, into native Python datatypes that can then be easily rendered into JSON, XML, or other content types.

## 🔍 API Views

Below is the detailed explanation of each API view present in the `friend_views.py` file:

### 1. `ListCreateFriendsAPIView`
- **Purpose**: 
  - **GET**: Lists all friends of the current user.
  - **POST**: Adds a new friend to the user's friend list.
- **Permissions**: Requires the user to be authenticated and have an active status.
- **Pagination**: Uses `StandardPagination` to paginate the results.
- **Methods**:
  - `get_serializer_class`: Returns the appropriate serializer based on the HTTP method.
  - `get_queryset`: Retrieves the list of friends, distinguishing between favorite and non-favorite friends.

### 2. `ListNotificationAPIView`
- **Purpose**: Lists all notifications for the user.
- **Permissions**: Requires the user to be authenticated and have an active status.
- **Pagination**: Uses `StandardPagination`.
- **Methods**: 
  - `get_queryset`: Retrieves all notifications for the current user, ordered by creation date.
  - `list`: Extends the response to include counts of seen and overall notifications.

### 3. `UpdateNotificationAPIView`
- **Purpose**: Updates the status of a notification (accept or reject).
- **Permissions**: Requires the user to be authenticated and have an active status.
- **Methods**:
  - `get_object`: Retrieves the notification based on the provided ID.
  - `get_serializer_context`: Provides additional context for the serializer.

### 4. `RemoveFriendAPIView`
- **Purpose**: Removes a friend from the user's friend list.
- **Permissions**: Requires the user to be authenticated and have an active status.
- **Methods**:
  - `get_object`: Retrieves the user who is to be removed from the friend list.

### 5. `AddPlayerAsFavouritesAPIView`
- **Purpose**: Adds a player to the user's favorites list.
- **Permissions**: Requires the user to be authenticated and have an active status.

### 6. `UpdatePlayerAsFavouritesAPIView`
- **Purpose**: Updates a player's status in the favorites list.
- **Permissions**: Requires the user to be authenticated and have an active status.
- **Methods**:
  - `get_object`: Retrieves the favorite player object based on the ID provided.

### 7. `PrivateProfileAPIView`
- **Purpose**: Toggles the privacy settings of the user's profile.
- **Permissions**: Requires the user to be authenticated and have an active status.
- **Methods**:
  - `get_object`: Retrieves the user's profile.

### 8. `DeleteFavouritesAPIView`
- **Purpose**: Removes a player from the user's favorites list.
- **Permissions**: Requires the user to be authenticated and have an active status.
- **Methods**:
  - `destroy`: Handles the deletion of a favorite player and logs the event.

### 9. `ReadNotificationAPIView`
- **Purpose**: Marks all notifications as read.
- **Permissions**: Requires the user to be authenticated and have an active status.
- **Methods**:
  - `get_object`: Retrieves the current user.

### 10. `ProfilePermissionAPIView`
- **Purpose**: Retrieves the profile permissions of another user.
- **Permissions**: Requires the user to be authenticated and have an active status.
- **Pagination**: Uses `StandardPagination`.
- **Methods**:
  - `get_queryset`: Retrieves the friend list based on privacy settings.
  - `list`: Customizes the response to include profile details and logs the profile view event.

### 11. `CancelRequestAPIView`
- **Purpose**: Cancels a sent friend request.
- **Permissions**: Requires the user to be authenticated and have an active status.
- **Methods**:
  - `get_object`: Retrieves the friend request that is to be canceled.

### 12. `RemoveNotificationAPIView`
- **Purpose**: Deletes one or all notifications.
- **Permissions**: Requires the user to be authenticated and have an active status.
- **Methods**:
  - `post`: Deletes notifications based on the type specified.

### 13. `FriendRequestNotificationAPIView`
- **Purpose**: Lists incoming and outgoing friend requests.
- **Permissions**: Requires the user to be authenticated and have an active status.
- **Pagination**: Uses `StandardPagination`.

## 📦 Dependencies

- **Django Models**: Utilizes models from `nimda`, `friendship`, `accounts`, and `players` apps.
- **Rest Framework**: Uses generic views and response management from Django Rest Framework.
- **Custom Messages**: Employs custom messages for user feedback.
- **Utilities**: Implements utility methods for logging and IP address retrieval.

## 🔧 Configuration

The file leverages Django's configuration settings to manage user authentication, permissions, and database queries efficiently.

## 🎨 Conclusion

The `friend_views.py` file is a comprehensive implementation for handling friend-related operations within the Django application. It makes extensive use of Django Rest Framework's capabilities, offering a robust and scalable solution for managing user relationships, notifications, and interactions.