# Documentation for `user_views.py`

The `user_views.py` file is part of a Django application and is primarily responsible for handling user-related API views for the administration of a platform named Ryvals. It uses Django's REST framework to build a series of API endpoints that allow administrators to manage users and their data efficiently. Here, we'll explore the purpose and functionality of each class in the file, along with the associated serializers and permissions.

## Table of Contents

- [UserListAdminAPIView](#userlistadminapiview)
- [UserRetrieveAdminAPIView](#userretrieveadminapiview)
- [UpdateUserActivationStatusAdminAPIView](#updateuseractivationstatusadminapiview)
- [ListCreateAdminStaffAPIView](#listcreateadminstaffapiview)
- [ListCreateAdminStaffMemberAPIView](#listcreateadminstaffmemberapiview)
- [EditAdminStaffAPIView](#editadminstaffapiview)
- [UpdateAdminStaffActivationStatusAPIView](#updateadminstaffactivationstatusapiview)
- [SeizeMoneyAPIView](#seizemoneyapiview)
- [ListTransactionHistoryAPIView](#listtransactionhistoryapiview)
- [TransactionStatusUpdateAPIView](#transactionstatusupdateapiview)
- [RefereeListAPIView](#refereelistapiview)
- [RefereeDetailAPIView](#refereedetailapiview)
- [UserAffiliateDaysAPIView](#useraffiliatedaysapiview)
- [UserReferralCodeAPIView](#userreferralcodeapiview)
- [ListAdminStaffPermissionAPIView](#listadminstaffpermissionapiview)
- [CreateAdminStaffGroupsAPIView](#createadminstaffgroupsapiview)
- [RetrieveUpdateDestroyAdminStaffPermissionAPIView](#retrieveupdatedestroyadminstaffpermissionapiview)
- [PermissionViewSet](#permissionviewset)
- [ListUsersReportAPIView](#listusersreportapiview)
- [ListComplaintsReportAPIView](#listcomplaintsreportapiview)
- [ExportReportCSVAPIView](#exportreportcsvapiview)
- [UserFreelobbyLimitAPIView](#userfreelobbylimitapiview)

### UserListAdminAPIView

**Purpose**: 
This API view allows Ryvals Admins to list all users on the platform. It supports filtering and sorting of users based on various criteria such as name, username, phone, and email.

**Key Features**:
- Filters users based on a query string.
- Supports sorting by various fields.
- Logs each access of the user list.

**Code Example**:
```python
class UserListAdminAPIView(generics.ListAPIView):
    '''
    User Listing API View for Ryvals Admins
    '''
    serializer_class = UserListSerializer
    permission_classes = (PrivateTokenAccessPermission, IsAnyRyvalsAdmin, IsActivated, CustomDjangoModelPermissions)
    pagination_class = StandardPagination
```

### UserRetrieveAdminAPIView

**Purpose**: 
Fetches detailed information of a specific user based on their ID.

**Key Features**:
- Retrieves user data using user ID.
- Logs the access of user details.

### UpdateUserActivationStatusAdminAPIView

**Purpose**: 
Allows Ryvals Admins to activate or deactivate user accounts.

**Key Features**:
- Updates the activation status of a user.
- Handles exceptions if the user does not exist.

### ListCreateAdminStaffAPIView

**Purpose**: 
Facilitates the listing and creation of admin staff members.

**Key Features**:
- Lists all admin staff members.
- Allows for the addition of new admin staff.
- Supports filtering and sorting.

### ListCreateAdminStaffMemberAPIView

**Purpose**: 
Lists all staff members during the lobby creation process.

**Key Features**:
- Retrieves staff members with specific roles.

### EditAdminStaffAPIView

**Purpose**: 
Enables retrieval, updating, and removal of Ryvals staff member details.

**Key Features**:
- Supports retrieving, updating, and deleting staff members.
- Prevents deletion of super admins or owners.

### UpdateAdminStaffActivationStatusAPIView

**Purpose**: 
Allows Ryvals Super Admins to activate or deactivate admin staff accounts.

**Key Features**:
- Updates activation status and handles exceptions.

### SeizeMoneyAPIView

**Purpose**: 
Enables Ryvals Admins to seize wallet amounts from users.

**Key Features**:
- Seizes money from user accounts.
- Uses transaction management to ensure data integrity.

### ListTransactionHistoryAPIView

**Purpose**: 
Lists all transactions associated with a user.

**Key Features**:
- Retrieves transaction logs.
- Logs the access of transaction history.

### TransactionStatusUpdateAPIView

**Purpose**: 
Allows Ryvals Admins to update the status of user transactions.

**Key Features**:
- Updates transaction status to 'Release' or 'Seize'.
- Handles exceptions if the transaction is not found.

### RefereeListAPIView

**Purpose**: 
Lists referees who have invited friends via a referral.

**Key Features**:
- Supports filtering and sorting.
- Provides aggregated data on referral earnings.

### RefereeDetailAPIView

**Purpose**: 
Retrieves detailed information about a specific referee.

### UserAffiliateDaysAPIView

**Purpose**: 
Manages individual referral days for players.

**Key Features**:
- Updates affiliate days for users.

### UserReferralCodeAPIView

**Purpose**: 
Allows editing or updating user referral codes.

**Key Features**:
- Validates and updates referral codes.

### ListAdminStaffPermissionAPIView

**Purpose**: 
Lists permissions for admin staff.

**Key Features**:
- Retrieves permissions for a specific group.

### CreateAdminStaffGroupsAPIView

**Purpose**: 
Allows the creation of admin staff groups.

**Key Features**:
- Retrieves and creates staff groups.

### RetrieveUpdateDestroyAdminStaffPermissionAPIView

**Purpose**: 
Handles viewing, updating, and deletion of permission groups.

**Key Features**:
- Manages permissions for staff groups.

### PermissionViewSet

**Purpose**: 
Provides a read-only view set for permissions.

### ListUsersReportAPIView

**Purpose**: 
View report details for users.

**Key Features**:
- Generates reports on user data with filters.

### ListComplaintsReportAPIView

**Purpose**: 
View report details of user complaints.

**Key Features**:
- Filters complaints based on date and status.

### ExportReportCSVAPIView

**Purpose**: 
Exports filtered data into a CSV file.

**Key Features**:
- Supports exporting reports for users, complaints, transactions, and lobbies.
- Uploads CSV to an AWS S3 bucket.

### UserFreelobbyLimitAPIView

**Purpose**: 
Manages the free lobby limit for users.

**Key Features**:
- Updates the limit for free lobbies for individual users.

This comprehensive set of API views provides robust functionalities for managing users, transactions, staff, and reports within the Ryvals platform. Each view is equipped with permission checks, ensuring that only authorized administrators can perform sensitive operations.