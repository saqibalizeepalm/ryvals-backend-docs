# Documentation for `fortnite.py`

## Overview

The `fortnite.py` module is responsible for managing game-specific operations and features related to Fortnite within a gaming platform. It extends the base functionality provided by `GameBaseCommonMethods` to include Fortnite-specific logic for adding games, determining available modes, updating game details, and handling game conditions.

## Classes and Methods

### FortniteGameMethods

This class encapsulates the methods specific to handling Fortnite gaming functionalities.

#### Methods:

- **`addgame(self, data)`**
  - **Description:** This method is used to add a Fortnite game using the provided data.
  - **Parameters:** 
    - `data`: A dictionary containing the necessary information for game creation.
  - **Returns:** A tuple `(True, SUCCESS)` indicating the success of game addition.

- **`available_mode(self, game)`**
  - **Description:** Provides the available modes for Fortnite games.
  - **Parameters:** 
    - `game`: An instance of the `Game` model representing the Fortnite game.
  - **Returns:** A list of dictionaries, each representing a mode with its tag and type.

- **`updategame(self, data)`**
  - **Description:** Updates the game status based on the current state and whether manual updates are allowed.
  - **Parameters:** 
    - `data`: A dictionary containing details about the current game status.
  - **Returns:** A tuple containing a Boolean and a message indicating the result of the update operation. Possible outcomes include:
    - `(False, ACTIVE_LOBBY_ERROR)` if the lobby is active and manual updates are not allowed.
    - `(False, ENDED_LOBBY_ERROR)` if the lobby has ended.
    - `(True, SUCCESS)` if the game is upcoming or updates are allowed.

- **`game_condition(self, start_datetime, current_datetime, last_entry_datetime, current_status, is_manual)`**
  - **Description:** Checks various game conditions to ensure the game setup is valid.
  - **Parameters:** 
    - `start_datetime`: The start date and time of the game.
    - `current_datetime`: The current date and time.
    - `last_entry_datetime`: The last entry date and time allowed for the game.
    - `current_status`: The current status of the game.
    - `is_manual`: A Boolean indicating if manual updates are permitted.
  - **Returns:** A tuple with a Boolean and a message indicating the result of the condition check. Possible outcomes include:
    - `(False, LOBBY_START_DATE_ERROR)` if the start date is in the past and manual updates are not allowed.
    - `(False, LOBBY_LAST_ENTRY_TIME_ERROR)` if the last entry time is invalid and manual updates are not allowed.
    - `(True, SUCCESS)` if all conditions are satisfied.

## Constants Imported

- **`SUCCESS`**: Indicates a successful operation.
- **`FORTNITE_STATS_MSG`**: Message indicating that participant code is required.
- **`ACTIVE_LOBBY_ERROR`**: Error message for active lobby.
- **`ENDED_LOBBY_ERROR`**: Error message for ended lobby.
- **`LOBBY_START_DATE_ERROR`**: Error message when the lobby start date is invalid.
- **`LOBBY_LAST_ENTRY_TIME_ERROR`**: Error message when the last entry time is invalid.

## Usage

The `FortniteGameMethods` class is used to handle all Fortnite-specific logic within the gaming platform. It provides methods to add games, determine available modes, update game statuses, and check game conditions, ensuring that all operations are consistent with the rules and constraints of the Fortnite game environment.

## Conclusion

The `fortnite.py` file is an integral part of the gaming platform, facilitating the management and operation of Fortnite games. By leveraging the base methods and extending them with game-specific logic, it ensures a seamless and efficient integration of Fortnite gaming mechanics into the broader system.