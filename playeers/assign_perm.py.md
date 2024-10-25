# Documentation for `assign_perm.py`

This script is part of a Django management command that assigns newly added permissions to all super admins, excluding a particular admin specified by their email. This can be particularly useful when new permissions are introduced to the system and need to be distributed to existing super admins without manually updating each admin's permissions.

### Overview

- **Purpose**: To automate the assignment of new permissions to all super admin users except the one specified.
- **Functionality**: The script fetches permissions related to a specific admin and assigns these permissions to all other super admins who are marked as admin owners.

### Components

#### Imports

```python
from accounts.models import RyvalsAdmin
from django.contrib.auth.models import Permission
from django.core.management.base import BaseCommand
```

- **RyvalsAdmin**: Custom model representing admin users in the system.
- **Permission**: Django's built-in model that handles permissions.
- **BaseCommand**: Provides the structure for creating custom Django management commands.

#### Command Class

```python
class Command(BaseCommand):
```

This class inherits from `BaseCommand`, allowing it to be executed as a Django management command.

- **help**: A string that describes what the command does. This is shown when the help command is run.

#### Handle Method

```python
def handle(self, *args, **kwargs):
```

- **Purpose**: The main logic of the command resides here. It is executed whenever the command is called.

##### Steps

1. **Identify Specific Admin**:
   ```python
   email = 'ryvalsuper1@mailinator.com'
   permission = Permission.objects.filter(user=RyvalsAdmin.objects.get(email=email))
   ```
   - Fetches the admin identified by the given email.
   - Retrieves all permissions associated with this admin.

2. **Assign Permissions to Other Super Admins**:
   ```python
   admins = RyvalsAdmin.objects.filter(is_admin_owner=True).exclude(email=email)
   [admin.user_permissions.set(permission) for admin in admins]
   ```
   - Fetches all admins who are designated as admin owners but excludes the specified email.
   - Assigns the fetched permissions to these admins.

3. **Output Results**:
   ```python
   if len(admins) > 0:
       self.stdout.write('Assigned all new permission to all super admins')
   else:
       self.stdout.write('Every admin have full permissions')
   ```
   - Provides console feedback on whether the permissions were assigned or if no eligible admins were found.

### Usage

To run this command:
1. Navigate to your Django project's root directory.
2. Execute the command using:
   ```
   python manage.py <command_name>
   ```
   Replace `<command_name>` with the name you have given to this management command in your Django project.

### Conclusion

This script automates the tedious task of assigning new permissions to super admins. By ensuring that all admin owners except the one specified receive the appropriate permissions, it maintains consistency and security across the admin panel.