# Documentation for `serializers.py`

## Overview

This file, `serializers.py`, is part of a Django-based project. It utilizes Django REST Framework to define serializers, which are responsible for converting complex data types such as querysets and model instances into native Python data types. These can then be easily rendered into JSON or other content types. This file primarily focuses on the serialization of game-related entities such as Games, Lobbies, and Players.

## Index

1. [Imports](#1-imports)
2. [Serializers](#2-serializers)
   - [GameListSerializer](#game-list-serializer)
   - [GameDetailSerializer](#game-detail-serializer)
   - [PlayerStatsSerializer](#player-stats-serializer)
   - [LobbyListSerializer](#lobby-list-serializer)
   - [GameDemoListSerializer](#game-demo-list-serializer)
   - [LobbyDetailSerializer](#lobby-detail-serializer)
   - [RuleSerializer](#rule-serializer)
   - [EnrolledPlayerListSerializer](#enrolled-player-list-serializer)
   - [TeamSerializer](#team-serializer)
   - [ListRegisteredTeammatesSerializer](#list-registered-teammates-serializer)

---

## 1. Imports

```python
import math
import pytz
import json
import logging
from datetime import datetime, timedelta

from django.utils import timezone
from django.contrib.auth import get_user_model
from rest_framework import serializers
from rest_framework.exceptions import APIException
from django.utils.translation import gettext_lazy as _

from accounts.models import Player
from app.utils import UtilityMethods
from players.models import GameAccount, PlayerLobby, Team, TeamPlayer, TeamLobby, Tournament, PPKTournamentSubMatch, PPKTournamentSubMatchTeam, TournamentSubMatch
from tournament.models import TournamentTeamInvite
from nimda.models import Config
from games.core.factory import GameFactory
from games.messages import GAME_NOT_FOUND
from ryvals.core.messages import PLAYER_ONLY
from games.models import Game, Lobby, RuleTemplate, GameDemo
```

### Key Imports

- **Django and REST Framework Modules**: For timezone, authentication, and serialization.
- **Model Imports**: Includes essential models like `Game`, `Lobby`, `Player`, etc.
- **Utility Imports**: Utility methods and constants for operations and error messages.

---

## 2. Serializers

### GameListSerializer

**Purpose**: Serializes game data for listing purposes.

- **Fields**: ID, name, description, game type, slug, images, player limits, and more.
- **Custom Methods**:
  - `get_game_allowed_mode()`: Retrieves allowed game modes.
  - `get_game_type()`: Retrieves the label for the game type.

```python
class GameListSerializer(serializers.ModelSerializer):
    ''' Serializer for game listing for all users '''
    game_type = serializers.SerializerMethodField('get_game_type')
    game_allowed_mode = serializers.SerializerMethodField('get_game_allowed_mode')
    ...
```

### GameDetailSerializer

**Purpose**: Serializes detailed game data.

- **Fields**: Includes all fields from the `Game` model.

```python
class GameDetailSerializer(serializers.ModelSerializer):
    ''' Serializer for game detail view for all users '''
    class Meta:
        model = Game
        fields = '__all__'
```

### PlayerStatsSerializer

**Purpose**: Serializes player statistics in a lobby.

- **Fields**: Player's name, kills, assists, winnings, and more.
- **Custom Methods**:
  - `get_winnings()`: Calculates and returns player's winnings based on game and lobby type.
  - `get_team_name()`: Returns the team name for certain game types.

```python
class PlayerStatsSerializer(serializers.ModelSerializer):
    ''' Player Stats Serializer '''
    winnings = serializers.SerializerMethodField('get_winnings')
    team_name = serializers.SerializerMethodField('get_team_name')
    ...
```

### LobbyListSerializer

**Purpose**: Serializes lobby data for listing purposes.

- **Fields**: Includes game details, enrollment status, start and end times, and more.
- **Custom Methods**: 
  - `get_game()`: Retrieves game-related information.
  - `get_enrolment_status()`: Checks if the user is enrolled in the lobby.
  - Time-related calculations using `datetime`.

```python
class LobbyListSerializer(serializers.ModelSerializer):
    ''' Serializer for lobby list for all users '''
    TIME_STRING_FORMAT_CONST = '%I:%M %p %Z'
    game = serializers.SerializerMethodField('get_game')
    is_enrolled = serializers.SerializerMethodField('get_enrolment_status')
    ...
```

### GameDemoListSerializer

**Purpose**: Serializes game demo data for listing purposes.

- **Fields**: Game details, title, content, video, and status.

```python
class GameDemoListSerializer(serializers.ModelSerializer):
    ''' Serializer for game demo list for all users '''
    game = serializers.SerializerMethodField('get_game')
    ...
```

### LobbyDetailSerializer

**Purpose**: Serializes detailed lobby data, including match statistics.

- **Fields**: Extends fields from `LobbyListSerializer` and adds match statistics.
- **Custom Methods**:
  - `get_is_last_entry_time_ended()`: Determines if the last entry time has passed.

```python
class LobbyDetailSerializer(LobbyListSerializer):
    ''' Serializer for lobby detail view for all users '''
    match_stats = serializers.SerializerMethodField()
    is_last_entry_time_ended = serializers.SerializerMethodField()
    ...
```

### RuleSerializer

**Purpose**: Serializes rule templates.

- **Fields**: ID, name, and rules of the template.

```python
class RuleSerializer(serializers.ModelSerializer):
    class Meta:
        model = RuleTemplate
        fields = ['id', 'name', 'rules']
    ...
```

### EnrolledPlayerListSerializer

**Purpose**: Serializes a list of enrolled players in a lobby.

- **Fields**: Player ID, game account, email, phone number, Discord ID, and username.

```python
class EnrolledPlayerListSerializer(serializers.Serializer):
    ''' Serializer for list of enrolled players in a lobby '''
    id = serializers.SerializerMethodField('get_player_id')
    game_account = serializers.SerializerMethodField('get_game_account')
    ...
```

### TeamSerializer

**Purpose**: Serializes team information.

- **Fields**: Team ID, name, and player count.

```python
class TeamSerializer(serializers.ModelSerializer):
    ''' Team Serializer '''
    class Meta:
        model = Team
        fields = ['id', 'name', 'player_count']
```

### ListRegisteredTeammatesSerializer

**Purpose**: Serializes a list of registered teammates for a team in a lobby.

- **Fields**: Teammate details such as ID, name, email, Discord ID, and game account.

```python
class ListRegisteredTeammatesSerializer(serializers.ModelSerializer):
    ''' Serializer for list of registered teammates for a team in lobby '''
    uid = serializers.IntegerField(source='player.id')
    first_name = serializers.CharField(source='player.first_name')
    ...
```

---

**Note**: The serializers are crucial for API endpoints in the Django project, enabling the seamless conversion of data between complex data models and JSON format for client use.