# Documentation for `models.py` 📄

## Overview
The `models.py` file is an integral part of the Django framework, where data models are defined. These models interact with the database, providing an abstraction layer to manage data in Python objects rather than complex SQL queries. This file in the application defines different models related to locations, community videos, configurations, permissions, logs, and various game-related actions.

## Index
- [Imports](#imports)
- [Model: RestrictLocation](#model-restrictlocation)
- [Model: CommunityVideo](#model-communityvideo)
- [Model: Config](#model-config)
- [Model: PermissionExclude](#model-permissionexclude)
- [Model: Report](#model-report)
- [Model: Logs](#model-logs)
- [Model: Apex and Other Games](#model-apex-and-other-games)
- [Model: ActivityEventLog](#model-activityeventlog)

## Imports
The file begins by importing necessary modules and classes:

```python
from django.db import models
from app.services.start_logger_when_server_starts import LOGGER_THREAD
from games.models import Lobby
from app.utils import UtilityMethods
from ryvals.core.models import TimeStampModel
from multiselectfield import MultiSelectField
from django.contrib.auth import get_user_model
from nimda.messages import CUSTOM_PERMISSION_GAME_MSG
from django.contrib.auth.models import Group, Permission
from cities_light.models import Country, Region, City
from django.utils.translation import ugettext_lazy as _
```

These imports include Django models, utilities, and translations, along with user models and external dependencies.

## Model: RestrictLocation
**Purpose:** Restrict locations, such as countries or regions, that could be banned for particular actions.

```python
class RestrictLocation(models.Model):
    _label = _('Banned location')
    _verbiage = _('Assist in banned location actions')
    ...
```
- **Fields:**
  - `country`: ForeignKey to `Country`, representing the country to be restricted.
  - `location`: ForeignKey to `Region`, representing the specific region.
  - `location_type`: Descriptive field for location type.

## Model: CommunityVideo
**Purpose:** Store details about community videos shared by players.

```python
class CommunityVideo(TimeStampModel):
    ''' Community Tab : stored youtube video link shared by players '''
    ...
```
- **Fields:**
  - `youtube_link`: URL of the YouTube video.
  - `lobby`: ForeignKey to `Lobby`, indicating the associated lobby.
  - `description`, `username`, `twitter`, `twitch`, `youtube`: Various fields to store additional details.
  - `pinned`: Boolean field indicating if the video is pinned.

## Model: Config
**Purpose:** Configuration settings for various features and limits in the application.

```python
class Config(models.Model):
    _label = _('Config')
    ...
```
- **Fields:** Include bonus amounts, thresholds, percentages, times, and other configuration parameters.

## Model: PermissionExclude
**Purpose:** Manage permissions that should be excluded for certain actions.

```python
class PermissionExclude(TimeStampModel):
    permission = models.ForeignKey(Permission, related_name='exclude_permissions', on_delete=models.CASCADE)
    ...
```
- **Fields:**
  - `permission`: ForeignKey to `Permission` model.

## Model: Report
**Purpose:** Handle report-related actions with specific permissions.

```python
class Report(models.Model):
    _label = _('Report')
    ...
```
- **Permissions:**
  - `view_report`: Allows viewing of reports.

## Model: Logs
**Purpose:** Log various events for activities and actions performed in the system.

```python
class Logs(TimeStampModel):
    _label = _('Logs')
    ...
```
- **Fields:**
  - `user`, `email`, `username`, `ip`: Details about the user and their session.
  - `action`: Integer field denoting the type of event.
  - `message`: Description of the event.
  - `vpn`, `extras`: Additional details.

- **Method: `add_entry`**: A static method to add log entries.

## Model: Apex and Other Games
**Purpose:** Manage permissions specific to different games like Apex, PUBG, Fortnite, etc.

```python
class Apex(models.Model):
    _label = _('Apex')
    ...
```
- **Permissions**: Each game model includes permissions related to their specific actions.

## Model: ActivityEventLog
**Purpose:** Filters activity log choices based on event types.

```python
class ActivityEventLog(TimeStampModel):
    ''' model for filter the activity log choices with the type '''
    ...
```
- **Fields:**
  - `events`: Uses `MultiSelectField` to store multiple event choices.
  - `type`: Denotes the type of event (Admin, Player, Other).

---

This documentation provides a comprehensive overview of the `models.py` file, detailing its purpose, structure, and the functionality of each model. The file plays a crucial role in maintaining the integrity and functionality of the application by defining how data is structured and interacted with in the database.