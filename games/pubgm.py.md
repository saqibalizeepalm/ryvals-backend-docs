# PUBG Mobile (PUBGM) Game Methods Documentation 📚🎮

## Introduction
The `pubgm.py` file is part of a gaming application backend. It contains the implementation of methods specific to PlayerUnknown's Battlegrounds Mobile (PUBGM) within the application. This file defines the methods used to manage game functionality such as adding new games, updating games, and checking game conditions.

---

## Table of Contents
- [Imports](#imports)
- [Class: PUBGMGameMethods](#class-pubgmagemethods)
  - [Method: addgame](#method-addgame)
  - [Method: available_mode](#method-available_mode)
  - [Method: updategame](#method-updategame)
  - [Method: game_condition](#method-game_condition)

---

## Imports
The file starts with a series of import statements that bring in necessary modules and classes:

```python
from games.models import Game, Lobby
from players.models import Challenge
from games.base import GameBaseCommonMethods
from games.core.messages import GAME_STATS_MSG, SUCCESS, PUBG_TOKEN_REQUIRED, LOBBY_ACTIVE, LOBBY_ENDED, SOMTHING_WENT_WRONG
from games.messages import (LOBBY_START_DATE_ERROR, LOBBY_LAST_ENTRY_TIME_ERROR)
```

- **games.models**: Provides access to the `Game` and `Lobby` models.
- **players.models**: Provides access to the `Challenge` model.
- **games.base**: The base class for common game methods.
- **games.core.messages**: Contains constant messages for game statuses.
- **games.messages**: Contains error messages related to lobby timing and conditions.

---

## Class: PUBGMGameMethods
This class is a subclass of `GameBaseCommonMethods` and it encapsulates methods specific to PUBG Mobile.

```python
class PUBGMGameMethods(GameBaseCommonMethods):
```

### Method: addgame
Adds a game based on the provided data.

```python
def addgame(self, data):
    return True, SUCCESS
```

- **Parameters**: `data` - A dictionary containing game-related information.
- **Returns**: A tuple `(True, SUCCESS)`, indicating the operation was successful.

### Method: available_mode
Returns a list of available modes for a given game.

```python
def available_mode(self, game):
    allowed_mode = [Challenge.Mode.SOLO, Challenge.Mode.DUO, Challenge.Mode.QUAD]
    return [{'mode': mode, 'modetag': Challenge.ModeConvertTag(mode).label, 'mode_type': Challenge.Mode(mode).label} for mode in allowed_mode]
```

- **Parameters**: `game` - The game for which modes are being queried.
- **Returns**: A list of dictionaries, each containing information about a mode (`mode`, `modetag`, and `mode_type`).

### Method: updategame
Updates the game status based on the provided data.

```python
def updategame(self, data):
    current_status = data.get('current_status')
    is_manual = data.get('is_manual')
    if current_status == Lobby.CurrentStatus.ACTIVE and not is_manual:
        return False, LOBBY_ACTIVE
    elif current_status == Lobby.CurrentStatus.ACTIVE and is_manual:
        return True, SUCCESS
    elif current_status == Lobby.CurrentStatus.ENDED:
        return False, LOBBY_ENDED
    elif current_status == Lobby.CurrentStatus.UPCOMING:
        return True, SUCCESS
    return False, SOMTHING_WENT_WRONG
```

- **Parameters**: `data` - A dictionary containing current game status and manual status.
- **Returns**: A tuple indicating success or failure, along with a relevant message.

### Method: game_condition
Checks if the game conditions such as start date and last entry time are valid.

```python
def game_condition(self, start_datetime, current_datetime, last_entry_datetime, current_status, is_manual):
    if start_datetime < current_datetime and not is_manual:
        return False, LOBBY_START_DATE_ERROR
    if (last_entry_datetime < current_datetime or last_entry_datetime > start_datetime) and not is_manual:
        return False, LOBBY_LAST_ENTRY_TIME_ERROR
    return True, SUCCESS
```

- **Parameters**:
  - `start_datetime`: The start date and time of the game.
  - `current_datetime`: The current date and time.
  - `last_entry_datetime`: The last entry date and time.
  - `current_status`: The current status of the game.
  - `is_manual`: Whether the game setup is manual.
- **Returns**: A tuple indicating success or failure, along with a relevant message.

---

## Conclusion
The `pubgm.py` file provides a clear structure for managing PUBG Mobile game functionalities within the application. It allows for the addition of games, checking available modes, updating game statuses, and validating game conditions effectively.