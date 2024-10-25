# Documentation for `cod.py` 🎮

This documentation provides an overview of the `cod.py` file, which contains methods related to the Call of Duty game functionalities. The methods are designed to manage game settings, modes, and conditions for lobbies within the game.

## Table of Contents
1. [Overview](#overview)
2. [Classes and Methods](#classes-and-methods)
   - [CODMGameMethods](#codmgamemethods)
     - [addgame()](#addgame)
     - [available_mode()](#available_mode)
     - [updategame()](#updategame)
     - [game_condition()](#game_condition)
3. [Constants and Imports](#constants-and-imports)

## Overview
The `cod.py` file is part of a larger gaming application and defines functionalities specific to the Call of Duty Mobile game. It extends common game methods and provides game-specific implementations for setting up and managing game lobbies, handling game modes, and validating game conditions.

## Classes and Methods

### CODMGameMethods
The `CODMGameMethods` class extends `GameBaseCommonMethods` and provides specific implementations for Call of Duty Mobile. It includes methods to add games, list available modes, update game status, and verify game conditions.

#### `addgame(self, data)`
- **Description**: Returns a success message when a game is added.
- **Parameters**: 
  - `data` (dict): Data containing game information.
- **Returns**: Tuple (bool, str) - Status of the addition and a success message.

```python
def addgame(self, data):
    return True, SUCCESS
```

#### `available_mode(self, game)`
- **Description**: Lists available game modes for Call of Duty Mobile.
- **Parameters**: 
  - `game` (Game): The game object for which modes are listed.
- **Returns**: List of dictionaries containing mode details.

```python
def available_mode(self, game):
    allowed_mode = [Challenge.Mode.SOLO, Challenge.Mode.DUO, Challenge.Mode.QUAD]
    return [{'mode': mode, 'modetag': Challenge.ModeConvertTag(mode).label, 'mode_type': Challenge.Mode(mode).label} for mode in allowed_mode]
```

#### `updategame(self, data)`
- **Description**: Updates the game status based on current status and manual settings.
- **Parameters**: 
  - `data` (dict): Data containing current status and manual update flag.
- **Returns**: Tuple (bool, str) - Status of the update and a corresponding message.

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

#### `game_condition(self, start_datetime, current_datetime, last_entry_datetime, current_status, is_manual)`
- **Description**: Checks the conditions for game timing and status.
- **Parameters**: 
  - `start_datetime` (datetime): Start date and time of the game.
  - `current_datetime` (datetime): Current date and time.
  - `last_entry_datetime` (datetime): Last entry date and time for the game.
  - `current_status` (Lobby.CurrentStatus): Current status of the lobby.
  - `is_manual` (bool): Flag indicating if the update is manual.
- **Returns**: Tuple (bool, str) - Whether the condition is met and a corresponding message.

```python
def game_condition(self, start_datetime, current_datetime, last_entry_datetime, current_status, is_manual):
    if start_datetime < current_datetime and not is_manual:
        return False, LOBBY_START_DATE_ERROR
    if (last_entry_datetime < current_datetime or last_entry_datetime > start_datetime) and not is_manual:
        return False, LOBBY_LAST_ENTRY_TIME_ERROR
    return True, SUCCESS
```

## Constants and Imports
The `cod.py` file utilizes several imports and constants to facilitate its functionality:

### Imports
- **Models**: `Game`, `Lobby`, `Challenge` from `games.models` and `players.models`
- **Base Methods**: `GameBaseCommonMethods` from `games.base`
- **Messages**: Various message constants from `games.core.messages` and `games.messages`

### Message Constants
- **Success and Error Messages**:
  - `SUCCESS`
  - `LOBBY_ACTIVE`
  - `LOBBY_ENDED`
  - `SOMTHING_WENT_WRONG`
  - `LOBBY_START_DATE_ERROR`
  - `LOBBY_LAST_ENTRY_TIME_ERROR`

This documentation provides a comprehensive overview of the `cod.py` file, explaining the purpose and functionality of each method and the overall class structure.