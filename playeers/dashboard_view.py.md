# 📜 Dashboard Views Documentation 📜

This documentation provides an in-depth look into the `dashboard_views.py` file, which is part of a Django application for managing and displaying various dashboards related to player lobbies, wallet transactions, community videos, and player statistics.

## 📑 Table of Contents
1. [Overview](#overview)
2. [Classes and Methods](#classes-and-methods)
   - [ListEnrolledLobbiesAPIView](#listenrolledlobbiesapiview)
   - [ListAvailableLobbiesAPIView](#listavailablelobbiesapiview)
   - [ListWalletTransactionAPIView](#listwallettransactionapiview)
   - [ListCommunityAPIView](#listcommunityapiview)
   - [TopPlayersListAPIView](#topplayerslistapiview)

## Overview
The `dashboard_views.py` file defines several API views using Django Rest Framework's generic views and custom views. These views are responsible for handling requests related to:
- Listing the lobbies a player is enrolled in.
- Displaying available lobbies for players.
- Showing wallet transactions.
- Listing community videos.
- Displaying the top players based on a specific metric, such as the number of kills.

## Classes and Methods

### 🚀 ListEnrolledLobbiesAPIView
**Purpose**: Lists the lobbies that a player is currently enrolled in.

- **Permission Classes**: 
  - `PrivateTokenAccessPermission`
  - `IsPlayer`
  - `IsActivated`
  
- **Serializer**: `ListDashboardLobbiesSerializer`

- **Method**: `get_queryset`
  - Filters lobbies based on whether they are active or have ended.
  - Uses the current date and time to determine the status of each lobby.
  - Retrieves lobbies excluding those related to tournaments.

### 🗂️ ListAvailableLobbiesAPIView
**Purpose**: Lists the lobbies available for a player to enroll in.

- **Permission Classes**: 
  - `PrivateTokenAccessPermission`
  - `IsPlayer`
  - `IsActivated`
  
- **Serializer**: `ListDashboardLobbiesSerializer`

- **Method**: `get_queryset`
  - Filters active lobbies excluding those the player is already enrolled in.
  - Allows filtering by game slug via query parameters.
  - Excludes lobbies requiring verification if the player's profile is not verified.

### 💰 ListWalletTransactionAPIView
**Purpose**: Lists all wallet transactions for a player.

- **Permission Classes**: 
  - `PrivateTokenAccessPermission`
  - `IsPlayer`
  - `IsActivated`
  
- **Serializer**: `ListWalletTransactionSerializer`

- **Pagination**: Uses `StandardPagination` for paginating results.

- **Method**: `get_queryset`
  - Retrieves transaction details where the user is either the payee or the receiver.
  - Orders transactions by the latest first.

### 🎥 ListCommunityAPIView
**Purpose**: Provides a list of community videos.

- **Serializer**: `ListCommunitySerializer`

- **Queryset**: Retrieves the latest 6 community videos, prioritizing pinned videos.

### 🌟 TopPlayersListAPIView
**Purpose**: Lists the top 5 players based on the number of kills in the last 7 days.

- **Method**: `get`
  - Calculates the total kills and winnings for each player over the past week.
  - Aggregates data for players and sorts them by winnings.
  - Returns a JSON response with the top 5 players' data.

## Conclusion
The `dashboard_views.py` file is a crucial part of the application, providing endpoints for accessing and displaying various player-related data and statistics. The views leverage Django's ORM capabilities to efficiently query and process data, ensuring a seamless experience for users interacting with the dashboard.