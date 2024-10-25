# Documentation for `valorant.py`

The `valorant.py` file is part of a larger project related to gaming applications, specifically for handling game logic and operations for the game Valorant. This file defines methods related to the management and operations of Valorant lobbies and game conditions.

## Table of Contents

1. [Overview](#overview)
2. [Classes and Methods](#classes-and-methods)
   - [ValorantGameMethods](#valorantgamemethods)
     - [addgame](#addgame-method)
     - [updategame](#updategame-method)
     - [game_condition](#game_condition-method)
     - [available_mode](#available_mode-method)
3. [Usage](#usage)

## Overview

The `valorant.py` file contains a class called `ValorantGameMethods`, which is responsible for handling various operations related to Valorant games in the application. These operations include adding a game, updating the game state, checking game conditions, and determining available game modes.

This class extends `GameBaseCommonMethods`, which likely provides some common functionality for different games.

## Classes and Methods

### ValorantGameMethods

The `ValorantGameMethods` class includes methods that handle Valorant-specific game logic.

#### `addgame` Method

```python
def addgame(self, data):
    return True, SUCCESS
```

- **Purpose**: This method is used to add a new Valorant game. The method currently always returns `True` and a success message, indicating the game was added successfully.
- **Parameters**: 
  - `data`: A dictionary or data object that contains the necessary information to add a game.

#### `updategame` Method

```python
def updategame(self, data):
    current_status = data.get('current_status')
    is_manual = data.get('is_manual')
    if current_status == Lobby.CurrentStatus.ACTIVE or current_status == Lobby.CurrentStatus.ENDED:
        return True, SUCCESS
    if current_status == Lobby.CurrentStatus.UPCOMING:
        return True, SUCCESS
    return False, VALORANT_TOKEN
```

- **Purpose**: To update the status of a Valorant game based on the current game status and whether it's manually updated.
- **Parameters**: 
  - `data`: A dictionary containing the current status and manual update flag of the game.
- **Returns**: 
  - A tuple `(bool, message)`, where the boolean indicates success or failure, and the message provides additional context.

#### `game_condition` Method

```python
def game_condition(self, start_datetime, current_datetime, last_entry_datetime, current_status, is_manual):
    if current_status == Lobby.CurrentStatus.UPCOMING:
        if start_datetime < current_datetime:
            return False, LOBBY_START_DATE_ERROR
        if last_entry_datetime < current_datetime or last_entry_datetime > start_datetime:
            return False, LOBBY_LAST_ENTRY_TIME_ERROR
    return True, SUCCESS
```

- **Purpose**: To verify if the game conditions are appropriate for a Valorant lobby to be valid.
- **Parameters**: 
  - `start_datetime`: The start date and time of the lobby.
  - `current_datetime`: The current date and time.
  - `last_entry_datetime`: The last entry date and time for the lobby.
  - `current_status`: The current status of the lobby.
  - `is_manual`: A flag indicating if the lobby is manually updated.
- **Returns**: A tuple with a boolean indicating if the conditions are met and a message detailing any errors or a success indicator.

#### `available_mode` Method

```python
def available_mode(self, game):
    allowed_mode = [Challenge.Mode.PENTA]
    return [{'mode':mode, 'modetag':Challenge.ModeConvertTag(mode).label, 'mode_type':Challenge.Mode(mode).label} for mode in allowed_mode]
```

- **Purpose**: To provide the available game modes for Valorant.
- **Parameters**: 
  - `game`: The game object or identifier for which available modes are being fetched.
- **Returns**: A list of dictionaries, each representing an available mode with its corresponding tags and labels.

## Usage

The `ValorantGameMethods` class is typically used within a larger gaming application to handle game-specific logic for Valorant. It can be integrated into views or services that manage game creation, updates, and validation of lobbies.

The methods provided allow for flexible and modular handling of Valorant game operations, ensuring that game logic is encapsulated and easily maintainable.