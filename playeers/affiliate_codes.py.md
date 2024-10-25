# Documentation for `affiliate_codes.py`

## Overview

The `affiliate_codes.py` script is a Django management command designed to assign affiliate (referral) codes to users who have signed up but do not yet have one. This is particularly useful for awarding referral bonuses or tracking user sign-ups through referral marketing.

## Functionality

### Command Class

- **Class**: `Command`
- **Inherits From**: `BaseCommand`

#### Attributes

- **help**: A brief description of what the command does, which is "Assign Affiliate codes for already signup users".

#### Methods

- **handle(self, *args, **kwargs)**: This is the core method executed when the command is run. It performs the following steps:

  1. **Query Users Without Referral Codes**:
     - The command queries all user profiles from the `Profile` model where the `referral_code` field is `null`.
     - This is achieved using Django's ORM: `Profile.objects.filter(referral_code__isnull=True)`.

  2. **Count Profiles**:
     - It counts the number of profiles retrieved by the query using `.count()`.

  3. **Assign Referral Codes**:
     - If there are profiles without referral codes, the command iterates over each profile:
       - Generates a unique affiliate code using `UtilityMethods.generate_ref_code(player.user.username)`.
       - Assigns this code to the user's `referral_code` attribute and saves the profile.

  4. **Output Result**:
     - If referral codes were assigned, it outputs "Referral Codes Assign Successfully".
     - If all users already have referral codes, it outputs "All users have Affiliate Code".

### Utility Methods

- **UtilityMethods.generate_ref_code(username)**: This method is used to generate a unique referral code based on the user's username. The implementation details of this method are not shown here but are assumed to ensure uniqueness and possibly adhere to a specific format.

## Usage

To run this command, you would use Django's management command execution from the command line:

```bash
python manage.py <command_name>  # where <command_name> is the name registered for this script
```

## Code Block

Here is the main structure of the `affiliate_codes.py`:

```python
from accounts.models import Profile
from app.utils import UtilityMethods
from django.core.management.base import BaseCommand

class Command(BaseCommand):
    help = 'Assign Affiliate codes for already signup users'

    def handle(self, *args, **kwargs):
        all_profile = Profile.objects.filter(referral_code__isnull=True)
        profile_count = all_profile.count()
        if profile_count > 0:
            for player in all_profile:
                affilate_code = UtilityMethods.generate_ref_code(player.user.username)
                player.referral_code = affilate_code
                player.save()
            self.stdout.write('Referral Codes Assign Successfully')
        else:
            self.stdout.write('All users have Affiliate Code')
```

## Conclusion

The `affiliate_codes.py` script is a useful tool for bulk assigning referral codes to existing users who lack them, enabling seamless referral tracking and marketing efforts. This management command can be easily integrated and executed within a Django project to ensure all users have the necessary affiliate codes.