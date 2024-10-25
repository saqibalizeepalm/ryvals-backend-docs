d# Documentation for `messages.py` 📜

The `messages.py` file is an essential part of the application, specifically designed to store and manage user-facing messages. These messages are used throughout the application to provide feedback to users about various operations. The file utilizes Django's translation capabilities to ensure that messages can be internationalized.

## Table of Contents
- [Overview](#overview)
- [Message Definitions](#message-definitions)
- [Usage](#usage)
- [Code Example](#code-example)

## Overview
The purpose of `messages.py` is to centralize all the user feedback messages that can be shown across the application. This approach makes it easy to manage and update messages, as well as facilitate the support of multiple languages using Django's `gettext_lazy`.

### Main Features
- **Centralized Message Management**: All messages are defined in one place.
- **Internationalization**: Ready for translation into different languages.
- **Ease of Use**: Provides standardized messages that can be used across different modules of the application.

## Message Definitions
Here are the primary messages defined in the file:

| Constant Name           | Message Description                                           |
|-------------------------|---------------------------------------------------------------|
| `SUCCESS`               | Indicates a successful operation.                             |
| `APEX_STATS_MSG`        | Indicates missing codes for Apex game setup.                  |
| `FORTNITE_STATS_MSG`    | Indicates missing participant code for Fortnite setup.        |
| `GAME_STATS_MSG`        | Indicates missing admin and participant codes.                |
| `PUBG_TOKEN_REQUIRED`   | Indicates that a stats code is required for PUBG.             |
| `LOBBY_ACTIVE`          | Warns that changes cannot be made to an active lobby.         |
| `LOBBY_ENDED`           | Warns that changes cannot be made to an ended lobby.          |
| `SOMTHING_WENT_WRONG`   | Generic error message indicating an unexpected error.         |
| `SERVER_REQUIRED`       | Indicates a missing server name for Valorant setup.           |
| `VALORANT_TOKEN`        | Indicates missing stats code for Valorant.                    |

## Usage
These messages are typically used in views, serializers, or models to provide feedback to the user. For example, when certain conditions are not met during a game setup, the appropriate message can be returned to inform the user of what went wrong.

### Example Usage
```python
from games.messages import SUCCESS, APEX_STATS_MSG

def setup_apex_game(data):
    if 'admin_code' in data and 'participant_code' in data and 'stats_code' in data:
        return True, SUCCESS
    return False, APEX_STATS_MSG
```

## Code Example
Below is the complete code for `messages.py`:

```python
from django.utils.translation import gettext_lazy as _

SUCCESS = _('Success')
APEX_STATS_MSG = _('Admin, Participant and Stats code is required.')
FORTNITE_STATS_MSG = _('Participant code is required.')
GAME_STATS_MSG = _('Admin and Participant code is required.')
PUBG_TOKEN_REQUIRED = _("Stats Code is required.")
LOBBY_ACTIVE = _('You not change anything if lobby is active.')
LOBBY_ENDED = _('You not change anything if lobby is Ended.')
SOMTHING_WENT_WRONG = _('Something went wrong please try again.')
SERVER_REQUIRED = _('Valorant server name is required.')
VALORANT_TOKEN = _('Valorant Stats code is required.')
```

## Conclusion
The `messages.py` file serves as a crucial component for managing user feedback within the application. By centralizing the messages and utilizing Django's translation capabilities, it enhances the maintainability and internationalization of the application.