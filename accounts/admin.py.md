# 📚 Django Admin Configuration Documentation

Welcome to the documentation for the Django Admin configuration file, **`admin.py`**! This file is an integral part of your Django project, serving as the command center for managing the admin interface. Let's dive into what this file does and how it's structured.

## Table of Contents

1. [Introduction](#introduction)
2. [Key Imports](#key-imports)
3. [Custom Admin Classes](#custom-admin-classes)
   - [UserAdmin](#useradmin)
   - [AdminProfile](#adminprofile)
4. [Model Registration](#model-registration)
5. [Dynamic Model Registration](#dynamic-model-registration)
6. [Conclusion](#conclusion)

## Introduction

The **`admin.py`** file is used in Django projects to customize the admin interface, allowing administrators to manage models and their data efficiently. This file defines how models are displayed and interacted with within the Django admin panel.

## Key Imports

Before we dive into the functionality, let's take a look at the key imports:

```python
from django.apps import apps
from django.contrib import admin
from accounts.models import User, Profile
from games.models import Lobby
from players.models import Tournament, TournamentRound, TournamentMatch, TournamentSubMatch, \
    PPKTournamentSubMatch, PPKTournamentSubMatchTeam, PPKTournamentMatchWinnerTeams, Challenge, \
    VersusTeam, VersusTeamPlayer, TransactionDetail, GameAccount
from tournament.models import TournamentTeam, TournamentTeamInvite, RemovedTournamentTeam, GamePlayerRank
```

- **`django.apps`**: Used to get all registered models.
- **`django.contrib.admin`**: Provides functionalities to register models with the admin interface.
- **`accounts.models`**, **`games.models`**, **`players.models`**, **`tournament.models`**: These modules contain the models that will be registered for admin management.

## Custom Admin Classes

### UserAdmin

The **`UserAdmin`** class customizes the display and search fields for the `User` model in the admin interface.

```python
class UserAdmin(admin.ModelAdmin):
    list_display = ['email', 'username', 'first_name', 'last_name', 'role', 'status']
    search_fields = ['email', 'username', 'first_name', 'last_name']
```

- **`list_display`**: Specifies the fields to be displayed in the list view.
- **`search_fields`**: Specifies the fields that can be searched.

### AdminProfile

The **`AdminProfile`** class customizes the display and search fields for the `Profile` model.

```python
class AdminProfile(admin.ModelAdmin):
    list_display = [
        'user', 'is_verified', 'discord_id', 'wallet_balance', 'bonus_balance', 'seized_amount',
        'kyc_verification_status', 'free_lobby_limit',
    ]
    search_fields = ['user__email', 'user__username', 'user__first_name', 'user__last_name']
```

- **`list_display`**: Fields displayed in the admin list view for Profile.
- **`search_fields`**: Fields available for search in the admin interface.

## Model Registration

Specific models are registered with the admin, using the custom admin classes defined above:

```python
admin.site.register(User, UserAdmin)
admin.site.register(Profile, AdminProfile)
```

## Dynamic Model Registration

This section dynamically registers all models, excluding those in the `ignore_list`, with the admin interface. This approach reduces redundancy and ensures new models are automatically managed.

```python
models = apps.get_models()
ignore_list = [
    Tournament, TournamentRound, TournamentMatch, TournamentSubMatch, Lobby, PPKTournamentSubMatch,
    PPKTournamentSubMatchTeam, PPKTournamentMatchWinnerTeams, Challenge, VersusTeam, VersusTeamPlayer,
    TransactionDetail, TournamentTeam, TournamentTeamInvite, RemovedTournamentTeam, GamePlayerRank,
    GameAccount
]

for model in models:
    try:
        if model not in ignore_list:
            admin.site.register(model)
    except admin.sites.AlreadyRegistered:
        pass
```

- **`apps.get_models()`**: Retrieves all registered models in the project.
- **`ignore_list`**: A list of models that should not be automatically registered.
- **`admin.site.register(model)`**: Attempts to register each model not in the ignore list.

## Conclusion

The **`admin.py`** file is crucial for setting up and customizing the Django admin interface. By defining custom admin classes and dynamically registering models, this file helps maintain an efficient and organized admin panel. Use this configuration to manage data seamlessly and ensure administrators have the tools they need. 🎉

Feel free to modify and expand this setup to suit your specific project needs!