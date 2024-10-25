# Documentation for `user_serializers.py`

This documentation provides a detailed explanation of the `user_serializers.py` file, which is responsible for handling various user-related operations through serializers in a Django-based application. The primary focus is on user management, including activation status, administration, referrals, and permissions.

## Index

1. [Overview](#overview)
2. [Serializers](#serializers)
   - [UserListSerializer](#userlistserializer)
   - [AccountActivationDetailSerializer](#accountactivationdetailserializer)
   - [UserDetailAdminSerializer](#userdetailadminserializer)
   - [UpdateUserActivationStatusSerializer](#updateuseractivationstatusserializer)
   - [AddAdminStaffSerializer](#addadminstaffserializer)
   - [EditAdminStaffSerializer](#editadminstaffserializer)
   - [ListAdminStaffSerializer](#listadminstaffserializer)
   - [AdminStaffDetailSerializer](#adminstaffdetailserializer)
   - [SeizeMoneySerializer](#seizemoneyserializer)
   - [ListUserTransactionHistorySerializer](#listusertransactionhistoryserializer)
   - [TransactionStatusUpdateSerializer](#transactionstatusupdateserializer)
   - [RefereeListSerializer](#refereelistserializer)
   - [RefereeDetailSerializer](#refereedetailserializer)
   - [UserAffiliateDaysSerializer](#useraffiliatedaysserializer)
   - [UserReferralCodeSerializer](#userreferralcodeserializer)
   - [PermissionSerializer](#permissionserializer)
   - [ListAdminStaffPermissionSerializer](#listadminstaffpermissionserializer)
   - [CreateAdminStaffGroupsSerializer](#createadminstaffgroupsserializer)
   - [DetailAdminStaffPermissionSerializer](#detailadminstaffpermissionserializer)
   - [EditAdminStaffPermissionSerializer](#editadminstaffpermissionserializer)
   - [PermissionsSerializer](#permissionsserializer)
   - [ContentTypeSerializer](#contenttypeserializer)
   - [ListUsersReportSerializer](#listusersreportserializer)
   - [ListComplaintsReportSerializer](#listcomplaintsreportserializer)
   - [UserFreeLobbyLimitSerializer](#userfreelobbylimitserializer)
3. [Utilities and Constants](#utilities-and-constants)

---

## Overview

This file is part of a Django REST Framework application that provides serialization and validation for user-related data. It includes serializers for user activation, administrative actions, user transactions, and referral management. The serializers are used to convert complex data types like querysets and model instances into native Python data types that can be easily rendered into JSON or XML, and vice versa.

---

## Serializers

### UserListSerializer

- **Purpose**: Provides user information for the User List API.
- **Fields**:
  - `joining_date`: User's joining date.
  - `account_status`: Current status of the user account.
  - `referral`: Referral details including name and code.

### AccountActivationDetailSerializer

- **Purpose**: Serializes user account activation details.
- **Fields**:
  - `status_modified_by`: Details of the admin who modified the status.

### UserDetailAdminSerializer

- **Purpose**: Provides detailed user information for the User Detail API.
- **Fields**:
  - `account_status`: Account activation status.
  - `social_accounts`: Connected social accounts.
  - `referral`: Referral details.

### UpdateUserActivationStatusSerializer

- **Purpose**: Updates the status of a user.
- **Methods**:
  - `validate`: Ensures proper status transitions.
  - `update`: Changes user status and logs the action.

### AddAdminStaffSerializer

- **Purpose**: Adds a new admin staff member.
- **Methods**:
  - `validate`: Validates input data for adding admin staff.
  - `create`: Creates a new admin user and assigns permissions.

### EditAdminStaffSerializer

- **Purpose**: Edits existing admin staff details.
- **Methods**:
  - `validate`: Validates input data for editing admin staff.
  - `update`: Updates admin staff details and logs changes.

### ListAdminStaffSerializer

- **Purpose**: Lists all admin staff members.
- **Fields**: Basic admin staff details like name, email, role, and status.

### AdminStaffDetailSerializer

- **Purpose**: Provides detailed information about an admin staff member.
- **Fields**:
  - `address`: Address details of the admin.
  - `permission`: Permissions assigned to the admin.

### SeizeMoneySerializer

- **Purpose**: Handles money seizure from user accounts.
- **Methods**:
  - `validate`: Checks user status before seizure.
  - `update`: Updates the user's financial details and logs the action.

### ListUserTransactionHistorySerializer

- **Purpose**: Serializes user transaction history.
- **Fields**: Details about transactions like payee, receiver, amount, and status.

### TransactionStatusUpdateSerializer

- **Purpose**: Allows releasing or seizing player transactions.
- **Methods**:
  - `update`: Updates the status of transactions.

### RefereeListSerializer

- **Purpose**: Lists all referees who invited friends through referrals.
- **Fields**: Detailed information about each referee's earnings and referrals.

### RefereeDetailSerializer

- **Purpose**: Provides details of all referrals made by a referee.
- **Fields**: Includes overall and monthly earnings, referral details, and code.

### UserAffiliateDaysSerializer

- **Purpose**: Manages players' referral days individually.
- **Methods**:
  - `validate_days`: Validates the number of days.
  - `update`: Updates affiliate days for a user.

### UserReferralCodeSerializer

- **Purpose**: Updates a user's referral code.
- **Methods**:
  - `validate`: Checks for code length and duplication.
  - `update`: Applies changes to the referral code.

### PermissionSerializer

- **Purpose**: Serializes group permissions.
- **Fields**: Permissions and their details.

### ListAdminStaffPermissionSerializer

- **Purpose**: Lists all permissions for admin staff.
- **Fields**: Permissions associated with a group.

### CreateAdminStaffGroupsSerializer

- **Purpose**: Creates groups with permissions for staff.
- **Methods**:
  - `validate`: Checks for group name conflicts.
  - `create`: Adds a new group with specified permissions.

### DetailAdminStaffPermissionSerializer

- **Purpose**: Provides detailed information about admin group permissions.
- **Methods**:
  - `get_permissions`: Retrieves permissions for a content type.

### EditAdminStaffPermissionSerializer

- **Purpose**: Edits group names and permissions.
- **Methods**:
  - `validate`: Ensures uniqueness of group names.
  - `update`: Updates group details and permissions.

### PermissionsSerializer

- **Purpose**: Retrieves the list of group permissions.

### ContentTypeSerializer

- **Purpose**: Serializes content type details, including permissions.
- **Fields**: Label, verbiage, and permissions.

### ListUsersReportSerializer

- **Purpose**: Gathers player details for reporting.
- **Fields**: Player name, referral details, and join date.

### ListComplaintsReportSerializer

- **Purpose**: Provides details of user complaints.
- **Fields**: Complaint details including game, lobby, and participants.

### UserFreeLobbyLimitSerializer

- **Purpose**: Manages players' free lobby limits individually.
- **Methods**:
  - `validate`: Validates lobby limit.
  - `update`: Applies changes to lobby limits.

---

## Utilities and Constants

- **Helper Functions and Methods**: Functions like `validate`, `update`, and `create` are used extensively for validating input data and updating the database.
- **Constants**: Various constants such as `FIRST_NAME_CONST` and `LAST_NAME_CONST` are used for validation and error messages.
- **Logging**: Logging is implemented using the `logging` module to track operations and errors.