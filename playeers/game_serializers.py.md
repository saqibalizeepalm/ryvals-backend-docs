# Documentation for `game_serializers.py`

## Overview

The `game_serializers.py` file contains various serializer classes used in the context of gaming-related operations within an application. These serializers help handle data conversion and validation processes, particularly for enrolling players in lobbies, managing team registrations, handling complaints, and more. These operations are crucial for ensuring the smooth functionality of a gaming platform where users can participate in various gaming events.

## Table of Contents

1. [EnrollPlayerInLobbySerializer](#enrollplayerinlobbyserializer)
2. [FileComplaintSerializer](#filecomplaintserializer)
3. [RegisterTeamSerializer](#registerteamserializer)
4. [ListAvailableTeammatesSerializer](#listavailableteammatesserializer)
5. [TeamInviteResponseSerializer](#teaminviteresponseserializer)
6. [ReplaceTeammateSerializer](#replaceteammateserializer)
7. [TeammateSerializer](#teammateserializer)
8. [TeammateLeaveTeamSerializer](#teammateleaveteamserializer)
9. [ListTeamSerializer](#listteamserializer)
10. [OwnerPayOtherTeammatesSerializer](#ownerpayotherteammatesserializer)

## Serializers

### 1. EnrollPlayerInLobbySerializer

- **Purpose**: Handles the enrollment of a player into a gaming lobby.
- **Fields**:
  - `lobby_id`: IntegerField, ID of the lobby to enroll in.
  - `promo_choice`: BooleanField, indicates if a promotion is being used.
  - `player_ip`: IPAddressField, the player's IP address.
- **Validation**:
  - Checks if the lobby is still open for enrollment.
  - Verifies player's geofencing, game account linkage, and sufficient funds.
  - Ensures the lobby has not started or ended.
  - Validates player’s enrollment status and other conditions like free lobby limits.

### 2. FileComplaintSerializer

- **Purpose**: Facilitates the filing of complaints by players against other players within a lobby.
- **Fields**:
  - `lobby_id`: IntegerField, ID of the lobby where the complaint is filed.
  - `offender_id`: IntegerField, ID of the player against whom the complaint is being filed.
  - `streaming_link`: CharField, URL of the streaming link for evidence.
  - `message`: CharField, Description of the complaint.
- **Validation**:
  - Validates the streaming link format.
  - Ensures the complaint is filed within a permissible time frame.
  - Verifies if both the reporter and offender are enrolled in the lobby.

### 3. RegisterTeamSerializer

- **Purpose**: Manages the registration of a team in a gaming lobby.
- **Fields**:
  - `lobby_id`: IntegerField, ID of the lobby for team registration.
  - `promo_choice`: BooleanField, indicates if a promotion is being used.
  - `is_paying_full`: BooleanField, indicates if the team leader is paying the full entry fee.
  - `team_id`: IntegerField, ID of the team to be registered.
- **Validation**:
  - Checks for team invite status, member availability, and mod time.
  - Validates lobby start and end conditions.
  - Ensures team has sufficient funds and meets the lobby requirements.

### 4. ListAvailableTeammatesSerializer

- **Purpose**: Lists available teammates for a player within a lobby context.
- **Fields**:
  - `is_available`: SerializerMethodField, checks if a teammate is available.
- **Functionality**:
  - Determines availability based on accepted invites and current enrollment status within a lobby.

### 5. TeamInviteResponseSerializer

- **Purpose**: Handles responses to team invites, either accepting or rejecting them.
- **Fields**:
  - `promo_choice`: BooleanField, optional, indicates promotional usage during acceptance.
- **Validation**:
  - Ensures the invite is valid and processes the player's response.
  - Checks if the lobby conditions allow for accepting the invite.

### 6. ReplaceTeammateSerializer

- **Purpose**: Facilitates replacing a teammate in a team.
- **Fields**:
  - `remove_player`: IntegerField, ID of the player to be removed.
  - `new_player`: IntegerField, ID of the new player to be added.
- **Validation**:
  - Validates player removal eligibility and new player availability.
  - Ensures that changes comply with mod times and lobby conditions.

### 7. TeammateSerializer

- **Purpose**: Serializes teammate information for a team.
- **Fields**:
  - `uid`, `first_name`, `last_name`, `username`, `email`, `status`, `is_available`
- **Functionality**:
  - Provides detailed teammate information, including availability status.

### 8. TeammateLeaveTeamSerializer

- **Purpose**: Manages the logic for a player leaving a team.
- **Functionality**:
  - Validates the player's ability to leave based on mod times and updates the team structure accordingly.

### 9. ListTeamSerializer

- **Purpose**: Lists a player's existing teams along with details.
- **Fields**:
  - `teammates`, `lobby`, `has_paid_total`, `total_paid_yet`
- **Functionality**:
  - Provides a comprehensive list of teams and related financial details.

### 10. OwnerPayOtherTeammatesSerializer

- **Purpose**: Allows team owners to pay for other teammates.
- **Fields**:
  - `lobby_id`, `promo_choice`, `team_id`, `user_id`
- **Validation**:
  - Ensures the owner has not exhausted mod times and has sufficient funds.

## Conclusion

The `game_serializers.py` file is an integral part of the application, managing user interactions related to gaming lobbies and team management. It ensures data integrity and smooth operation through comprehensive validation and data handling procedures. These serializers not only streamline processes but also enhance user experience by managing complex gaming-related interactions with precision.