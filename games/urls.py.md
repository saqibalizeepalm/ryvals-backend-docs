# Documentation for `urls.py` 📚

This document serves as detailed documentation for the `urls.py` file in a Django application, specifically for the `games` API version 1. This file is crucial as it maps URL patterns to views, allowing HTTP requests to be routed to the appropriate view logic.

## Index

1. [Overview](#overview)
2. [Django URL Dispatcher](#django-url-dispatcher)
3. [URL Patterns](#url-patterns)
4. [View Associations](#view-associations)
5. [Summary](#summary)

## Overview

The `urls.py` file defines URL patterns for the `api_games_v1` app. These patterns direct HTTP requests to the corresponding view logic, enabling users to interact with the gaming API.

## Django URL Dispatcher

In Django, the URL dispatcher is used to match the incoming requests to the defined URL patterns. Each pattern is associated with a view, which processes the request and returns a response.

### Import Statements

```python
from django.urls import path
from games.api.views import (
    GameDetailAPIView,
    GameListAPIView,
    ListEnrolledPlayersAPIView,
    ListRegisteredTeammatesAPIView,
    LobbyDetailAPIView,
    LobbyListAPIView,
    GameDemoListAPIView,
    GameDemosListAPIView
)
```

- **`path`**: A function used to define URL patterns.
- **View Imports**: Various view classes from `games.api.views` that handle the logic for each endpoint.

## URL Patterns

### URL Patterns Table

| **Path** | **View** | **Name** | **Description** |
|----------|----------|----------|-----------------|
| `''` | `GameListAPIView.as_view()` | `game_list` | Lists all available games. |
| `'game-demos/'` | `GameDemosListAPIView.as_view()` | `game_demos_list` | Lists all game demos. |
| `'<slug:slug>/'` | `GameDetailAPIView.as_view()` | `game_detail` | Retrieves details for a specific game identified by a slug. |
| `'<slug:slug>/lobby/'` | `LobbyListAPIView.as_view()` | `lobby_list` | Lists all lobbies for a specific game. |
| `'<slug:slug>/game-demo/'` | `GameDemoListAPIView.as_view()` | `game_demo_list` | Lists game demos for a specific game. |
| `'<slug:slug>/lobby/<int:pk>/'` | `LobbyDetailAPIView.as_view()` | `lobby_detail` | Retrieves details for a specific lobby. |
| `'<slug:slug>/lobby/<int:lobby_id>/enrolled-players/'` | `ListEnrolledPlayersAPIView.as_view()` | `list_enrolled_player` | Lists players enrolled in a specific lobby. |
| `'<slug:slug>/lobby/<int:lobby_id>/teammates/'` | `ListRegisteredTeammatesAPIView.as_view()` | `list_team_members` | Lists team members in a specific lobby. |

### URL Patterns Explained

- **Game List**: The root path (`''`) lists all available games.
- **Game Demos**: The `game-demos/` path lists all available game demos across games.
- **Specific Game Details**: Using a slug (`<slug:slug>`), retrieves details for that game.
- **Lobby List**: Lists all lobbies associated with a specific game using the game's slug.
- **Game Demo List**: Retrieves demos associated with a specific game.
- **Lobby Details**: Retrieves detailed information about a specific lobby using its primary key.
- **Enrolled Players**: Lists all players enrolled in a particular lobby.
- **Team Members**: Lists all team members registered for a specific lobby.

## View Associations

Each URL pattern is associated with a view that handles the request logic:

- **`GameListAPIView`**: Handles requests for the list of games.
- **`GameDetailAPIView`**: Handles requests for game details.
- **`LobbyListAPIView`**: Handles requests for lobby listings.
- **`LobbyDetailAPIView`**: Handles requests for lobby details.
- **`ListEnrolledPlayersAPIView`**: Handles requests for listing enrolled players.
- **`ListRegisteredTeammatesAPIView`**: Handles requests for listing registered teammates.
- **`GameDemoListAPIView`**: Handles requests for game demos of a specific game.
- **`GameDemosListAPIView`**: Handles requests for all game demos.

## Summary

The `urls.py` file for the `api_games_v1` application efficiently maps various URL endpoints to their corresponding view logic. This setup is crucial for managing game-related data, lobbies, and player interactions within the application. By organizing these URL patterns, the application ensures a seamless user experience and robust API functionality.