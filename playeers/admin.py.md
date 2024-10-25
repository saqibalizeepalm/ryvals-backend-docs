# Documentation for `admin.py` 🎉

## Overview 🚀

The `admin.py` file is a crucial component of a Django application that utilizes the Django admin interface to manage various models. This file defines custom admin classes for several models related to tournaments, challenges, versus teams, transactions, and gaming accounts. By customizing the admin interface, this file helps streamline the management and administration of these models, making it easier for administrators to view, search, and filter data efficiently.

## Index 📚

1. [Imports](#imports)
2. [Admin Classes](#admin-classes)
   - [AdminTournament](#admintournament)
   - [AdminTournamentRound](#admintournamentround)
   - [AdminTournamentMatch](#admintournamentmatch)
   - [AdminTournamentSubMatch](#admintournamentsubmatch)
   - [AdminPPKTournamentSubMatch](#adminppktournamentsubmatch)
   - [AdminPPKTournamentSubMatchTeam](#adminppktournamentsubmatchteam)
   - [AdminPPKTournamentMatchWinnerTeams](#adminppktournamentmatchwinnerteams)
   - [AdminChallenge](#adminchallenge)
   - [AdminVersusTeam](#adminversusteam)
   - [AdminVersusTeamPlayer](#adminversusteamplayer)
   - [AdminTransactionDetail](#admintransactiondetail)
   - [AdminGameAccount](#admingameaccount)
3. [Admin Registration](#admin-registration)

## Imports 📦

```python
from django.contrib import admin
from players.models import (
    Tournament, TournamentRound, TournamentMatch, TournamentSubMatch, 
    PPKTournamentSubMatch, PPKTournamentSubMatchTeam, 
    PPKTournamentMatchWinnerTeams, Challenge, VersusTeam, 
    VersusTeamPlayer, TransactionDetail, GameAccount
)
```

- **Django Admin Module**: This is imported to create custom admin interfaces.
- **Models**: Various models related to tournaments, challenges, and transactions are imported from the `players.models` module.

## Admin Classes 🛠️

### AdminTournament

Customizes the admin interface for the `Tournament` model.

- **list_display**: Displays key fields like `id`, `name`, `game`, etc.
- **search_fields**: Enables searching by fields like `id`, `name`, and `game_type`.
- **list_filter**: Allows filtering by `game_type` and `game__name`.

### AdminTournamentRound

Customizes the admin interface for the `TournamentRound` model.

- **list_display**: Displays fields such as `id`, `tournament_name`, `round_number`, and `matches`.
- **search_fields**: Enables searching by `tournament__name`.

### AdminTournamentMatch

Customizes the admin interface for the `TournamentMatch` model.

- **list_display**: Displays fields like `id`, `tournament_name`, `winner`, etc.
- **search_fields**: Enables searching by `tournament__name` and `admin__username`.

### AdminTournamentSubMatch

Customizes the admin interface for the `TournamentSubMatch` model.

- **list_display**: Displays fields such as `id`, `tournament_name`, `round_number`, etc.
- **search_fields**: Enables searching by `tournament__name` and `lobby__name`.

### AdminPPKTournamentSubMatch

Customizes the admin interface for the `PPKTournamentSubMatch` model.

- **list_display**: Displays fields like `id`, `round_number`, `match_number`, etc.
- **search_fields**: Enables searching by `tournament__name` and `lobby__name`.

### AdminPPKTournamentSubMatchTeam

Customizes the admin interface for the `PPKTournamentSubMatchTeam` model.

- **list_display**: Shows fields such as `id`, `tournament_name`, `team`, etc.
- **search_fields**: Enables searching by `sub_match__tournament__name`.

### AdminPPKTournamentMatchWinnerTeams

Customizes the admin interface for the `PPKTournamentMatchWinnerTeams` model.

- **list_display**: Displays fields like `id`, `tournament_name`, `match_number`, etc.
- **search_fields**: Enables searching by `match__tournament__name`.

### AdminChallenge

Customizes the admin interface for the `Challenge` model.

- **list_display**: Displays fields such as `id`, `mode`, `game_name`, `player`, etc.
- **search_fields**: Enables searching by `id` and `game__name`.
- **list_filter**: Allows filtering by `mode` and `game__name`.

### AdminVersusTeam

Customizes the admin interface for the `VersusTeam` model.

- **list_display**: Displays fields like `id`, `name`, `player`, etc.
- **search_fields**: Enables searching by `name`, `player__username`, and `game__name`.

### AdminVersusTeamPlayer

Customizes the admin interface for the `VersusTeamPlayer` model.

- **list_display**: Shows fields such as `id`, `team_name`, `player`, etc.
- **search_fields**: Enables searching by `player__username` and `team__name`.

### AdminTransactionDetail

Customizes the admin interface for the `TransactionDetail` model.

- **list_display**: Displays fields like `transaction_number`, `payee`, `receiver`, etc.
- **search_fields**: Enables searching by fields related to `payee`, `receiver`, `lobby`, and more.

### AdminGameAccount

Customizes the admin interface for the `GameAccount` model.

- **list_display**: Shows fields such as `id`, `player_username`, `game_name`, etc.
- **search_fields**: Enables searching by `player` related fields.

## Admin Registration 🗂️

The final section of the `admin.py` file registers all the models with their respective admin classes. This makes them accessible via the Django admin interface.

```python
admin.site.register(Tournament, AdminTournament)
admin.site.register(TournamentRound, AdminTournamentRound)
admin.site.register(TournamentMatch, AdminTournamentMatch)
admin.site.register(TournamentSubMatch, AdminTournamentSubMatch)
admin.site.register(PPKTournamentSubMatch, AdminPPKTournamentSubMatch)
admin.site.register(PPKTournamentSubMatchTeam, AdminPPKTournamentSubMatchTeam)
admin.site.register(PPKTournamentMatchWinnerTeams, AdminPPKTournamentMatchWinnerTeams)
admin.site.register(Challenge, AdminChallenge)
admin.site.register(VersusTeam, AdminVersusTeam)
admin.site.register(VersusTeamPlayer, AdminVersusTeamPlayer)
admin.site.register(TransactionDetail, AdminTransactionDetail)
admin.site.register(GameAccount, AdminGameAccount)
```

By registering these models, you ensure they are available for management through the Django admin site, allowing for efficient data manipulation and oversight.