# Frontend Views Documentation

This document provides a comprehensive overview of the `frontend_views.py` file, which forms part of the backend for managing static pages, slider images, FAQs, banned locations, community videos, and lobby reports for Ryvals Admins. This file primarily utilizes Django's class-based views to handle various CRUD operations and implements custom permissions. Below is a detailed explanation of the views and their functionalities.

## Table of Contents
1. [Introduction](#introduction)
2. [Views](#views)
   - [ListCreateStaticPageAdminAPIView](#listcreatestaticpageadminapiview)
   - [RetrieveUpdateStaticPageAdminAPIView](#retrieveupdatestaticpageadminapiview)
   - [ListCreateSliderImageAPIView](#listcreatesliderimageapiview)
   - [RetrieveUpdateDestroySliderImageAPIView](#retrieveupdatedestroysliderimageapiview)
   - [ListCreateFAQAdminAPIView](#listcreatefaqadminapiview)
   - [RetrieveUpdateDestroyFAQAdminAPIView](#retrieveupdatedestroyfaqadminapiview)
   - [ListCreateFAQTopicAdminAPIView](#listcreatefaqtopicadminapiview)
   - [RetrieveUpdateDestroyFAQTopicAdminAPIView](#retrieveupdatedestroyfaqtopicadminapiview)
   - [BannedLocationsAPIView](#bannedlocationsapiview)
   - [RemoveBannedLocationAPIView](#removebannedlocationapiview)
   - [ListCreateCommunityAPIView](#listcreatecommunityapiview)
   - [RetrieveUpdateDestroyCommunityAPIView](#retrieveupdatedestroycommunityapiview)
   - [AllEndedLobbyListAPIView](#allendedlobbylistapiview)
   - [AllUserNameListAPIView](#allusernamelistapiview)
   - [RetrieveUpdateConfigDetails](#retrieveupdateconfigdetails)
   - [ReportLobbyListAPIView](#reportlobbylistapiview)

---

## Introduction

The `frontend_views.py` file is part of the Ryvals application, designed to handle various frontend-related operations for Ryvals Admins. It focuses on managing static content, viewing reports, and handling CRUD operations for community content. It leverages Django REST Framework's class-based views for structured and reusable code.

---

## Views

### ListCreateStaticPageAdminAPIView
**Purpose**: Allows Ryvals Super Admins to create static pages and all Ryvals Admins to view a list of static pages.

- **Methods**: `GET`, `POST`
- **Permissions**: Requires admin-level permissions.
- **Pagination**: Uses infinite scroll pagination for listing static pages.

### RetrieveUpdateStaticPageAdminAPIView
**Purpose**: Enables Ryvals Super Admins to edit static pages and all Ryvals Admins to view static page details.

- **Methods**: `GET`, `PUT`
- **Permissions**: Requires admin-level permissions.
- **Details**: Retrieves or updates a static page based on a unique slug.

### ListCreateSliderImageAPIView
**Purpose**: Allows admin users to save and list images for image sliders.

- **Methods**: `GET`, `POST`
- **Permissions**: Admin-level access required.

### RetrieveUpdateDestroySliderImageAPIView
**Purpose**: Provides detailed view, update, and delete functionalities for individual slider images.

- **Methods**: `GET`, `PUT`, `DELETE`
- **Permissions**: Admin-level access required.
- **Error Handling**: Returns errors if the image is not found or deletion fails.

### ListCreateFAQAdminAPIView
**Purpose**: Allows Ryvals Admins to list and create FAQs.

- **Methods**: `GET`, `POST`
- **Permissions**: Admin-level access with specific model permissions.

### RetrieveUpdateDestroyFAQAdminAPIView
**Purpose**: Admin view to handle FAQ details, updates, and deletions.

- **Methods**: `GET`, `PUT`, `DELETE`
- **Permissions**: Requires specific model permissions.
- **Error Handling**: Handles errors if the FAQ does not exist.

### ListCreateFAQTopicAdminAPIView
**Purpose**: Enables viewing and creating FAQ topics.

- **Methods**: `GET`, `POST`
- **Permissions**: Admin-level access required.

### RetrieveUpdateDestroyFAQTopicAdminAPIView
**Purpose**: Provides functionality to view details, update, and delete FAQ topics.

- **Methods**: `PUT`, `DELETE`
- **Permissions**: Admin-level access required.

### BannedLocationsAPIView
**Purpose**: Admin API to view and create banned locations.

- **Methods**: `GET`, `POST`
- **Permissions**: Admin-level access required.

### RemoveBannedLocationAPIView
**Purpose**: Allows admins to remove banned locations.

- **Methods**: `DELETE`, `PUT`
- **Permissions**: Admin-level access required.

### ListCreateCommunityAPIView
**Purpose**: Admin view for listing and creating community videos.

- **Methods**: `GET`, `POST`
- **Permissions**: Admin-level access required.
- **Pagination**: Standard pagination for listing community videos.

### RetrieveUpdateDestroyCommunityAPIView
**Purpose**: Provides detailed view, update, and delete functionalities for community videos.

- **Methods**: `GET`, `PUT`, `DELETE`
- **Permissions**: Admin-level access required.

### AllEndedLobbyListAPIView
**Purpose**: Lists all ended lobbies for admin review.

- **Methods**: `GET`
- **Permissions**: Admin-level access required.

### AllUserNameListAPIView
**Purpose**: List all usernames for community interaction.

- **Methods**: `GET`
- **Permissions**: Access for both players and admins.
- **Pagination**: Optional pagination with sorting by friendship status.

### RetrieveUpdateConfigDetails
**Purpose**: Retrieve or update configuration details.

- **Methods**: `GET`, `PUT`
- **Permissions**: No permission required for `GET`.

### ReportLobbyListAPIView
**Purpose**: Admin view to report lobby details.

- **Methods**: `GET`
- **Permissions**: Admin-level access with specific permissions.
- **Filtering**: Allows filtering by date range and lobby type.

This documentation provides an overview of each view's purpose, methods, permissions, and any additional relevant details. For detailed usage, consult the code comments and method definitions directly within the `frontend_views.py` file.