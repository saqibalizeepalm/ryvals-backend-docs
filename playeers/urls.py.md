# `urls.py` Documentation

This file is responsible for configuring the URL endpoints for the `players` Django application. It connects specific URL patterns to the corresponding views, enabling different functionalities within the application.

## Table of Contents
- [Overview](#overview)
- [URL Patterns](#url-patterns)
  - [Profile Management](#profile-management)
  - [Lobby Management](#lobby-management)
  - [Game Account Management](#game-account-management)
  - [Dashboard](#dashboard)
  - [Friends Management](#friends-management)
  - [Versus Management](#versus-management)
  - [Challenges Management](#challenges-management)

## Overview
The `urls.py` file maps various URL paths to their respective view classes. These mappings enable the application to handle HTTP requests for different features like profile updates, lobby enrollments, game account management, and more.

## URL Patterns

### Profile Management
These endpoints allow users to manage their profiles, including linking social accounts, updating profile images, and setting notifications.

| URL Path                   | View Class                          | Description                                           |
|----------------------------|-------------------------------------|-------------------------------------------------------|
| `profile/`                 | `RetrieveUpdatePlayerProfileAPIView`| Retrieve or update the user's profile.                |
| `link-account/`            | `LinkSocialAccountAPIView`          | Link a social media account to the user's profile.    |
| `disconnect-account/`      | `DisconnectSocialAccountAPIView`    | Disconnect a linked social media account.             |
| `paypal-update/`           | `UpdatePaypalIDAPIView`             | Update the user's PayPal ID.                          |
| `profile/avatar/`          | `UpdateProfileImageAPIView`         | Update the user's profile image.                      |
| `profile/notification/`    | `UpdateProfileNotificationAPIView`  | Update the user's notification settings.              |
| `profile/check-username/`  | `UsernameAvailabilityAPIView`       | Check if a username is available.                     |

### Lobby Management
Endpoints for enrolling in lobbies, registering teams, and managing team invites.

| URL Path                                        | View Class                    | Description                                              |
|-------------------------------------------------|-------------------------------|----------------------------------------------------------|
| `lobby/enroll/`                                 | `EnrollPlayerInLobbyAPIView`  | Enroll a player in a lobby.                              |
| `lobby/register-team/`                          | `RegisterTeamAPIView`         | Register a team for a lobby.                             |
| `lobby/make-payment/`                           | `OwnerPayOtherTeammatesAPIView`| Team owner makes a payment for teammates.                |
| `lobby/<int:lobby_id>/teammates/`               | `ListAvailableTeammatesAPIView`| List team members available for a lobby.                 |
| `lobby/<int:lobby_id>/existing-teams/`          | `ListTeamAPIView`             | List existing teams in a lobby.                          |
| `lobby/<int:lobby_id>/password-verification/`   | `LobbyPasswordAuthAPIView`    | Verify password for a lobby.                             |

### Game Account Management
Manage the linking, updating, and verification of game accounts.

| URL Path                          | View Class                              | Description                                         |
|-----------------------------------|-----------------------------------------|-----------------------------------------------------|
| `game-account/`                   | `AddGameAccountAPIView`                 | Link a new game account.                            |
| `game-account/<int:game_id>/`     | `UpdateDestroyGameAccountAPIView`       | Update or delete a game account.                    |
| `profile/verify/`                 | `OTPConfirmationAPIView`                | Confirm user verification via OTP.                  |
| `captcha/verify/`                 | `CaptchaConfirmationAPIView`            | Confirm verification via captcha.                   |

### Dashboard
Endpoints for dashboard-related functionalities, including viewing available lobbies and wallet transactions.

| URL Path                          | View Class                              | Description                                         |
|-----------------------------------|-----------------------------------------|-----------------------------------------------------|
| `dashboard/<type>-lobbies/`       | `ListEnrolledLobbiesAPIView`            | List active or previous lobbies.                    |
| `dashboard/available-lobbies/`    | `ListAvailableLobbiesAPIView`           | List available lobbies.                             |
| `wallet-history/`                 | `ListWalletTransactionAPIView`          | View wallet transaction history.                    |

### Friends Management
Endpoints for managing friends, notifications, and friend requests.

| URL Path                         | View Class                             | Description                                         |
|----------------------------------|----------------------------------------|-----------------------------------------------------|
| `friends/`                       | `ListCreateFriendsAPIView`             | List or create friends.                             |
| `notifications/`                 | `ListNotificationAPIView`              | List notifications.                                 |
| `notification-status/<int:id>/`  | `UpdateNotificationAPIView`            | Update notification status.                         |
| `friend-requests/`               | `FriendRequestNotificationAPIView`     | List incoming and outgoing friend requests.         |
| `remove-friend/<int:id>/`        | `RemoveFriendAPIView`                  | Remove a friend.                                    |

### Versus Management
Endpoints for managing versus teams and invites.

| URL Path                         | View Class                             | Description                                         |
|----------------------------------|----------------------------------------|-----------------------------------------------------|
| `versus-team/`                   | `AddVersusTeamAPIView`                 | Add a new versus team.                              |
| `versus-items/`                  | `ListVersusItemForTeamAPIView`         | List versus items for a team.                       |
| `versus-team/<int:pk>/`          | `VersusTeamRetrieveUpdateDeleteAPIView`| Retrieve, update, or delete a versus team.          |
| `versus/<int:team>/action/`      | `VersusSeparateTeamInviteAPIView`      | Take action on a team invite.                       |

### Challenges Management
Endpoints for creating, managing, and responding to challenges.

| URL Path                          | View Class                              | Description                                         |
|-----------------------------------|-----------------------------------------|-----------------------------------------------------|
| `challenges-team/`                | `AddChallengesTeamAPIView`              | Add a challenge team.                               |
| `challenges/`                     | `AddChallengesAPIView`                  | Add a new challenge.                                |
| `challenge-invite/<int:challenge>/`| `ChallengesInviteAPIView`               | Respond to a challenge invite.                      |
| `challenge-accept/<int:id>/`      | `ChallengesAcceptAPIView`               | Accept an open challenge.                           |
| `challenge/<int:challenge_id>/teammates/` | `ListAvailablePlayerForChallengeAPIView` | List available teammates for a challenge.     |

Each of these URL patterns is associated with a specific view class, which handles the HTTP requests and responses for the respective functionality within the application.