# Documentation for `game_serializers.py` 📚

This file, `game_serializers.py`, contains Django REST Framework serializers designed to manage various aspects related to game functionalities in the Ryvals application. The serializers handle different operations such as game creation, updating game details, adding and managing lobbies, and processing game demos. Additionally, it includes functionalities for handling player transactions, reporting, and game statistics.

## Index 📑

- [Imports](#imports)
- [Helper Functions](#helper-functions)
- [Serializers](#serializers)
  - [AddGameSerializer](#addgameserializer)
  - [GameUpdateAdminSerializer](#gameupdateadminserializer)
  - [AddRuleSerializer](#addruleserializer)
  - [AddLobbySerializer](#addlobbyserializer)
  - [AddGameDemoSerializer](#addgamedemoserializer)
  - [UpdateLobbySerializer](#updatelobbyserializer)
  - [UpdateGameDemoSerializer](#updategamedemoserializer)
  - [PlayerSerializer](#playerserializer)
  - [TeamPlayerSerializer](#teamplayerserializer)
  - [LobbyListDetailAdminSerializer](#lobbylistdetailadminserializer)
  - [GameDemoListDetailAdminSerializer](#gamedemolistdetailadminserializer)
  - [UpdateLobbyActivationStatusSerializer](#updatelobbyactivationstatusserializer)
  - [RemovePlayerFromLobbySerializer](#removeplayerfromlobbyserializer)
  - [RemoveTeamFromLobbySerializer](#removeteamfromlobbyserializer)
  - [ComplaintListSerializer](#complaintlistserializer)
  - [ComplaintDetailSerializer](#complaintdetailserializer)
  - [UpdatedLobbyStatsFileCountSerializer](#updatedlobbystatsfilecountserializer)
  - [EnrolledPlayerStatsUpdateSerializer](#enrolledplayerstatsupdateserializer)
  - [TransactionsReportUnclaimedMoneySerializer](#transactionsreportunclaimedmoneyserializer)
  - [TransactionsReportDormantMoneySerializer](#transactionsreportdormantmoneyserializer)
  - [TransactionsReportSerializer](#transactionsreportserializer)
  - [UpdateAdminChallengeSerializer](#updateadminchallengeserializer)

## Imports

These are the Python libraries and Django modules used in this file:

```python
import pytz
import json
import stripe
import logging
from decimal import Decimal
from emails.utils import Email
from twilio.rest import Client
from django.conf import settings
from django.utils import timezone
from accounts.models import Player, RyvalsAdmin, ReferralReport
from nimda.models import Config, Logs
from rest_framework import serializers
from datetime import datetime, timedelta
from django.db.models.query_utils import Q
from payments.messages import PAYMENT_SUCCESS
from django.contrib.auth import get_user_model
from django.db import IntegrityError, transaction
from django.db.models import Sum
from rest_framework.exceptions import APIException
from games.models import Game, Lobby, RuleTemplate, GameDemo
from games.api.serializers import LobbyListSerializer, GameDemoListSerializer
from django.utils.translation import gettext_lazy as _
from players.messages import SUBJECT_RESULTS_AVAILABLE
from app.messages import (AMOUNT_REFUND_MSG, AMOUNT_REFUND_MSG_REMOVED_BY_ADMIN, MATCH_RESULTS_MSG,
                          MATCH_STATS_COMING, MATCH_STATS_COMING_1, TOURNAMENT_MATCH_STATS_COMING)
from app.utils import UtilityMethods
from ryvals.core.messages import FIELD_REQUIRED, MAX_DECIMAL_PLACES, MAX_DIGITS, MAX_LENGTH_MESSAGE, LOBBY_PASSWORD_MIN_MAX_LENGHT
from players.models import (PlayerLobby, StripeTransfer, Notifications, TransactionDetail, TeamLobby,
                            Challenge, Tournament, PPKTournamentSubMatchTeam, Complaint, GameAccount, TeamPlayer,
                            RemovedLobbyPlayer, TournamentSubMatch)
from tournament.models import TournamentTeamInvite
from games.core.factory import GameFactory, ApexGame, PubgGame, CODMGame
from ryvals.core.discord import (create_channel_webhook, create_private_channel, send_message,
                                 update_channels, remove_player_from_channel)
from nimda.messages import (ACTIVE_LOBBY_ERROR, DUPLICATE_GAME_ERROR, DUPLICATE_LOBBY_ERROR, ENDED_LOBBY_ERROR,
                            LOBBY_UPDATE_ERROR, GAME_DEMO_UPDATE_ERROR, RULE_CREATION_ERROR, UNEXPECTED_LOBBY_ERROR,
                            AMOUNT_REFUND, LOBBY_REFUND_ERROR, LOBBY_CANCEL_BY_ADMIN_REFUND_TEAM, DUPLICATE_GAME_DEMO_ERROR,
                            UNEXPECTED_GAME_DEMO_ERROR, INVALID_MAX_PINNED_DEMO, MAX_PINNED_DEMO_REACHED,
                            REPLACE_DEMO_NOT_EXISTS, REPLACE_DEMO_NOT_PINNED, DEMO_ALREADY_PINNED,
                            REMOVED_FROM_LOBBY_REFUND, LOBBY_LAST_ENTRY_TIME_OVER, PLAYER_REMOVAL_FROM_LOBBY_ERROR,
                            TEAM_REMOVAL_FROM_LOBBY_ERROR, CHALLENGE_LAST_UPDATE_TIME_OVER, UNEXPECTED_REPLACE_WITH_GAME_DEMO_ERROR,
                            TOURNAMENT_LOBBY_ERROR)
from games.messages import (LOBBY_LAST_ENTRY_TIME_ERROR, MATCH_LAST_ENTRY_TIME_ERROR, LOBBY_START_DATE_ERROR,
                            MATCH_START_DATE_ERROR, LOBBY_START_TIME_ERROR, PLAYER_COUNT_RANGE_ERROR)
from nimda.messages import TOPIC_NAME_VALIDATION, LOBBY_NAME_VALIDATION
```

## Helper Functions

These helper functions are used to validate and process game demos and lobbies:

- `if_exist_replace_with_demo(replace_with_demo_id)`: Checks if a demo exists to be replaced.
- `if_replace_with_demo_is_pinned(replace_with_demo_id)`: Checks if the demo to be replaced is pinned.
- `if_max_allowed_pinned_demo_already_set()`: Checks if the maximum number of allowed pinned demos is already set.
- `is_lobby_mode_allowed(game_id, mode, game_type)`: Validates if a lobby mode is allowed for a given game and type.

## Serializers

### AddGameSerializer

This serializer handles the addition of new games by Ryvals admins. It requires fields like game name, type, status, and images.

**Fields:**
- `id`
- `name`
- `type`
- `description`
- `status`
- `logo`
- `background_image`
- `game_demo_background_image`

```python
class AddGameSerializer(serializers.Serializer):
    ...
```

### GameUpdateAdminSerializer

Allows administrators to update game-related details such as background images and rules.

**Fields:**
- `game_demo_background_image`
- `background_image`
- `traditional_image`
- `killrace_image`
- `game_rules`
- `helper_image`

```python
class GameUpdateAdminSerializer(serializers.Serializer):
    ...
```

### AddRuleSerializer

This serializer is used to add rule templates for games.

**Fields:**
- `id`
- `name`
- `rules`

```python
class AddRuleSerializer(serializers.Serializer):
    ...
```

### AddLobbySerializer

Handles the creation of lobbies for games, including settings like player limits, game type, and schedule.

**Fields:**
- `id`
- `game_id`
- `name`
- `mode`
- `game_type`
- `min_players`
- `max_players`
- `start_date`
- `start_time`
- `last_entry_time`
- `status`
- `reward`
- `entry_fee`
- `is_verified`
- `rules`
- `admin_id`
- `admin_code`
- `participant_code`
- `stats_code`
- `free_lobby`
- `gamemap`
- `region`
- `lobby_password`
- `is_manual`
- `tournament_id`

```python
class AddLobbySerializer(serializers.Serializer):
    ...
```

### AddGameDemoSerializer

Allows adding a demo video or content related to a game.

**Fields:**
- `id`
- `game_id`
- `title`
- `status`
- `content`
- `video`
- `is_pinned`

```python
class AddGameDemoSerializer(serializers.Serializer):
    ...
```

### UpdateLobbySerializer

Serializer for updating the details of an existing lobby, including schedule and configuration changes.

**Fields:**
- `game_id`
- `name`
- `min_players`
- `max_players`
- `start_date`
- `start_time`
- `last_entry_time`
- `status`
- `reward`
- `entry_fee`
- `is_verified`
- `rules`
- `game_type`
- `current_status`
- `admin_id`
- `admin_code`
- `participant_code`
- `stats_code`
- `free_lobby`
- `mode`
- `gamemap`
- `region`
- `lobby_password`
- `is_manual`

```python
class UpdateLobbySerializer(serializers.Serializer):
    ...
```

### UpdateGameDemoSerializer

This serializer updates the details of a game demo, including its pinning status.

**Fields:**
- `game_id`
- `title`
- `status`
- `content`
- `video`
- `is_pinned`

```python
class UpdateGameDemoSerializer(serializers.Serializer):
    ...
```

### PlayerSerializer

Serializes player details for lobby lists.

**Fields:**
- `id`
- `first_name`
- `last_name`
- `username`
- `email`
- `phone`
- `discord_id`
- `gaming_account`
- `stats_required`

```python
class PlayerSerializer(serializers.Serializer):
    ...
```

### TeamPlayerSerializer

Serializes team player details for lobby lists.

**Fields:**
- `id`
- `first_name`
- `last_name`
- `username`
- `email`
- `phone`
- `team_id`
- `team_name`
- `discord_id`
- `has_paid`
- `is_owner`
- `status`
- `gaming_account`
- `stats_required`

```python
class TeamPlayerSerializer(serializers.Serializer):
    ...
```

### LobbyListDetailAdminSerializer

Provides detailed serializing of lobbies for admin views, including players and configurations.

**Fields:**
- `admin`
- `lobby_players`
- `pubg_results`
- `free_lobby`
- `admin_removed_players`
- `is_last_entry_time_ended`

```python
class LobbyListDetailAdminSerializer(LobbyListSerializer):
    ...
```

### GameDemoListDetailAdminSerializer

Serializes game demos for detailed admin views, including pinning status.

**Fields:**
- `max_allowed_pinned_demo`

```python
class GameDemoListDetailAdminSerializer(GameDemoListSerializer):
    ...
```

### UpdateLobbyActivationStatusSerializer

Handles the update of a lobby's activation status.

**Fields:**
- `status`

```python
class UpdateLobbyActivationStatusSerializer(serializers.Serializer):
    ...
```

### RemovePlayerFromLobbySerializer

Manages the removal of a player from a lobby and handles relevant transactions and notifications.

**Fields:**
- `player_id`
- `lobby_id`
- `reason`

```python
class RemovePlayerFromLobbySerializer(serializers.Serializer):
    ...
```

### RemoveTeamFromLobbySerializer

Facilitates the removal of a team from a lobby, handling necessary refunds and notifications.

**Fields:**
- `team_id`
- `lobby_id`
- `reason`

```python
class RemoveTeamFromLobbySerializer(serializers.Serializer):
    ...
```

### ComplaintListSerializer

Serializes a list of complaints filed by users against other players.

**Fields:**
- `reporter`
- `lobby`
- `offender`

```python
class ComplaintListSerializer(serializers.ModelSerializer):
    ...
```

### ComplaintDetailSerializer

Provides detailed serialization for a specific complaint.

```python
class ComplaintDetailSerializer(ComplaintListSerializer):
    ...
```

### UpdatedLobbyStatsFileCountSerializer

Updates image count and list for lobby stats, specifically for PUBG stats.

**Fields:**
- `count`
- `pubg_images`

```python
class UpdatedLobbyStatsFileCountSerializer(serializers.Serializer):
    ...
```

### EnrolledPlayerStatsUpdateSerializer

Updates player statistics for enrolled players by the admin.

**Fields:**
- `users`
- `status`

```python
class EnrolledPlayerStatsUpdateSerializer(serializers.Serializer):
    ...
```

### TransactionsReportUnclaimedMoneySerializer

Serializes data for reporting unclaimed money from transactions.

**Fields:**
- `lobby`
- `name_of_the_game`
- `winning_amount`
- `total_kills`
- `start_date`
- `total_enrollment_money`
- `ryvals_share`
- `unclaimed_money`
- `entry_fee`
- `reward`

```python
class TransactionsReportUnclaimedMoneySerializer(serializers.ModelSerializer):
    ...
```

### TransactionsReportDormantMoneySerializer

Serializes data for reporting dormant money from transactions.

**Fields:**
- `user_id`
- `username`
- `email`
- `wallet_balance`
- `inactivity_timeline`
- `inactivity_charges`
- `last_enrollement_date`
- `last_activity`

```python
class TransactionsReportDormantMoneySerializer(serializers.ModelSerializer):
    ...
```

### TransactionsReportSerializer

Serializes transaction details for reporting purposes.

**Fields:**
- `player`
- `transaction_id`
- `name_of_the_game`
- `transaction_type`
- `transaction_amount`
- `create_date`
- `status`
- `ryvals_share`
- `transaction_fee`
- `lobby_name`
- `payment_method`

```python
class TransactionsReportSerializer(serializers.ModelSerializer):
    ...
```

### UpdateAdminChallengeSerializer

Updates admin challenge game codes.

**Fields:**
- `admin_id`
- `admin_code`
- `participant_code`
- `stats_code`

```python
class UpdateAdminChallengeSerializer(serializers.Serializer):
    ...
```

This documentation provides an overview of the serializers used to manage various game-related functionalities within the Ryvals application, with detailed explanations of their roles and the fields they require.