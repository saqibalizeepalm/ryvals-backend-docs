# Documentation for `messages.py` 📜

The `messages.py` file is an essential component for managing user-facing messages within a Django application. This file specifically deals with error messages and notifications that are meant to guide users when they encounter issues or require confirmations regarding their actions on the platform.

## Table of Contents
- [Overview](#overview)
- [Purpose](#purpose)
- [Message Descriptions](#message-descriptions)
  - [LOBBY_NOT_FOUND](#lobby_not_found)
  - [GAME_NOT_FOUND](#game_not_found)
  - [PLAYER_COUNT_RANGE_ERROR](#player_count_range_error)
  - [LOBBY_START_DATE_ERROR](#lobby_start_date_error)
  - [MATCH_START_DATE_ERROR](#match_start_date_error)
  - [LOBBY_START_TIME_ERROR](#lobby_start_time_error)
  - [LOBBY_LAST_ENTRY_TIME_ERROR](#lobby_last_entry_time_error)
  - [MATCH_LAST_ENTRY_TIME_ERROR](#match_last_entry_time_error)
  - [ACCESS_NOT_ALLOWED](#access_not_allowed)
  - [UNEXPECTED_PROFILE_ERROR](#unexpected_profile_error)
  - [GAME_EITHER_DELETED_OR_DEACTIVATED](#game_either_deleted_or_deactivated)
- [Localization](#localization)

## Overview

The `messages.py` file utilizes Django's translation utilities to define a set of messages that can be displayed to users. These messages help in providing feedback, especially error notifications, enhancing user experience by informing users about what went wrong and suggesting corrective actions.

## Purpose

### Key Objectives:
- **Centralized Message Management**: Maintain a single source for all user-facing messages related to game lobbies and matches.
- **Error Guidance**: Help users understand what went wrong and how they can address the issue.
- **Localization Support**: Allow messages to be translated into different languages using Django's translation framework.

## Message Descriptions

Below are the detailed descriptions of each message defined in the file:

### LOBBY_NOT_FOUND
```python
LOBBY_NOT_FOUND = _('We were unable to find the lobby. Please try again.')
```
- **Purpose**: Informs the user that the specified lobby could not be located.

### GAME_NOT_FOUND
```python
GAME_NOT_FOUND = _('We could not find the game you were looking for. Please try again.')
```
- **Purpose**: Alerts the user that the game they are searching for is not available.

### PLAYER_COUNT_RANGE_ERROR
```python
PLAYER_COUNT_RANGE_ERROR = _('Minimum player count should be less than Maximum player count.')
```
- **Purpose**: Communicates an error when the user sets a minimum player count that is not less than the maximum.

### LOBBY_START_DATE_ERROR
```python
LOBBY_START_DATE_ERROR = _('Lobby start date should be set for a future date. Please try again.')
```
- **Purpose**: Notifies the user that the lobby start date must be in the future.

### MATCH_START_DATE_ERROR
```python
MATCH_START_DATE_ERROR = _('Match start date should be set for a future date. Please try again.')
```
- **Purpose**: Similar to `LOBBY_START_DATE_ERROR`, but specifically for match start dates.

### LOBBY_START_TIME_ERROR
```python
LOBBY_START_TIME_ERROR = _('Lobby start time should be set for a future time. Please try again.')
```
- **Purpose**: Ensures that the lobby start time is not set for a past time.

### LOBBY_LAST_ENTRY_TIME_ERROR
```python
LOBBY_LAST_ENTRY_TIME_ERROR = _('Lobby last entry time should be set for a future time and less than the lobby start time. Please try again.')
```
- **Purpose**: Validates that the last entry time for a lobby is before its start time and in the future.

### MATCH_LAST_ENTRY_TIME_ERROR
```python
MATCH_LAST_ENTRY_TIME_ERROR = _('Match last entry time should be set for a future time and less than the match start time. Please try again.')
```
- **Purpose**: Similar validation as `LOBBY_LAST_ENTRY_TIME_ERROR`, but for matches.

### ACCESS_NOT_ALLOWED
```python
ACCESS_NOT_ALLOWED = _('You need to get verified before accessing this page. Contact Chris to get started!')
```
- **Purpose**: Informs users that they need verification to access certain pages, with a contact point for assistance.

### UNEXPECTED_PROFILE_ERROR
```python
UNEXPECTED_PROFILE_ERROR = _('We couldn\'t find the appropriate lobbies for you. You might not have access to this page.')
```
- **Purpose**: Alerts users when there is an issue with accessing lobbies due to potential profile restrictions.

### GAME_EITHER_DELETED_OR_DEACTIVATED
```python
GAME_EITHER_DELETED_OR_DEACTIVATED = _('Game is either deleted or deactivated')
```
- **Purpose**: Notifies users that the game they are trying to access is no longer available.

## Localization

All messages are wrapped in Django's `_()` function from `django.utils.translation`, which allows for easy internationalization and localization of the application. This means that the messages can be translated into different languages to cater to a global audience. 

In conclusion, the `messages.py` file is a vital part of ensuring clear communication between the application and its users, by providing standardized and translatable message templates for various scenarios.