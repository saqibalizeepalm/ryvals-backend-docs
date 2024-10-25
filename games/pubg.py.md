# PUBG Module Documentation 🎮

Welcome to the documentation for the `pubg.py` module, which is part of a gaming application structure. This module specifically handles functionalities related to the popular game PlayerUnknown's Battlegrounds (PUBG).

This document provides an in-depth explanation of the code within the `pubg.py` file, describing its components, methods, and their purposes.

## Table of Contents 📑
1. [Overview](#overview)
2. [Imports](#imports)
3. [Class: PubgGameMethods](#class-pubggamemethods)
   - [Method: addgame](#method-addgame)
   - [Method: updategame](#method-updategame)
   - [Method: game_condition](#method-game_condition)
   - [Method: available_mode](#method-available_mode)

## Overview

The `pubg.py` module defines methods specific to handling PUBG game logic in the context of a gaming application. It uses the base methods provided by `GameBaseCommonMethods` and implements additional functionality required for PUBG.

## Imports

The module starts by importing necessary classes and methods from other parts of the application:

```python
from games.models import Game, Lobby
from players.models import Challenge
from games.base import GameBaseCommonMethods
from games.core.messages import GAME_STATS_MSG, SUCCESS, PUBG_TOKEN_REQUIRED
from games.messages import (LOBBY_START_DATE_ERROR, LOBBY_LAST_ENTRY_TIME_ERROR)
```

- **Game, Lobby**: Models representing game and lobby entities.
- **Challenge**: Model representing game challenges.
- **GameBaseCommonMethods**: Base class containing common methods for games.
- **Messages**: Constants used for status messages and errors.

## Class: PubgGameMethods

The `PubgGameMethods` class extends `GameBaseCommonMethods` and implements PUBG-specific logic. Here is a breakdown of its methods:

```python
class PubgGameMethods(GameBaseCommonMethods):
```

### Method: addgame

```python
def addgame(self, data):
    if data['admin_code'] and data['participant_code']:
        return True, SUCCESS
    return False, GAME_STATS_MSG
```

- **Purpose**: Validates the presence of necessary codes to add a game.
- **Parameters**: `data` - a dictionary containing game data including `admin_code` and `participant_code`.
- **Returns**: A tuple indicating success or failure with an appropriate message.

### Method: updategame

```python
def updategame(self, data):
    current_status = data.get('current_status')
    is_manual = data.get('is_manual')
    stats_code = data.get('stats_code')
    
    if stats_code and (current_status == Lobby.CurrentStatus.ACTIVE or current_status == Lobby.CurrentStatus.ENDED):
        return True, SUCCESS
    if current_status == Lobby.CurrentStatus.UPCOMING:
        return True, SUCCESS
    return False, PUBG_TOKEN_REQUIRED
```

- **Purpose**: Updates game information based on its current status and provided data.
- **Parameters**: `data` - a dictionary containing update data.
- **Returns**: A tuple indicating whether the update was successful along with a message.

### Method: game_condition

```python
def game_condition(self, start_datetime, current_datetime, last_entry_datetime, current_status, is_manual):
    if current_status == Lobby.CurrentStatus.UPCOMING:
        if start_datetime < current_datetime:
            return False, LOBBY_START_DATE_ERROR
        if last_entry_datetime < current_datetime or last_entry_datetime > start_datetime:
            return False, LOBBY_LAST_ENTRY_TIME_ERROR
    return True, SUCCESS
```

- **Purpose**: Checks the validity of game start and entry times based on its current status.
- **Parameters**: 
  - `start_datetime`: Scheduled start date and time of the lobby.
  - `current_datetime`: Current date and time.
  - `last_entry_datetime`: Last permissible entry date and time.
  - `current_status`: Current status of the lobby.
  - `is_manual`: Flag indicating if manual updates are allowed.
- **Returns**: A tuple indicating whether conditions are met for the game to start.

### Method: available_mode

```python
def available_mode(self, game):
    allowed_mode = [Challenge.Mode.SOLO, Challenge.Mode.DUO, Challenge.Mode.QUAD]
    return [{'mode': mode, 'modetag': Challenge.ModeConvertTag(mode).label, 'mode_type': Challenge.Mode(mode).label} for mode in allowed_mode]
```

- **Purpose**: Provides the available modes for PUBG.
- **Parameters**: `game` - the game entity for which modes are being retrieved.
- **Returns**: A list of dictionaries with mode details.

---

This document provides a comprehensive understanding of the `pubg.py` module's functionality within the gaming application. For further inquiries or detailed exploration, feel free to delve into the source code or associated modules. 🕹️