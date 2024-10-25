# Documentation for `codwarzone.py` 📜

## Overview
The `codwarzone.py` file contains the implementation of methods specifically for handling the game logic related to Call of Duty: Warzone. This file defines the `CODWarzoneGameMethods` class, which is built upon common game functions provided by `GameBaseCommonMethods`. The class is responsible for defining the behavior and available modes for Call of Duty: Warzone lobbies.

### Key Components
- **Imports**: This file imports necessary modules like models and common function definitions from other parts of the application.
- **Class `CODWarzoneGameMethods`**: This class handles game-specific logic for Call of Duty: Warzone.

---

## Class: `CODWarzoneGameMethods` 🌟

This class extends the `GameBaseCommonMethods` to provide specific functionalities for Call of Duty: Warzone.

### Methods

#### 1. `addgame(self, data)`
- **Description**: This method is designed to handle the addition of a new game or lobby for Call of Duty: Warzone.
- **Parameters**:
  - `data`: A dictionary containing details about the game or lobby.
- **Returns**: 
  - `True, SUCCESS`: Indicates the game was added successfully.

```python
def addgame(self, data):
    return True, SUCCESS
```

#### 2. `available_mode(self, game)`
- **Description**: This method returns the available modes for Call of Duty: Warzone.
- **Parameters**:
  - `game`: The game instance for which modes are being fetched.
- **Returns**: A list of dictionaries containing mode details.
- **Modes**:
  - SOLO
  - DUO

```python
def available_mode(self, game):
    allowed_mode = [Challenge.Mode.SOLO, Challenge.Mode.DUO]
    return [{'mode': mode, 'modetag': Challenge.ModeConvertTag(mode).label, 'mode_type': Challenge.Mode(mode).label} for mode in allowed_mode]
```

#### 3. `updategame(self, data)`
- **Description**: This method updates the status of a Call of Duty: Warzone game or lobby.
- **Parameters**:
  - `data`: A dictionary containing the updated details about the game or lobby.
- **Returns**: A tuple indicating success or failure and a message.
- **Logic**:
  - Checks the current status of the lobby.
  - Handles different conditions based on whether the update is manual or automatic.

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

#### 4. `game_condition(self, start_datetime, current_datetime, last_entry_datetime, current_status, is_manual)`
- **Description**: This method checks the validity of game conditions such as start time and entry time.
- **Parameters**:
  - `start_datetime`: The start date and time of the game.
  - `current_datetime`: The current date and time.
  - `last_entry_datetime`: The last allowable entry time for the game.
  - `current_status`: The current status of the lobby.
  - `is_manual`: A flag indicating if the process is manual.
- **Returns**: A tuple indicating if the conditions are met and a message.

```python
def game_condition(self, start_datetime, current_datetime, last_entry_datetime, current_status, is_manual):
    if start_datetime < current_datetime and not is_manual:
        return False, LOBBY_START_DATE_ERROR
    if (last_entry_datetime < current_datetime or last_entry_datetime > start_datetime) and not is_manual:
        return False, LOBBY_LAST_ENTRY_TIME_ERROR
    return True, SUCCESS
```

---

## Summary
The `CODWarzoneGameMethods` class provides a structured way to handle game logic specific to Call of Duty: Warzone, including adding new games, checking available modes, updating game status, and validating game conditions. This ensures that the game experiences are managed efficiently and consistently.