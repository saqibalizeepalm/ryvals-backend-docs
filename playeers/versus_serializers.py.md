# Documentation for `versus_serializers.py`

**File**: `versus_serializers.py`

## Overview

The `versus_serializers.py` file defines a set of serializers for managing Versus Teams and Challenges within a gaming application. These serializers are used to handle the serialization and deserialization of data and to validate and process incoming data requests related to Versus Team operations and Challenge management.

## Table of Contents

1. [Import Statements](#import-statements)
2. [Constants](#constants)
3. [Serializers](#serializers)
   - [ListVersusTeamSerializer](#listversusteamserializer)
   - [AddVersusTeamSerializer](#addversusteamserializer)
   - [VersusTeamDetailSerializer](#versusteamdetailserializer)
   - [UpdateVersusTeamSerializer](#updateversusteamserializer)
   - [VersusTeamCreateInviteSerializer](#versusteamcreateinviteserializer)
   - [VersusTeamTakeActionInviteSerializer](#versusteamtakeactioninviteserializer)
   - [VersusSeparateTeamInviteSerializer](#versusseparateteaminviteserializer)
   - [VersusRemovePlayerSerializer](#versusremoveplayerserializer)
   - [AddChallengesTeamSerializer](#addchallengesteamserializer)
   - [ListChallengesSerializer](#listchallengesserializer)
   - [ListOpenChallengesSerializer](#listopenchallengesserializer)
   - [MatchInviteChallengeSerializer](#matchinvitechallengeserializer)
   - [ChallengeDetailRetrieveSerializer](#challengedetailretrieveserializer)
   - [AddChallengesSerializer](#addchallengesserializer)
   - [ChallengesInviteSerializer](#challengesinviteserializer)
   - [ChallengesAcceptSerializer](#challengesacceptserializer)
   - [ListAvailablePlayerForChallengeSerializer](#listavailableplayerforchallengeserializer)
   - [ChallengeReplaceTeammateSerializer](#challengereplaceteammateserializer)
   - [ChallengeTeammateLeaveTeamSerializer](#challengeteammateleaveteamserializer)
   - [ChlngOwnerPayOtherTeammatesAPIViewSerializer](#chlngownerpayotherteammatesapiviewserializer)

---

## Import Statements

The file begins with a series of import statements that bring in necessary Django modules, third-party packages, and local application modules. Key imports include:

- `django.db.models`, `django.utils`, `rest_framework`, and others for database and HTTP request handling.
- Models related to players, games, and challenges such as `VersusTeam`, `Challenge`, `MatchInvite`, etc.
- Utility methods for handling various tasks like sending emails, logging, and handling permissions.

## Constants

Various constants are defined for ease of use throughout the file, including:

- **Timezones**: `US_EAST_TIMEZONE_CONST`, `utc_tz`, `est_tz`
- **Formatting Constants**: `TIME_STRING_FORMAT_CONST`, `PROMO_CHOICE__CONST`
- **Logger**: `logger` for logging purposes.

## Serializers

The serializers in this file are responsible for converting complex data such as querysets and model instances into native Python datatypes, which can then be easily rendered into JSON or other content types. They also provide deserialization, allowing parsed data to be converted back into complex types after being validated.

### ListVersusTeamSerializer

**Purpose**: Serializes data for listing Versus Teams, providing details like team ID, name, mode, game, and creator.

**Key Fields**:
- `id`, `name`, `mode`, `modetag`, `game`, `members`, `create_date`, `leader`, `game_logo`, `creator`, `status`.

### AddVersusTeamSerializer

**Purpose**: Handles the addition of new Versus Teams. Validates team creation requests ensuring the player has a game account.

**Key Fields**:
- `name`, `mode`, `game_id`.

### VersusTeamDetailSerializer

**Purpose**: Serializes detailed information about a Versus Team, including player details.

**Key Fields**:
- `id`, `game`, `mode`, `modetag`, `create_date`, `name`, `players`, `has_player`.

### UpdateVersusTeamSerializer

**Purpose**: Allows updates to be made to existing Versus Teams, ensuring name uniqueness.

**Key Fields**:
- `name`, `mode`.

### VersusTeamCreateInviteSerializer

**Purpose**: Manages the creation of invites for players to join a Versus Team.

**Key Fields**:
- `username`.

### VersusTeamTakeActionInviteSerializer

**Purpose**: Handles taking action on team invites (accept/reject).

**Key Fields**:
- `action`.

### VersusSeparateTeamInviteSerializer

**Purpose**: A separate serializer for handling team invites, similar to `VersusTeamTakeActionInviteSerializer`.

**Key Fields**:
- `action`.

### VersusRemovePlayerSerializer

**Purpose**: Manages the removal of a player from a Versus Team.

### AddChallengesTeamSerializer

**Purpose**: Serializes data for adding challenges related to teams, including team details.

**Key Fields**:
- `leader_name`, `players`, `modetag`.

### ListChallengesSerializer

**Purpose**: Lists open and private challenges, providing detailed information about each challenge.

**Key Fields**:
- `modetag`, `versus`, `current_status`, `countdown_time`, `match_date`, `match_time`, `creator`, `action_type`, `enrolled`, `rejected`, `winning`, `payment_required`.

### ListOpenChallengesSerializer

**Purpose**: Serializer for listing open challenges, similar to `ListChallengesSerializer`.

**Key Fields**:
- `modetag`, `current_status`, `countdown_time`.

### MatchInviteChallengeSerializer

**Purpose**: Serializes information about specific player stats in a challenge.

**Key Fields**:
- `invite_status`, `username`, `leader`, `teams`, `payment_status`, `player_winning`.

### ChallengeDetailRetrieveSerializer

**Purpose**: Retrieves details of a specific challenge with match stats.

**Key Fields**:
- `official_stats`, `team_1_payment_mode`, `team_2_payment_mode`.

### AddChallengesSerializer

**Purpose**: Handles the creation of new challenges, validating data and ensuring funds sufficiency.

**Key Fields**:
- `game_id`, `mode`, `match_date`, `match_time`, `entry_fee`, `team_1`, `team_2`.

### ChallengesInviteSerializer

**Purpose**: Handles actions on team challenge invites when team 1 knows team 2.

**Key Fields**:
- `action`, `is_paying_full`, `bonus`, `leader`.

### ChallengesAcceptSerializer

**Purpose**: Manages the acceptance of any open challenge, ensuring game account and funds availability.

**Key Fields**:
- `team_id`, `is_paying_full`, `bonus`.

### ListAvailablePlayerForChallengeSerializer

**Purpose**: Checks the availability of players for a challenge invitation.

**Key Fields**:
- `is_available`.

### ChallengeReplaceTeammateSerializer

**Purpose**: Handles the replacement of a teammate within a challenge team.

**Key Fields**:
- `remove_player`, `new_player`.

### ChallengeTeammateLeaveTeamSerializer

**Purpose**: Allows a player to leave a joined team in a challenge.

### ChlngOwnerPayOtherTeammatesAPIViewSerializer

**Purpose**: Manages payments made by team owners for their teammates in challenges.

**Key Fields**:
- `challenge_id`, `promo_choice`, `team_id`, `user_id`.

---

This documentation provides a comprehensive overview of the `versus_serializers.py` file, detailing each serializer's purpose and key fields. The serializers collectively ensure robust management of Versus Teams and Challenges within the application, handling scenarios from team creation to challenge participation.