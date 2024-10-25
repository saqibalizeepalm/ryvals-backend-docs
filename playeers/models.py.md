# Models.py Documentation

This documentation provides a detailed overview of the `models.py` file, which is a core component of a Django application dealing with tournaments, challenges, transactions, and other functionalities related to a gaming platform. The file includes a variety of models that define the database schema and business logic for the application.

---

## Table of Contents

1. [Imports and Setup](#imports-and-setup)
2. [Models Overview](#models-overview)
   - [Challenge](#challenge)
   - [Price](#price)
   - [Tournament](#tournament)
   - [TransactionDetail](#transactiondetail)
   - [AccountActivationStatusDetail](#accountactivationstatusdetail)
   - [GameAccount](#gameaccount)
   - [Complaint](#complaint)
   - [PlayerLobby](#playerlobby)
   - [StripeTransfer](#stripetransfer)
   - [FavouritePlayers](#favouriteplayers)
   - [Notifications](#notifications)
   - [VersusTeam](#versusteam)
   - [Team](#team)
   - [TeamLobby](#teamlobby)
   - [TeamPlayer](#teamplayer)
   - [RemovedLobbyPlayer](#removedlobbyplayer)
   - [VersusTeamPlayer](#versusteamplayer)
   - [Match](#match)
   - [MatchInvite](#matchinvite)
   - [StripeAccount](#stripeaccount)
   - [EASportsPlayer](#easportsplayer)
   - [TournamentRound](#tournamentround)
   - [TournamentMatch](#tournamentmatch)
   - [PPKTournamentMatchWinnerTeams](#ppktournamentmatchwinnerteams)
   - [PPKTournamentSubMatch](#ppktournamentsubmatch)
   - [PPKTournamentSubMatchTeam](#ppktournamentsubmatchteam)
   - [TournamentSubMatch](#tournamentsubmatch)
   - [Shift4SavedCards](#shift4savedcards)

---

## Imports and Setup

The file begins by importing necessary modules and settings:

```python
import logging
import json
import random
import string
import secrets

from django.db import models
from django.conf import settings
from django.utils import timezone
from accounts.models import Player
from games.models import Game, Lobby
from django.dispatch import receiver
from channels.layers import get_channel_layer
from ryvals.core.models import TimeStampModel
from django.contrib.auth import get_user_model
from django.db.models.signals import post_save
from asgiref.sync import async_to_sync, sync_to_async
from nimda.messages import CUSTOM_PERMISSION_GAME_MSG
from django.utils.translation import ugettext_lazy as _
```

### Logging
- **Logging** is set up using the `logging` module to track errors and other information.

### User Model
- **User** is defined using `get_user_model()` to ensure compatibility with custom user models.

---

## Models Overview

### Challenge

- **Purpose**: Represents a challenge created by a player for another team.
- **Fields**:
  - `mode`, `game`, `player`, `match_date`, `match_time`, etc.
- **Permissions**:
  - Custom permission to upload and publish challenges.

### Price

- **Purpose**: Defines the price for a particular position in a tournament.
- **Fields**:
  - `position`, `price`

### Tournament

- **Purpose**: Represents a tournament with various configurations.
- **Fields**:
  - `name`, `game_type`, `entry_fee`, `status`, etc.
- **Choices**:
  - `GameType`, `Bracket`, `Seeding`, `Status`.

### TransactionDetail

- **Purpose**: Logs monetary transactions for players.
- **Fields**:
  - `transaction_number`, `payee`, `amount`, `status`, etc.
- **Choices**:
  - `Type`, `Status`, `Mode`, `PaymentMethod`.

### AccountActivationStatusDetail

- **Purpose**: Records reasons for account activation or deactivation.
- **Fields**:
  - `user`, `status`, `reason`.

### GameAccount

- **Purpose**: Links players with their gaming accounts.
- **Fields**:
  - `player`, `game`, `gaming_account`.

### Complaint

- **Purpose**: Logs complaints filed by players against others.
- **Fields**:
  - `reporter`, `lobby`, `offender`, `message`, `status`.

### PlayerLobby

- **Purpose**: Tracks lobbies that players enroll in.
- **Fields**:
  - `player`, `lobby`, `kills`, `team_placement`, etc.

### StripeTransfer

- **Purpose**: Records Stripe transfers and manages refunds.
- **Fields**:
  - `transfer`, `lobby`, `player`, `tansfer_type`.

### FavouritePlayers

- **Purpose**: Manages favorite players for users.
- **Fields**:
  - `parent`, `favourite_player`.

### Notifications

- **Purpose**: Represents notifications sent to players.
- **Fields**:
  - `from_user`, `to_user`, `message`, `is_seen`, etc.

### VersusTeam

- **Purpose**: Represents a team created for versus matches.
- **Fields**:
  - `name`, `player`, `mode`, `game`.

### Team

- **Purpose**: Defines a generic team.
- **Fields**:
  - `name`, `player_count`.

### TeamLobby

- **Purpose**: Associates teams with lobbies.
- **Fields**:
  - `team`, `lobby`, `has_paid_total`.

### TeamPlayer

- **Purpose**: Manages players within a team.
- **Fields**:
  - `player`, `team`, `status`, `pay_type`.

### RemovedLobbyPlayer

- **Purpose**: Records players removed from a lobby by admin.
- **Fields**:
  - `player`, `lobby`, `reason`.

### VersusTeamPlayer

- **Purpose**: Tracks players in versus teams.
- **Fields**:
  - `team`, `player`, `leader`, `status`.

### Match

- **Purpose**: Represents matches between teams.
- **Fields**:
  - `team_1`, `team_2`, `winning_team`, `challenge`, `stats`.

### MatchInvite

- **Purpose**: Manages match invitations and payments.
- **Fields**:
  - `player`, `invite`, `team`, `match`, `challenge`.

### StripeAccount

- **Purpose**: Links Stripe accounts to players.
- **Fields**:
  - `account_id`, `player`, `payouts_enabled`.

### EASportsPlayer

- **Purpose**: Manages EA Sports players capable of making free challenges.
- **Fields**:
  - `player`, `is_active`.

### TournamentRound

- **Purpose**: Defines rounds within a tournament.
- **Fields**:
  - `round_number`, `matches`, `tournament`.

### TournamentMatch

- **Purpose**: Represents matches within a tournament.
- **Fields**:
  - `round`, `match_number`, `winner`, `tournament`.

### PPKTournamentMatchWinnerTeams

- **Purpose**: Tracks winner teams in PPK tournaments.
- **Fields**:
  - `match`, `team`, `team_position`.

### PPKTournamentSubMatch

- **Purpose**: Defines sub-matches within a PPK tournament.
- **Fields**:
  - `round`, `match`, `sub_match_number`, `lobby`.

### PPKTournamentSubMatchTeam

- **Purpose**: Manages teams within PPK tournament sub-matches.
- **Fields**:
  - `team`, `sub_match`, `team_position`, `kills`.

### TournamentSubMatch

- **Purpose**: Represents sub-matches within a tournament.
- **Fields**:
  - `round`, `match`, `sub_match_number`, `lobby`.

### Shift4SavedCards

- **Purpose**: Manages saved cards for transactions.
- **Fields**:
  - `token`, `user`, `transaction_id`, `card_number`.

---

This documentation covers the core functionality and fields of each model in the `models.py` file, providing a comprehensive guide to the database schema and business logic implemented in the application.