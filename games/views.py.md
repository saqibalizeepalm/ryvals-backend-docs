# Documentation for `views.py` 📄

This document provides a detailed explanation of the `views.py` file, which is a crucial part of the games application. The file primarily consists of class-based views using Django's REST framework to handle various API endpoints related to games, lobbies, and game demos.

## Table of Contents 📑
1. [Overview](#overview)
2. [Class-based Views](#class-based-views)
   - [GameListAPIView](#gamelistapiview)
   - [GameDetailAPIView](#gamedetailapiview)
   - [LobbyListAPIView](#lobbylistapiview)
   - [GameDemoListAPIView](#gamedemolistapiview)
   - [GameDemosListAPIView](#gamedemoslistapiview)
   - [LobbyDetailAPIView](#lobbydetailapiview)
   - [ListEnrolledPlayersAPIView](#listenrolledplayersapiview)
   - [ListRegisteredTeammatesAPIView](#listregisteredteammatesapiview)
3. [Permissions](#permissions)
4. [Pagination](#pagination)
5. [Filters and Querysets](#filters-and-querysets)

## Overview

The `views.py` file uses Django's REST framework to define various API endpoints. These endpoints allow users to list games, view game details, list lobbies, and get details about specific lobbies. It also supports listing enrolled players and registered teammates for a team within a lobby.

## Class-based Views

### GameListAPIView

- **Purpose**: Lists all active games that are not deleted.
- **Serializer**: `GameListSerializer`
- **Queryset**: Filters games by active status and non-deletion, ordered by `sort_order`.
  
**Usage**: This view is useful for displaying a list of all available games to users.

### GameDetailAPIView

- **Purpose**: Retrieves details of a specific game based on its slug.
- **Serializer**: `GameDetailSerializer`
- **Error Handling**: Raises an exception if the game is not found or is deactivated.

**Usage**: Used to display detailed information about a single game.

### LobbyListAPIView

- **Purpose**: Lists lobbies based on various filters such as game type, mode, and enrollment status.
- **Permissions**: Uses `PublicTokenAccessPermission` or `PrivateTokenAccessPermission`.
- **Filters**: Can filter by current, previous, or enrolled lobbies.

**Usage**: This view is essential for users to find lobbies they can join or have joined.

### GameDemoListAPIView

- **Purpose**: Lists demos for a particular game.
- **Permissions**: Same as `LobbyListAPIView`.
- **Pagination**: Uses `InfiniteScrollPagination` for seamless scrolling.

**Usage**: Useful for users to view game demos related to a specific game.

### GameDemosListAPIView

- **Purpose**: Lists all game demos across games.
- **Permissions**: Same as `LobbyListAPIView`.
- **Pagination**: Uses `InfiniteScrollPagination`.

**Usage**: Allows users to explore demos from all games available.

### LobbyDetailAPIView

- **Purpose**: Provides detailed information about a specific lobby.
- **Permissions**: Same as `LobbyListAPIView`.
- **Error Handling**: Handles scenarios where lobbies or games are deactivated.

**Usage**: Vital for users to see in-depth details about a lobby.

### ListEnrolledPlayersAPIView

- **Purpose**: Lists players enrolled in a lobby, excluding the request user.
- **Permissions**: Requires the user to be an activated player or admin.
  
**Usage**: This API is beneficial for players to see who else is enrolled in the same lobby.

### ListRegisteredTeammatesAPIView

- **Purpose**: Lists teammates registered for a team in a specific lobby.
- **Permissions**: Same as `ListEnrolledPlayersAPIView`.

**Usage**: Useful for team management and coordination within a lobby.

## Permissions

The views employ a variety of custom permissions to ensure that only authorized users can access certain data. This includes:

- `PublicTokenAccessPermission`
- `PrivateTokenAccessPermission`
- `IsPlayer`
- `IsAnyRyvalsAdmin`
- `IsActivated`

## Pagination

The views use pagination classes for managing large data sets:

- **StandardPagination**: Used for typical list views to limit the number of items per page.
- **InfiniteScrollPagination**: Used for views that benefit from infinite scrolling, enhancing user experience by loading more data as needed.

## Filters and Querysets

The views make extensive use of Django's ORM to filter and sort data. This includes:

- **Filter Lobbies**: Custom logic to filter lobbies based on type (current, previous, enrolled).
- **Filter Game Demos**: Filters demos by game slug and status.
- **Complex Querysets**: Combines Q objects for complex querying scenarios.

**Note**: Proper exception handling is employed throughout to catch and respond to errors, such as missing games or lobbies.

---

This detailed documentation aims to provide a comprehensive understanding of the `views.py` file and its functionality within the application. Each view is tailored to meet specific needs, ensuring a robust and flexible API for the games application. 🚀