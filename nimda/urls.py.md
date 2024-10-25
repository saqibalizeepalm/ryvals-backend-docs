# Documentation for `urls.py`

This documentation provides an overview of the URL configurations for the Django project related to the admin API version 1. This file sets up the URL endpoints and associates them with the respective views in the application. The URLs are essential for directing the incoming HTTP requests to the correct views which handle the business logic.

## Index

- [Introduction](#introduction)
- [URL Patterns](#url-patterns)
- [Endpoints Overview](#endpoints-overview)
- [Conclusion](#conclusion)

## Introduction

The `urls.py` file is a crucial part of Django applications. It serves as the routing table that maps URLs to views. This setup allows for a clean separation between the URL structure and the underlying view logic.

## URL Patterns

The URL patterns are defined using Django's `path` and `re_path` functions. These functions associate specific URL patterns with the corresponding view classes.

### Imported Modules

```python
from django.urls import path, re_path
from rest_framework.generics import RetrieveUpdateDestroyAPIView
from accounts.api.views import ResetPassword, ForgotPasswordActivation
from nimda.api.views.auth_views import (
    SignIn, SignOut, ChangePasswordView, ForgotPassword, 
    ListAllActivityLogs, ListAllActivityEvent
)
from nimda.api.views.game_views import (
    ListChallengesAPIView, GameRetrieveDestroyAdminAPIView, 
    ListComplaintAPIView, ListCreateGameAdminAPIView, 
    ListCreateLobbyAdminAPIView, ListCreateGameDemoAdminAPIView, 
    ListPinnedGameDemoAdminAPIView, ListCreateRulesAdminAPIView, 
    RetrieveComplaintAPIView, RetrieveUpdateDestroyLobbyAdminAPIView, 
    RetrieveUpdateDestroyGameDemoAdminAPIView, 
    UpdateLobbyActivationStatusAdminAPIView, GameUpdateAdminAPIView, 
    UpdatedLobbyStatsFileCountAPIView, EnrolledPlayerStatsUpdateAPIView, 
    TransactionsReportAdminAPIView, FetchLobbyStatsAdminAPIView, 
    CancelLobbyAdminAPIView, RemovePlayerFromLobbyAdminAPIView, 
    RemoveTeamFromLobbyAdminAPIView, ChallengeRetrieveUpdateDestroyAdminAPIView
)
from nimda.api.views.frontend_views import (
    ListCreateFAQAdminAPIView, ListCreateFAQTopicAdminAPIView, 
    ListCreateSliderImageAPIView, ListCreateStaticPageAdminAPIView, 
    RetrieveUpdateConfigDetails, RetrieveUpdateDestroyFAQAdminAPIView, 
    RetrieveUpdateDestroySliderImageAPIView, RetrieveUpdateStaticPageAdminAPIView, 
    BannedLocationsAPIView, RemoveBannedLocationAPIView, 
    ListCreateCommunityAPIView, RetrieveUpdateDestroyCommunityAPIView, 
    AllEndedLobbyListAPIView, AllUserNameListAPIView, 
    RetrieveUpdateDestroyFAQTopicAdminAPIView, ReportLobbyListAPIView
)
from nimda.api.views.user_views import (
    ListCreateAdminStaffAPIView, ListTransactionHistoryAPIView, 
    SeizeMoneyAPIView, UpdateAdminStaffActivationStatusAPIView, 
    UpdateUserActivationStatusAdminAPIView, UserListAdminAPIView, 
    UserRetrieveAdminAPIView, TransactionStatusUpdateAPIView, 
    RefereeListAPIView, RefereeDetailAPIView, UserAffiliateDaysAPIView, 
    ListAdminStaffPermissionAPIView, EditAdminStaffAPIView, 
    CreateAdminStaffGroupsAPIView, RetrieveUpdateDestroyAdminStaffPermissionAPIView, 
    PermissionViewSet, ListCreateAdminStaffMemberAPIView, 
    ListUsersReportAPIView, ListComplaintsReportAPIView, 
    ExportReportCSVAPIView, UserReferralCodeAPIView, UserFreelobbyLimitAPIView
)
```

### URL Patterns List

Each path corresponds to a specific view, and thus a specific functionality in the application. Below is a breakdown of the major URL patterns defined in the file:

```python
urlpatterns = [
    path('login/', SignIn.as_view(), name='admin_login'),
    path('logout/', SignOut.as_view(), name="admin_logout"),
    path('change-password/', ChangePasswordView.as_view(),name='admin_change_password'),
    path('forgot-password/', ForgotPassword.as_view(), name='admin_forgot_password'),
    path('forgot-password-activation/', ForgotPasswordActivation.as_view(), name='forgot_password_activation'),
    path('reset-password/', ResetPassword.as_view(), name='reset_password'),
    path('users/', UserListAdminAPIView.as_view(), name='list_user'),
    re_path(r'users/(?P<pk>[\d]+)/$', UserRetrieveAdminAPIView.as_view(), name='retrieve_user'),
    re_path(r'users/(?P<pk>[\d]+)/change-activation/', UpdateUserActivationStatusAdminAPIView.as_view(), name='update_user_activation'),
    re_path(r'users/(?P<pk>[\d]+)/transaction-history', ListTransactionHistoryAPIView.as_view(), name='list_transaction_history'),
    re_path(r'users/(?P<pk>[\d]+)/transaction-status', TransactionStatusUpdateAPIView.as_view(), name='transaction_payment_status_update'),
    path('rules/', ListCreateRulesAdminAPIView.as_view(), name='list_create_rule'),
    path('games/', ListCreateGameAdminAPIView.as_view(), name='list_create_game'),
    path('game-update/<int:id>/', GameUpdateAdminAPIView.as_view(), name='update_game_view'),
    path('users/affiliate-days/<int:id>/', UserAffiliateDaysAPIView.as_view(), name='update_user_affiliate_day'),
    path('users/referral-code/<int:id>/', UserReferralCodeAPIView.as_view(), name='update_user_affiliate_day'),
    path('users/free-lobby-limit/<int:id>/', UserFreelobbyLimitAPIView.as_view(), name='update_user_affiliate_day'),
    path('games/<slug:slug>/', GameRetrieveDestroyAdminAPIView.as_view(), name='retrieve_destroy_game'),
    path('lobby/', ListCreateLobbyAdminAPIView.as_view(), name='list_create_lobby'),
    path('game-demo/', ListCreateGameDemoAdminAPIView.as_view(), name='list_create_game_demo'),
    path('pinned-game-demo/', ListPinnedGameDemoAdminAPIView.as_view(), name='list_create_game_demo'),
    path('lobby/<int:pk>/', RetrieveUpdateDestroyLobbyAdminAPIView.as_view(), name='retrieve_update_destroy_lobby'),
    path('fetch-lobby-stats/', FetchLobbyStatsAdminAPIView.as_view(), name='fetch_lobby_stats'),
    path('cancel-lobby/', CancelLobbyAdminAPIView.as_view(), name='cancel_lobby'),
    path('remove-player-from-lobby/', RemovePlayerFromLobbyAdminAPIView.as_view(), name='remove_player_from_lobby'),
    path('remove-team-from-lobby/', RemoveTeamFromLobbyAdminAPIView.as_view(), name='remove_team_from_lobby'),
    path('game-demo/<int:pk>/', RetrieveUpdateDestroyGameDemoAdminAPIView.as_view(), name='retrieve_update_destroy_game_demo'),
    path('lobby-stats-update/<int:pk>/', EnrolledPlayerStatsUpdateAPIView.as_view(), name='enroll_player_stats_update'),
    path('lobby-files/<int:pk>/', UpdatedLobbyStatsFileCountAPIView.as_view(), name='update_lobby_stats_files'),
    re_path(r'lobby/(?P<pk>[\d]+)/change-activation/', UpdateLobbyActivationStatusAdminAPIView.as_view(), name='update_lobby_activation'),
    path('complaint/', ListComplaintAPIView.as_view(), name='list_complaint'),
    path('complaint/<int:pk>/', RetrieveComplaintAPIView.as_view(), name='retrieve_complaint'),
    path('staff/', ListCreateAdminStaffAPIView.as_view(), name='list_create_staff'),
    path('staff-members/', ListCreateAdminStaffMemberAPIView.as_view(), name='list_staff_member'),
    re_path(r'staff/(?P<pk>[\d]+)/$', EditAdminStaffAPIView.as_view(), name='retrieve_staff'),
    re_path(r'staff/(?P<pk>[\d]+)/update-status/', UpdateAdminStaffActivationStatusAPIView.as_view(), name='update_staff_activation'),
    path('pages/', ListCreateStaticPageAdminAPIView.as_view(), name='list_create_static_page'),
    path('pages/<slug:slug>/', RetrieveUpdateStaticPageAdminAPIView.as_view(), name='retrieve_update_static_page'),
    path('sliderimage/', ListCreateSliderImageAPIView.as_view(), name='list_create_slider_image'),
    path('sliderimage/<int:pk>/', RetrieveUpdateDestroySliderImageAPIView.as_view(), name='retrieve_update_destroy_slider_image'),
    path('faq/', ListCreateFAQAdminAPIView.as_view(), name='list_create_faq'),
    path('faq/<int:pk>/', RetrieveUpdateDestroyFAQAdminAPIView.as_view(), name='retrieve_update_destroy_faq'),
    path('faq/topics/', ListCreateFAQTopicAdminAPIView.as_view(), name='list_create_faq_topic'),
    path('faq/topics/<slug:slug>/', RetrieveUpdateDestroyFAQTopicAdminAPIView.as_view(), name='retrieve_update_destroy_faq_topic'),
    path('seize-money/<int:pk>/', SeizeMoneyAPIView.as_view(), name='seize_amount'),
    path('banned-locations/', BannedLocationsAPIView.as_view(), name='banned_locations'),
    path('banned-locations/<int:pk>/', RemoveBannedLocationAPIView.as_view(), name='remove_banned_location'),
    path('community/', ListCreateCommunityAPIView.as_view(), name='list_create_community_view'),
    path('community/<int:pk>/', RetrieveUpdateDestroyCommunityAPIView.as_view(), name='retrieve_update_destroy_view'),
    path('report/lobby/', ReportLobbyListAPIView.as_view(), name='report_lobbies_view'),
    path('reports/transactions/', TransactionsReportAdminAPIView.as_view(), name='transactions_report'),
    path('all-lobbies/', AllEndedLobbyListAPIView.as_view(), name='all-lobbies'),
    path('all-username/', AllUserNameListAPIView.as_view(), name='all-usernames'),
    path('referees/', RefereeListAPIView.as_view(), name='list_referee_view'),
    path('referees/<int:pk>/', RefereeDetailAPIView.as_view(), name='detail_referee_view'),
    path('config/', RetrieveUpdateConfigDetails.as_view(), name="update_config_detail"),
    path('staff-permissions/', ListAdminStaffPermissionAPIView.as_view(), name='list_staff_permission'),
    path('groups/', CreateAdminStaffGroupsAPIView.as_view(), name='create_staff_groups'),
    path('groups/<int:pk>/', RetrieveUpdateDestroyAdminStaffPermissionAPIView.as_view(), name='retrieve_update_staff_permissions'),
    path('permissions/', PermissionViewSet.as_view({'get':'list'}), name='view_all_permissions'),
    path('report/users/', ListUsersReportAPIView.as_view(), name='list_user_report'),
    path('report/complaints/', ListComplaintsReportAPIView.as_view(), name='list_complaints_report'),
    path('report/export-csv/', ExportReportCSVAPIView.as_view(), name='export_report_csv'),
    path('logs/', ListAllActivityLogs.as_view(), name='list_all_user_logs'),
    path('events/', ListAllActivityEvent.as_view(), name='list_all_activity_event'),
    path('challenges/', ListChallengesAPIView.as_view(), name='list_all_challenges'),
    path('challenges/<int:pk>/', ChallengeRetrieveUpdateDestroyAdminAPIView.as_view(), name='challenge_update_destroy'),
]
```

## Endpoints Overview

Below is a brief description of some of the key endpoints defined in this URL configuration:

- **Authentication Endpoints:**
  - `/login/`: Handles admin login.
  - `/logout/`: Handles admin logout.
  - `/change-password/`: Allows an admin to change their password.
  - `/forgot-password/`: Initiates the forgotten password process.
  - `/forgot-password-activation/`: Activates the forgotten password process.
  - `/reset-password/`: Resets the password for a user.

- **User Management:**
  - `/users/`: Lists all users.
  - `/users/<pk>/`: Retrieve a specific user.
  - `/users/<pk>/change-activation/`: Change the activation status of a user.
  - `/users/<pk>/transaction-history`: View the transaction history of a user.

- **Game and Lobby Management:**
  - `/games/`: List and create games.
  - `/lobby/`: List and create lobbies.
  - `/game-demo/`: List and create game demos.
  - `/pinned-game-demo/`: List pinned game demos.

- **Community and Content:**
  - `/community/`: List and create community content.
  - `/pages/`: List and create static pages.

- **Reports and Logs:**
  - `/report/lobby/`: Get lobby reports.
  - `/reports/transactions/`: Get transaction reports.
  - `/logs/`: View all user activity logs.
  - `/events/`: List all activity events.

## Conclusion

This `urls.py` file serves as a comprehensive map of the API endpoints available for the admin version 1. It provides a structured approach to managing different aspects of the application, from user authentication and management to content and report generation. This setup facilitates ease of navigation and scalability for further development.