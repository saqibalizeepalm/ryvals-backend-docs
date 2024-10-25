# Documentation for `apex.py`

This documentation provides an in-depth look into the `apex.py` file, detailing its purpose, structure, and functionality within the project. The file is designed to handle operations related to the game Apex Legends, leveraging a set of methods to manage game behavior, rules, and conditions.

## Table of Contents
- [Overview](#overview)
- [Class: ApexGameMethods](#class-apexgamemethods)
  - [Method: addgame](#method-addgame)
  - [Method: available_mode](#method-available_mode)
  - [Method: updategame](#method-updategame)
  - [Method: game_condition](#method-game_condition)

## Overview
The `apex.py` file is a specialized module that encapsulates the functionality specific to the game Apex Legends. It extends common game-related methods by implementing the `ApexGameMethods` class, which inherits from `GameBaseCommonMethods`. The main purpose of this module is to define and manage game-specific logic and constraints.

## Class: `ApexGameMethods`

### **Purpose**: 
The `ApexGameMethods` class is responsible for managing and validating various aspects of an Apex Legends game session, including its setup, allowed modes, status updates, and game conditions.

### Method: `addgame`
```python
def addgame(self, data):
    if data['admin_code'] and data['participant_code'] and data['stats_code']:
        return True, SUCCESS
    return False, APEX_STATS_MSG
```

#### **Description**:
- **Purpose**: Validates the presence of necessary codes (`admin_code`, `participant_code`, and `stats_code`) required to add a game.
- **Parameters**: `data` - Dictionary containing game-related data.
- **Returns**: A tuple indicating success (`True`) or failure (`False`) with an appropriate message.

#### **Usage**:
This method is used to ensure that all necessary codes are provided before a game can be successfully added.

### Method: `available_mode`
```python
def available_mode(self, game):
    allowed_mode = [Challenge.Mode.SOLO, Challenge.Mode.DUO, Challenge.Mode.TRIO, Challenge.Mode.HEXA]
    return [{'mode':mode, 'modetag':Challenge.ModeConvertTag(mode).label, 'mode_type':Challenge.Mode(mode).label} for mode in allowed_mode]
```

#### **Description**:
- **Purpose**: Returns a list of available game modes for Apex Legends.
- **Parameters**: `game` - The game instance for which modes are determined.
- **Returns**: A list of dictionaries, each containing mode information.

#### **Usage**:
This method provides a structured way to list all modes that Apex Legends supports, allowing for dynamic mode handling in the application.

### Method: `updategame`
```python
def updategame(self, data):
    current_status = data.get('current_status')
    is_manual = data.get('is_manual')
    if current_status == Lobby.CurrentStatus.ACTIVE and not is_manual:
        return False, ACTIVE_LOBBY_ERROR
    elif current_status == Lobby.CurrentStatus.ENDED:
        return False, ENDED_LOBBY_ERROR
    elif current_status == Lobby.CurrentStatus.UPCOMING:
        return True, SUCCESS
    else:
        return True, SUCCESS
```

#### **Description**:
- **Purpose**: Updates the game status and checks for any errors based on the current status.
- **Parameters**: `data` - Dictionary containing the game data to update.
- **Returns**: A tuple indicating success or specific errors related to the game status.

#### **Usage**:
This method is crucial for managing game state transitions and ensuring that manual interventions are accounted for.

### Method: `game_condition`
```python
def game_condition(self, start_datetime, current_datetime, last_entry_datetime, current_status, is_manual):
    if start_datetime < current_datetime and not is_manual:
        return False, LOBBY_START_DATE_ERROR
    if (last_entry_datetime < current_datetime or last_entry_datetime > start_datetime) and not is_manual:
        return False, LOBBY_LAST_ENTRY_TIME_ERROR
    return True, SUCCESS
```

#### **Description**:
- **Purpose**: Validates the timing conditions for starting a game.
- **Parameters**: 
  - `start_datetime`: Scheduled start time.
  - `current_datetime`: Current time.
  - `last_entry_datetime`: Last allowable time for entry.
  - `current_status`: Current status of the lobby.
  - `is_manual`: Boolean indicating if the operation is manual.
- **Returns**: A tuple indicating if the game can proceed (`True, SUCCESS`) or a specific error message.

#### **Usage**:
This method is used to enforce timing rules for games, ensuring that games start at the correct time and that entries are valid.

## Conclusion
The `apex.py` file is an essential component for handling Apex Legends-specific logic within the application's gaming platform. By extending common methods and implementing game-specific rules, it provides a robust framework for managing game sessions and ensuring compliance with predefined conditions.