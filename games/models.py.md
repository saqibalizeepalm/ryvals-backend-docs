# Documentation for `models.py` 🗃️

This file defines the core data models for the games, lobbies, and related components in a Django application. These models are used to interact with the database and manage data related to gaming entities.

## Index 📑

1. [Game Model](#game-model)
2. [RuleTemplate Model](#ruletemplate-model)
3. [Lobby Model](#lobby-model)
4. [GameDemo Model](#gamedemo-model)
5. [ImageSlider Model](#imageslider-model)

## Game Model 🎮

The `Game` model represents different games available in the system. This model is essential for defining the properties and status of each game.

### Fields 📋

| Field Name              | Type                          | Description                             |
|-------------------------|-------------------------------|-----------------------------------------|
| `name`                  | `CharField`                   | Name of the game.                       |
| `type`                  | `PositiveSmallIntegerField`   | Type of game (e.g., Pay Per Kill).      |
| `game_status`           | `PositiveSmallIntegerField`   | Current status of the game.             |
| `description`           | `TextField`                   | Description of the game.                |
| `status`                | `PositiveSmallIntegerField`   | Activation status of the game.          |
| `slug`                  | `SlugField`                   | URL-friendly version of the game name.  |
| `logo`                  | `CharField`                   | URL to the game logo.                   |
| `background_image`      | `CharField`                   | URL to the background image.            |
| `min_players`           | `PositiveIntegerField`        | Minimum players required.               |
| `max_players`           | `PositiveIntegerField`        | Maximum players allowed.                |
| `code_required`         | `BooleanField`                | Indicates if a stats token is required. |
| `stats_class`           | `CharField`                   | Class for the game stats.               |
| `has_upload`            | `BooleanField`                | If file upload is required.             |
| `is_multiple_upload`    | `BooleanField`                | If multiple file uploads are allowed.   |
| `aws_bucket_name`       | `CharField`                   | AWS bucket name for file storage.       |
| `types_of_game`         | `MultiSelectField`            | Types of games (e.g., PPK, Kill Race).  |

### Methods 🛠️

- `__str__`: Returns the name of the game.
- `save`: Overrides the save method to auto-generate a slug if not provided.

### Meta Options ⚙️

- `verbose_name`: "Game"
- `verbose_name_plural`: "Games"

## RuleTemplate Model 📜

The `RuleTemplate` model is used to store templates of rules applied to games.

### Fields 📋

| Field Name | Type       | Description       |
|------------|------------|-------------------|
| `name`     | `CharField`| Name of the rule. |
| `rules`    | `TextField`| Content of rules. |

### Methods 🛠️

- `__str__`: Returns the name of the rule template.

### Meta Options ⚙️

- `verbose_name`: "Rule Template"
- `verbose_name_plural`: "Rule Templates"

## Lobby Model 🏟️

The `Lobby` model handles the details of game lobbies, including their status, game type, and timing details.

### Fields 📋

| Field Name                | Type                          | Description                                   |
|---------------------------|-------------------------------|-----------------------------------------------|
| `game`                    | `ForeignKey`                  | Reference to associated game.                 |
| `name`                    | `CharField`                   | Name of the lobby.                            |
| `mode`                    | `PositiveSmallIntegerField`   | Mode of the lobby (e.g., Solo, Duo).          |
| `game_type`               | `PositiveSmallIntegerField`   | Type of game in the lobby.                    |
| `min_players`             | `PositiveIntegerField`        | Minimum players for the lobby.                |
| `max_players`             | `PositiveIntegerField`        | Maximum players allowed in the lobby.         |
| `start_date`              | `DateField`                   | Date when the lobby starts.                   |
| `start_time`              | `TimeField`                   | Time when the lobby starts.                   |
| `end_time`                | `TimeField`                   | Time when the lobby ends.                     |
| `status`                  | `PositiveSmallIntegerField`   | Activation status of the lobby.               |
| `reward`                  | `DecimalField`                | Reward for the lobby.                         |
| `entry_fee`               | `IntegerField`                | Entry fee for joining the lobby.              |
| `is_verified`             | `BooleanField`                | Indicates if the lobby is verified.           |
| `lobby_password`          | `CharField`                   | Password for private lobbies.                 |
| `is_password_protected`   | `BooleanField`                | If the lobby is password protected.           |
| `tournament_id`           | `BigIntegerField`             | Identifier for associated tournaments.        |
| `rules`                   | `TextField`                   | Rules for the lobby.                          |

### Methods 🛠️

- `__str__`: Returns the name of the lobby.

### Meta Options ⚙️

- `verbose_name`: "Lobby"
- `verbose_name_plural`: "Lobbies"

### Signals 📡

- **post_delete**: Deletes associated Discord channels when a lobby is deleted.

## GameDemo Model 🎥

The `GameDemo` model stores information about game demos, including their content and status.

### Fields 📋

| Field Name | Type                          | Description                   |
|------------|-------------------------------|-------------------------------|
| `game`     | `ForeignKey`                  | Reference to associated game. |
| `title`    | `CharField`                   | Title of the demo.            |
| `status`   | `PositiveSmallIntegerField`   | Activation status.            |
| `content`  | `TextField`                   | Content of the demo.          |
| `video`    | `CharField`                   | URL to the demo video.        |
| `is_pinned`| `BooleanField`                | If the demo is pinned.        |

### Methods 🛠️

- `__str__`: Returns the title of the game demo.

### Meta Options ⚙️

- `verbose_name`: "Game Demo"
- `verbose_name_plural`: "Game Demos"

## ImageSlider Model 🌄

The `ImageSlider` model is used to manage images and their descriptions for an image slider feature.

### Fields 📋

| Field Name    | Type         | Description                   |
|---------------|--------------|-------------------------------|
| `image`       | `CharField`  | URL to the image.             |
| `description` | `CharField`  | Description of the image.     |
| `link`        | `URLField`   | Link associated with the image.|

### Methods 🛠️

- `__str__`: Returns a string description of the image and its link.

---

This documentation provides an overview of the models and their components in the `models.py` file. Each model plays a vital role in managing different aspects of the gaming system, from game details to lobby management and game demos.