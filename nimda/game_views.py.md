# Game Views Documentation

This documentation provides a detailed overview of the `game_views.py` file, which contains various API views for managing games, lobbies, and challenges within the Ryvals platform. This module primarily serves administrative purposes, allowing admin users to perform CRUD operations on game-related entities.

## Table of Contents
1. [Overview](#overview)
2. [Classes and Methods](#classes-and-methods)
   - [ListCreateGameAdminAPIView](#listcreategameadminapiview)
   - [GameUpdateAdminAPIView](#gameupdateadminapiview)
   - [GameRetrieveDestroyAdminAPIView](#gameretrievedestroyadminapiview)
   - [ListCreateLobbyAdminAPIView](#listcreatelobbyadminapiview)
   - [ListCreateGameDemoAdminAPIView](#listcreategamedemoadminapiview)
   - [ListPinnedGameDemoAdminAPIView](#listpinnedgamedemoadminapiview)
   - [RetrieveUpdateDestroyLobbyAdminAPIView](#retrieveupdatedestroylobbyadminapiview)
   - [FetchLobbyStatsAdminAPIView](#fetchlobbystatsadminapiview)
   - [CancelLobbyAdminAPIView](#cancellobbyadminapiview)
   - [RemovePlayerFromLobbyAdminAPIView](#removeplayerfromlobbyadminapiview)
   - [RemoveTeamFromLobbyAdminAPIView](#removeteamfromlobbyadminapiview)
   - [RetrieveUpdateDestroyGameDemoAdminAPIView](#retrieveupdatedestroygamedemoadminapiview)
   - [ListCreateRulesAdminAPIView](#listcreaterulesadminapiview)
   - [UpdateLobbyActivationStatusAdminAPIView](#updatelobbyactivationstatusadminapiview)
   - [ListComplaintAPIView](#listcomplaintapiview)
   - [RetrieveComplaintAPIView](#retrievecomplaintapiview)
   - [UpdatedLobbyStatsFileCountAPIView](#updatedlobbystatsfilecountapiview)
   - [EnrolledPlayerStatsUpdateAPIView](#enrolledplayerstatsupdateapiview)
   - [TransactionsReportAdminAPIView](#transactionsreportadminapiview)
   - [ListChallengesAPIView](#listchallengesapiview)
   - [ChallengeRetrieveUpdateDestroyAdminAPIView](#challengeretrieveupdatedestroyadminapiview)
3. [Permissions](#permissions)

---

## Overview

The `game_views.py` file is part of the Ryvals administration backend, providing API endpoints for managing games, lobbies, and challenges. It facilitates operations such as creating, updating, deleting, and retrieving data related to these entities. The views are designed to ensure that only authorized admin users can perform these operations, utilizing Django Rest Framework for API management.

---

## Classes and Methods

### ListCreateGameAdminAPIView

- **Purpose**: Manage the list and creation of games.
- **Permissions**: Requires admin access.
- **Methods**:
  - `POST`: Create a new game.
  - `GET`: List all games.

### GameUpdateAdminAPIView

- **Purpose**: Update game details such as images and rules.
- **Permissions**: Requires admin access.
- **Methods**:
  - `PUT`: Update specific game attributes.

### GameRetrieveDestroyAdminAPIView

- **Purpose**: Retrieve or delete game details.
- **Permissions**: Requires admin access.
- **Methods**:
  - `GET`: Retrieve game details.
  - `DELETE`: Delete a game.

### ListCreateLobbyAdminAPIView

- **Purpose**: Manage the list and creation of lobbies.
- **Permissions**: Admins can create and view lobbies.
- **Methods**:
  - `POST`: Create a new lobby.
  - `GET`: List all lobbies, with filters and sorting options.

### ListCreateGameDemoAdminAPIView

- **Purpose**: Manage the list and creation of game demos.
- **Permissions**: Admin access required.
- **Methods**:
  - `POST`: Create a new game demo.
  - `GET`: List all game demos.

### ListPinnedGameDemoAdminAPIView

- **Purpose**: List pinned game demos for admin view.
- **Permissions**: Admin access required.
- **Methods**:
  - `GET`: List pinned game demos.

### RetrieveUpdateDestroyLobbyAdminAPIView

- **Purpose**: Retrieve, update or delete lobby details.
- **Permissions**: Admin access required.
- **Methods**:
  - `GET`: Retrieve lobby details.
  - `PUT`: Update a lobby.
  - `DELETE`: Delete a lobby.

### FetchLobbyStatsAdminAPIView

- **Purpose**: Fetch manual lobby stats for admin review.
- **Permissions**: Admin access required.
- **Methods**:
  - `POST`: Fetch stats based on game type.

### CancelLobbyAdminAPIView

- **Purpose**: Cancel a lobby.
- **Permissions**: Admin access required.
- **Methods**:
  - `POST`: Cancel the specified lobby.

### RemovePlayerFromLobbyAdminAPIView

- **Purpose**: Remove a player from a lobby.
- **Permissions**: Admin access required.
- **Methods**:
  - `PUT`: Remove player and handle refunds.

### RemoveTeamFromLobbyAdminAPIView

- **Purpose**: Remove a team from a lobby.
- **Permissions**: Admin access required.
- **Methods**:
  - `PUT`: Remove team and handle refunds.

### RetrieveUpdateDestroyGameDemoAdminAPIView

- **Purpose**: Retrieve, update or delete game demo details.
- **Permissions**: Admin access required.
- **Methods**:
  - `GET`: Retrieve details.
  - `PUT`: Update details.
  - `DELETE`: Delete a demo.

### ListCreateRulesAdminAPIView

- **Purpose**: Manage the list and creation of lobby rules.
- **Permissions**: Super admin access required.
- **Methods**:
  - `POST`: Create a rule.
  - `GET`: List all rules.

### UpdateLobbyActivationStatusAdminAPIView

- **Purpose**: Activate or deactivate lobbies.
- **Permissions**: Admin access required.
- **Methods**:
  - `PUT`: Update activation status of a lobby.

### ListComplaintAPIView

- **Purpose**: List complaints filed by users.
- **Permissions**: Admin access required.
- **Methods**:
  - `GET`: List all complaints.

### RetrieveComplaintAPIView

- **Purpose**: Retrieve details of a specific complaint.
- **Permissions**: Admin access required.
- **Methods**:
  - `GET`: Retrieve complaint details.

### UpdatedLobbyStatsFileCountAPIView

- **Purpose**: Update image count for PUBG stats.
- **Permissions**: Admin access required.
- **Methods**:
  - `PUT`: Update image count.

### EnrolledPlayerStatsUpdateAPIView

- **Purpose**: Update enrolled player stats.
- **Permissions**: Admin access required.
- **Methods**:
  - `PUT`: Update player stats.

### TransactionsReportAdminAPIView

- **Purpose**: Get transactions report.
- **Permissions**: Admin access required.
- **Methods**:
  - `GET`: List transactions with various filters and aggregations.

### ListChallengesAPIView

- **Purpose**: List all challenges.
- **Permissions**: Admin access required.
- **Methods**:
  - `GET`: List challenges with filters and sorting options.

### ChallengeRetrieveUpdateDestroyAdminAPIView

- **Purpose**: Manage challenges (retrieve, update, delete).
- **Permissions**: Admin access required.
- **Methods**:
  - `GET`: Retrieve challenge details.
  - `PUT`: Update a challenge.
  - `DELETE`: Delete a challenge if conditions are met.

---

## Permissions

The views in this module use a combination of custom and standard Django permissions to ensure that only authorized users can access or modify game-related data. These permissions include:

- **PrivateTokenAccessPermission**: Ensures that a valid token is provided for API access.
- **IsAnyRyvalsAdmin**: Allows access to any Ryvals admin user.
- **IsActivated**: Ensures the admin user is activated.
- **CustomDjangoModelPermissions**: Custom permissions for model-level access.
- **IsRyvalsSuperAdmin**: Specific to super admin users for certain actions.

These permissions are applied at the class level for each view to maintain security and data integrity across the platform.