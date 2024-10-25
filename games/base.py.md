# Documentation for `base.py` 🕹️

## Overview
The `base.py` file defines a series of common methods used across various games within the application. These methods encapsulate logic for game statistics and game state management, providing a centralized location for shared functionality. This promotes code reuse and clarity throughout the project.

## Table of Contents
1. [Import Statements](#import-statements)
2. [GameBaseCommonMethods Class](#gamebasecommonmethods-class)
   - [Methods](#methods)

---

## Import Statements
The file begins with a series of import statements, bringing in necessary modules and constants from other parts of the application:

```python
from games.models import Lobby
from games.core.messages import SUCCESS
from games.messages import (
    LOBBY_START_DATE_ERROR, 
    LOBBY_LAST_ENTRY_TIME_ERROR
)
from games.core.messages import SUCCESS, LOBBY_ACTIVE, LOBBY_ENDED, SOMTHING_WENT_WRONG
```

- **Lobby**: Model representing a game lobby.
- **Messages**: Various constants representing success and error messages, aiding in user feedback and logging.

## GameBaseCommonMethods Class
The primary component of this file is the `GameBaseCommonMethods` class, which serves as a utility class containing methods relevant to game operations.

### Methods

#### 1. `apex_stats(self)`
```python
def apex_stats(self):
    print("getting the apex game stats")
```
- **Purpose**: This method is a placeholder for retrieving statistics related to the game "Apex". It currently prints a message indicating its intended function.

#### 2. `pubg_stats(self)`
```python
def pubg_stats(self):
    print("getting the pubg stats")
```
- **Purpose**: Similar to `apex_stats`, this method is a placeholder for gathering "PUBG" game statistics, currently outputting a simple print statement.

#### 3. `cod_stats(self)`
```python
def cod_stats(self):
    print("getting the cod stats")
```
- **Purpose**: A placeholder method for "Call of Duty" statistics, indicating with a print statement that such functionality is planned.

#### 4. `updategame(self, data)`
```python
def updategame(self, data):
    current_status = data.get('current_status')
    if current_status == Lobby.CurrentStatus.ACTIVE:
        return False, LOBBY_ACTIVE
    elif current_status == Lobby.CurrentStatus.ENDED:
        return False, LOBBY_ENDED
    elif current_status == Lobby.CurrentStatus.UPCOMING:
        return True, SUCCESS
    return False, SOMTHING_WENT_WRONG
```
- **Purpose**: Evaluates and updates the game status based on the current status of the lobby.
- **Parameters**: 
  - `data`: Dictionary containing `current_status`.
- **Returns**: A tuple indicating success status and a message.

#### 5. `game_condition(self, start_datetime, current_datetime, last_entry_datetime, current_status)`
```python
def game_condition(self, start_datetime, current_datetime, last_entry_datetime, current_status):
    if start_datetime < current_datetime:
        return False, LOBBY_START_DATE_ERROR
    if last_entry_datetime < current_datetime or last_entry_datetime > start_datetime:
        return False, LOBBY_LAST_ENTRY_TIME_ERROR
    return True, SUCCESS
```
- **Purpose**: Checks if the game conditions are met based on provided datetime objects.
- **Parameters**:
  - `start_datetime`: The start time of the game.
  - `current_datetime`: The current time.
  - `last_entry_datetime`: The last permissible entry time.
  - `current_status`: The current status of the game.
- **Returns**: A tuple indicating whether conditions are satisfied and an associated message.

---

## Conclusion
The `base.py` file is essential for providing reusable methods that manage game-specific operations and status checks. By centralizing these methods, the file enhances maintainability and ensures consistent functionality across different game modules. Future expansions could involve replacing the placeholder methods with actual implementations for fetching game statistics.