# Documentation for `frontend_serializers.py`

This document provides an overview and detailed explanation of the `frontend_serializers.py` file. This file primarily contains Django REST Framework serializers, which are used for converting complex data types like Django QuerySets into Python data types that can be easily rendered into JSON, XML, or other content types. These serializers also handle validation of input data when it is being deserialized.

## Table of Contents
1. [Dependencies](#dependencies)
2. [Serializer Classes](#serializer-classes)
   - [AddStaticPageSerializer](#addstaticpageserializer)
   - [EditStaticPageSerializer](#editstaticpageserializer)
   - [AddImageSerializer](#addimageserializer)
   - [UpdateImageSerializer](#updateimageserializer)
   - [AddQuestionSerializer](#addquestionserializer)
   - [EditQuestionSerializer](#editquestionserializer)
   - [QuestionListSerializer](#questionlistserializer)
   - [ListFAQSerializer](#listfaqserializer)
   - [DetailFAQSerializer](#detailfaqserializer)
   - [AddFAQTopicSerializer](#addfaqtopicserializer)
   - [EditFAQTopicSerializer](#editfaqtopicserializer)
   - [RegionListSerializer](#regionlistserializer)
   - [ListBannedLocationSerializer](#listbannedlocationserializer)
   - [BannedLocationSerializer](#bannedlocationserializer)
   - [ListCommunitySerializer](#listcommunityserializer)
   - [AddCommunitySerializer](#addcommunityserializer)
   - [UpdateCommunitySerializer](#updatecommunityserializer)
   - [AllLobbyListSerializer](#alllobbylistserializer)
   - [AllUserNameListSerializer](#allusernamelistserializer)
   - [ConfigDetailSerializer](#configdetailserializer)
   - [UpdateConfigSerializer](#updateconfigserializer)
   - [ReportLobbyListSerializer](#reportlobbylistserializer)
   - [ListTournamentSerializer](#listtournamentserializer)
   - [AddTournamentSerializer](#addtournamentserializer)
   - [TournamentSubMatchSerializer](#tournamentsubmatchserializer)
   - [TournamentMatchSerializer](#tournamentmatchserializer)
   - [TournamentRoundPageSerilizer](#tournamentroundpageserilizer)
   - [CreateTournamentLobbyMatchSerilizer](#createtournamentlobbymatchserilizer)

## Dependencies

Before delving into the serializers, let's take a look at the dependencies used in this file:

```python
import logging
import pytz
import random
import secrets
from datetime import datetime, timedelta
from django.db import transaction
from django.utils import timezone
from django.db.models import Max, Min
from django.contrib.auth import get_user_model
from rest_framework import serializers
from rest_framework.exceptions import APIException
from django.db.models.query_utils import Q
from cities_light.models import Country, Region, City
from django.utils.translation import gettext_lazy as _
from nimda.models import Config, RestrictLocation, CommunityVideo, Logs
from games.models import ImageSlider, Lobby, Game
from pages.models import Question, StaticPage, Topic
from players.models import PlayerLobby, Tournament, Price, TournamentRound, TournamentMatch, TournamentSubMatch
from players.services.tournament_service import TournamentService
from ryvals.core.discord import create_private_channel, create_channel_webhook
from ryvals.core.messages import FIELD_REQUIRED, BLANK_NOT_ALLOWED
from players.api.serializers.versus_serializers import TIME_STRING_FORMAT_CONST
from friendship.models import Friend, FriendshipRequest
from nimda.messages import (
    FAQ_CREATE_ERROR, INVALID_HTML, INVALID_SORT_ORDER,
    STATIC_PAGE_CREATION_ERROR, STATIC_PAGE_EDIT_ERROR,
    TOPIC_CREATION_ERROR, TOPIC_ALREADY_EXISTS,
    ALREADY_BANNED, ALREADY_BANNED_ERROR,
    ALL_BANNED_STATES, VIDEO_ADD_ERROR,
    ORDERING_ERROR, TOPIC_NAME_TOO_LONG,
    TOUR_LOBBY_START_DATE_ERROR, TOUR_LAST_ENTRY_TIME_ERROR,
    DUPLICATE_LOBBY_ERROR, UNEXPECTED_LOBBY_ERROR,
    TOPIC_NAME_VALIDATION, INVALID_QUESTION_FORMAT
)
from app.utils import UtilityMethods
from nimda.api.serializers.user_serializers import US_EAST_TIMEZONE_CONST
from nimda.api.serializers.game_serializers import AddLobbySerializer

User = get_user_model()
logger = logging.getLogger('django')
secrets_generator = secrets.SystemRandom()
```

## Serializer Classes

### AddStaticPageSerializer

```python
class AddStaticPageSerializer(serializers.Serializer):
    ''' Add Static Page Serializer '''
    title = serializers.CharField(max_length=20, required=True, error_messages={'required': FIELD_REQUIRED % {'field': _('Title')}, 'blank': BLANK_NOT_ALLOWED % {'field': _('Title')}})
    content = serializers.CharField(required=True, error_messages={'required': FIELD_REQUIRED % {'field': _('Title')}, 'blank': BLANK_NOT_ALLOWED % {'field': _('Title')}})
```
- **Purpose**: Used for creating a new static page with a title and content.

### EditStaticPageSerializer

```python
class EditStaticPageSerializer(serializers.Serializer):
    ''' Edit Static Page Serializer '''
    title = serializers.CharField(max_length=20, required=True, error_messages={'required': FIELD_REQUIRED % {'field': _('Title')}, 'blank': BLANK_NOT_ALLOWED % {'field': _('Title')}})
    content = serializers.CharField(required=True, error_messages={'required': FIELD_REQUIRED % {'field': _('Title')}, 'blank': BLANK_NOT_ALLOWED % {'field': _('Title')}})
```
- **Purpose**: Used for editing an existing static page.

### AddImageSerializer

```python
class AddImageSerializer(serializers.Serializer):
    ''' Serializer to add the image to image slider '''
    image = serializers.CharField(required=True, error_messages={'required': FIELD_REQUIRED % {'field': _('Image')}})
    description = serializers.CharField(required=True, error_messages={'required': FIELD_REQUIRED % {'field': _('Description')}})
    link = serializers.URLField(required=True, error_messages={'required': FIELD_REQUIRED % {'field': _('Link')}})
```
- **Purpose**: Used for adding an image to an image slider with a description and link.

### UpdateImageSerializer

```python
class UpdateImageSerializer(serializers.Serializer):
    ''' Serializer to update the image in image slider '''
    image = serializers.CharField(required=False)
    description = serializers.CharField(required=False)
    link = serializers.URLField(required=False)
```
- **Purpose**: Used for updating an existing image in the image slider.

### AddQuestionSerializer

```python
class AddQuestionSerializer(serializers.Serializer):
    ''' Add Question Serializer '''
    question = serializers.CharField(required=True, error_messages={'required': FIELD_REQUIRED % {'field': 'Question'}, 'blank': BLANK_NOT_ALLOWED % {'field': 'Question'}})
    answer = serializers.CharField(required=True, error_messages={'required': FIELD_REQUIRED % {'field': 'Answer'}, 'blank': BLANK_NOT_ALLOWED % {'field': 'Answer'}})
    topic_id = serializers.IntegerField(required=True, error_messages={'required': FIELD_REQUIRED % {'field': 'Topic'}, 'blank': BLANK_NOT_ALLOWED % {'field': 'Topic'}})
```
- **Purpose**: Used for adding a new question to a specific topic.

### EditQuestionSerializer

```python
class EditQuestionSerializer(serializers.Serializer):
    ''' Edit FAQ Serializer '''
    question = serializers.CharField(required=False)
    answer = serializers.CharField(required=False)
    sort_order = serializers.IntegerField(required=False)
    status = serializers.IntegerField(required=False)
    topic_id = serializers.IntegerField(required=False)
```
- **Purpose**: Used for editing an existing FAQ question.

### QuestionListSerializer

```python
class QuestionListSerializer(serializers.ModelSerializer):
    class Meta:
        model = Question
        fields = ['id', 'question', 'answer', 'topic', 'status', 'sort_order']
```
- **Purpose**: Lists questions with their details.

### ListFAQSerializer

```python
class ListFAQSerializer(serializers.ModelSerializer):
    ''' List FAQ Serializer '''
    category = serializers.SerializerMethodField('get_question')

    def get_question(self, obj):
        response = {'name': obj.name, 'slug': obj.slug, 'questions': None}
        questions = Question.objects.filter(topic=obj, status=Question.Status.ACTIVE).order_by('sort_order')
        if questions:
            question_list = QuestionListSerializer(questions, many=True).data
            response['questions'] = question_list
        return response
```
- **Purpose**: Lists FAQ categories and their associated questions.

### DetailFAQSerializer

```python
class DetailFAQSerializer(serializers.ModelSerializer):
    ''' Detail FAQ Serializer '''
    class Meta:
        model = Question
        fields = ['id', 'question', 'topic', 'answer', 'sort_order', 'status']
```
- **Purpose**: Provides detailed information about a specific FAQ question.

### AddFAQTopicSerializer

```python
class AddFAQTopicSerializer(serializers.Serializer):
    ''' Add FAQ Topic Serializer TODO: merge functionality with add Question '''
    name = serializers.CharField(required=True, error_messages={'required': FIELD_REQUIRED % {'field': 'Name'}, 'blank': BLANK_NOT_ALLOWED % {'field': 'Name'}})
    sort_order = serializers.IntegerField(required=False)
    type = serializers.IntegerField(required=True)
```
- **Purpose**: Used for adding a new FAQ topic.

### EditFAQTopicSerializer

```python
class EditFAQTopicSerializer(serializers.Serializer):
    ''' Edit FAQ Topic Serializer TODO: merge functionality with edit Question '''
    name = serializers.CharField(required=False)
    sort_order = serializers.IntegerField(required=False)
    type = serializers.IntegerField(required=False)
```
- **Purpose**: Used for editing an existing FAQ topic.

### RegionListSerializer

```python
class RegionListSerializer(serializers.ModelSerializer):
    state_id = serializers.SerializerMethodField('get_state_id')
    state_name = serializers.SerializerMethodField('get_state_name')

    class Meta:
        model = RestrictLocation
        fields = ['state_id', 'state_name']

    def get_state_id(self, obj):
        return obj.location.id

    def get_state_name(self, obj):
        return obj.location.name
```
- **Purpose**: Lists states with their IDs and names for a given location.

### ListBannedLocationSerializer

```python
class ListBannedLocationSerializer(serializers.ModelSerializer):
    ''' List banned locations Serializer '''
    country_name = serializers.SerializerMethodField('get_country_name')
    all_states = serializers.SerializerMethodField('get_all_states')

    class Meta:
        model = RestrictLocation
        fields = ['id', 'country_id', 'country_name', 'all_states']

    def get_country_name(self, obj):
        return obj.country.name

    def get_all_states(self, obj):
        return RestrictLocation.objects.filter(country=obj.country)
```
- **Purpose**: Lists banned locations, including countries and all their states.

### BannedLocationSerializer

```python
class BannedLocationSerializer(serializers.Serializer):
    ''' List Banned Locations Serializer '''
    location_id = serializers.ListField(required=True)
    location_type = serializers.CharField(required=True)
```
- **Purpose**: Used for listing banned locations based on IDs and types.

### ListCommunitySerializer

```python
class ListCommunitySerializer(serializers.ModelSerializer):
    lobby_name = serializers.CharField(source='lobby.name', default=None)

    class Meta:
        model = CommunityVideo
        fields = '__all__'
```
- **Purpose**: Lists community videos along with their lobby names.

### AddCommunitySerializer

```python
class AddCommunitySerializer(serializers.Serializer):
    ''' Add Community Video Serializer '''
    youtube_link = serializers.URLField(required=True, error_messages={'required': FIELD_REQUIRED % {'field': 'Link'}, 'blank': BLANK_NOT_ALLOWED % {'field': 'Link'}})
    description = serializers.CharField(required=True, error_messages={'required': FIELD_REQUIRED % {'field': 'Description'}, 'blank': BLANK_NOT_ALLOWED % {'field': 'Description'}})
    lobby_id = serializers.IntegerField(required=True, error_messages={'required': FIELD_REQUIRED % {'field': _('Lobby id')}})
    username = serializers.CharField(required=True, error_messages={'required': FIELD_REQUIRED % {'field': 'Username'}, 'blank': BLANK_NOT_ALLOWED % {'field': 'Username'}})
    twitter = serializers.CharField(required=False, allow_blank=True)
    twitch = serializers.CharField(required=False, allow_blank=True)
    youtube = serializers.CharField(required=False, allow_blank=True)
    pinned = serializers.BooleanField(required=True, error_messages={'required': FIELD_REQUIRED % {'field': _('Pinned')}})
```
- **Purpose**: Adds a new community video with details including links and social media.

### UpdateCommunitySerializer

```python
class UpdateCommunitySerializer(serializers.Serializer):
    youtube_link = serializers.URLField(required=True, error_messages={'required': FIELD_REQUIRED % {'field': 'Link'}, 'blank': BLANK_NOT_ALLOWED % {'field': 'Link'}})
    description = serializers.CharField(required=True, error_messages={'required': FIELD_REQUIRED % {'field': 'Description'}, 'blank': BLANK_NOT_ALLOWED % {'field': 'Description'}})
    lobby_id = serializers.IntegerField(required=True, error_messages={'required': FIELD_REQUIRED % {'field': _('Lobby id')}})
    username = serializers.CharField(required=True, error_messages={'required': FIELD_REQUIRED % {'field': 'Username'}, 'blank': BLANK_NOT_ALLOWED % {'field': 'Username'}})
    twitter = serializers.CharField(required=False, allow_blank=True)
    twitch = serializers.CharField(required=False, allow_blank=True)
    youtube = serializers.CharField(required=False, allow_blank=True)
    pinned = serializers.BooleanField(required=True, error_messages={'required': FIELD_REQUIRED % {'field': _('Pinned')}})
```
- **Purpose**: Updates an existing community video with new details or links.

### AllLobbyListSerializer

```python
class AllLobbyListSerializer(serializers.ModelSerializer):
    ''' Serializer for listing all ended Lobbies '''
    class Meta:
        model = Lobby
        fields = ['id', 'name']
```
- **Purpose**: Lists all lobbies that have ended.

### AllUserNameListSerializer

```python
class AllUserNameListSerializer(serializers.ModelSerializer):
    ''' Serializer for listing all usernames for community '''
    def __init__(self, *args, **kwargs):
        super(AllUserNameListSerializer, self).__init__(*args, **kwargs)
        context = kwargs.get('context', None)
        if context:
            self.request = kwargs['context']['request']
    friend = serializers.SerializerMethodField()
    request = serializers.SerializerMethodField()
    disable_add_friend = serializers.SerializerMethodField()
```
- **Purpose**: Lists all usernames and their friendship status for the community.

### ConfigDetailSerializer

```python
class ConfigDetailSerializer(serializers.ModelSerializer):
    ''' Serializer for listing all details of config table. '''
    button_grey_out_time = serializers.SerializerMethodField()

    def get_button_grey_out_time(self, obj):
        total_time = obj.team_member_mod_time + obj.team_owner_mod_time + obj.team_lobby_buffer_time
        return total_time

    class Meta:
        model = Config
        fields = '__all__'
```
- **Purpose**: Provides details of the config table, including calculated fields.

### UpdateConfigSerializer

```python
class UpdateConfigSerializer(serializers.Serializer):
    ''' Update Config Serializer TODO: Add Buffer Time '''
    team_owner_mod_time = serializers.IntegerField(required=False)
    team_member_mod_time = serializers.IntegerField(required=False)
    ref_bonus_amount = serializers.IntegerField(required=False)
    ref_threshold_amount = serializers.IntegerField(required=False)
    ref_threshold_expire = serializers.IntegerField(required=False)
    referee_percentage = serializers.IntegerField(required=False)
    affiliate_days = serializers.IntegerField(required=False)
    favourite_friend = serializers.IntegerField(required=False)
    max_pinned_demo_count = serializers.IntegerField(required=False)
    inactivity_charges = serializers.IntegerField(required=False)
    inactivity_timeline = serializers.IntegerField(required=False)
    inactivity_reminder = serializers.IntegerField(required=False)
    free_lobby_limit = serializers.IntegerField(required=False)
```
- **Purpose**: Updates config settings with various parameters.

### ReportLobbyListSerializer

```python
class ReportLobbyListSerializer(serializers.ModelSerializer):
    ''' Serializer for get the lobbies details for report. '''
    name_of_the_game = serializers.SerializerMethodField('get_name_of_the_game')
    total_enrollment_money = serializers.SerializerMethodField('get_total_enrollment_money')
    winning_amount = serializers.SerializerMethodField('get_winning_amount')
    total_kills = serializers.SerializerMethodField('get_total_kills')
    create_date = serializers.SerializerMethodField('get_create_date')
    lobby_start_date = serializers.SerializerMethodField('get_lobby_start_date')
    entry_fee = serializers.SerializerMethodField('get_entry_fee')
    registered_players = serializers.SerializerMethodField('get_registered_players')
```
- **Purpose**: Provides a detailed report of lobby statistics.

### ListTournamentSerializer

```python
class ListTournamentSerializer(serializers.ModelSerializer):
    ''' List of Tournaments '''
    def __init__(self, *args, **kwargs):
        super(ListTournamentSerializer, self).__init__(*args, **kwargs)
        context = kwargs.get('context', None)
        if context:
            self.request = kwargs['context']['request']
```
- **Purpose**: Lists tournaments with their details and statuses.

### AddTournamentSerializer

```python
class AddTournamentSerializer(serializers.Serializer):
    ''' Serilizer for Add Tournament '''
    name = serializers.CharField(required=True, error_messages={'required': FIELD_REQUIRED % {'field': _('Name')}})
    game_id = serializers.IntegerField(required=True, error_messages={'required': FIELD_REQUIRED % {'field': _('Game id')}})
    game_type = serializers.IntegerField(required=True, error_messages={'required': FIELD_REQUIRED % {'field': _('Game Type')}})
    entry_fee = serializers.IntegerField(required=True, error_messages={'required': FIELD_REQUIRED % {'field': _('Entry Fee')}})
```
- **Purpose**: Adds a new tournament with specified parameters.

### TournamentSubMatchSerializer

```python
class TournamentSubMatchSerializer(serializers.ModelSerializer):
    ''' List of all sub matches of the match in the Tournament '''
    def __init__(self, *args, **kwargs):
        super(TournamentSubMatchSerializer, self).__init__(*args, **kwargs)
        context = kwargs.get('context', None)
        if context:
            self.request = kwargs['context']['request']
```
- **Purpose**: Lists all sub-matches within a tournament match.

### TournamentMatchSerializer

```python
class TournamentMatchSerializer(serializers.ModelSerializer):
    ''' List of all tournament matches '''
    match = serializers.SerializerMethodField()
    sub_match = serializers.SerializerMethodField()
    round_datetime = serializers.SerializerMethodField()
```
- **Purpose**: Lists all tournament matches with their details.

### TournamentRoundPageSerilizer

```python
class TournamentRoundPageSerilizer(serializers.ModelSerializer):
    ''' Serializer for listing the tournament Rounds '''
    round = serializers.SerializerMethodField()
    total_matches = serializers.IntegerField(source='matches')
    matches = serializers.SerializerMethodField()
    bracket_cloud_id = serializers.SerializerMethodField()
```
- **Purpose**: Lists tournament rounds and their associated matches.

### CreateTournamentLobbyMatchSerilizer

```python
class CreateTournamentLobbyMatchSerilizer(serializers.Serializer):
    ''' Add Tournament matches and sub matches Serilizer '''
    data = serializers.ListField(required=True, error_messages={'required': FIELD_REQUIRED % {'field': _('Start date')}})
```
- **Purpose**: Adds tournament matches and their sub-matches.

This comprehensive documentation aims to provide a clear understanding of each serializer class and its purpose, ensuring easy maintenance and extension of the frontend serializers.