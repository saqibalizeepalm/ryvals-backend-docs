# 📜 Documentation for `models.py`

This documentation provides a comprehensive overview of the `models.py` file, which is a part of a Django application. This file defines the data models used within the application, specifically related to user addresses and country sender IDs.

## Index

1. [Overview](#overview)
2. [Dependencies](#dependencies)
3. [Models](#models)
   - [Address](#address)
   - [CountrySenderId](#countrysenderid)
4. [Key Properties and Methods](#key-properties-and-methods)
   - [Address Properties](#address-properties)
5. [Meta Options](#meta-options)

## Overview

The `models.py` file is responsible for defining two key data models:

- `Address`: A model that represents a user's address.
- `CountrySenderId`: A model storing sender IDs associated with countries.

## Dependencies

The file imports several modules and classes:

```python
from django.db import models
from django.contrib.auth import get_user_model
from ryvals.core.models import AbstractBaseAddress
from django.utils.translation import ugettext_lazy as _
from cities_light.models import Country
```

- **Django Models**: Core functionality for defining database models.
- **User Model**: Utilizes Django's `get_user_model` for referencing the user.
- **AbstractBaseAddress**: An abstract model class that provides base address functionality.
- **Translation Utilities**: For managing translatable fields.
- **Country Model**: From `cities_light.models`, representing country data.

## Models

### Address

The `Address` model extends `AbstractBaseAddress` and represents an address associated with a user.

```python
class Address(AbstractBaseAddress):
    ''' User Address Model '''
    user = models.ForeignKey(User, on_delete=models.CASCADE, related_name='user_address')
```

- **`user`**: A foreign key linking the address to a user. Deletion of a user will cascade and delete associated addresses.

### CountrySenderId

The `CountrySenderId` model stores sender IDs linked to specific countries.

```python
class CountrySenderId(models.Model):
    country = models.ForeignKey(Country, on_delete=models.CASCADE, related_name='sender_country')
    sender_id = models.CharField(max_length=20, default=None, null=True)
```

- **`country`**: A foreign key to the `Country` model.
- **`sender_id`**: A character field storing the sender ID.

## Key Properties and Methods

### Address Properties

- **`address`**: A property method that constructs and returns a detailed address dictionary, including the full address and individual components like street, city, state, postal code, and country.

```python
@property
def address(self):
    # Code to build the address details
    return {
        'full': address,
        'street_address': self.street_address,
        'city': self.city,
        'state': self.state,
        'postal_code': self.postal_code,
        'country': country,
        'country_id': country_id,
        'country_code': f'+{country_phone}'
    }
```

## Meta Options

### Address Meta

- **`verbose_name`**: Human-readable name for the model.
- **`verbose_name_plural`**: Plural form of the model's name.

```python
class Meta:
    verbose_name = _('Address')
    verbose_name_plural = _('Addresses')
```

### CountrySenderId Meta

- **`verbose_name_plural`**: Plural form of the model's name, in this case, "Country Sender IDs".

```python
class Meta:
    verbose_name_plural = _('Country Sender IDs')
```

## Summary

The `models.py` file is integral to managing user address data and associating sender IDs with countries within the application. It utilizes Django's model framework to define relationships and ensure data integrity, providing a structured way to handle address-related data.