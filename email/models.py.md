# Documentation for `models.py` 📄

The `models.py` file is an essential part of a Django application. It defines the structure of the database tables, often referred to as models, which are used to store and manage data. Below is a detailed documentation of the `models.py` file provided.

## Table of Contents 📚
1. [Overview](#overview)
2. [Imported Modules](#imported-modules)
3. [Models Defined](#models-defined)
   - [EmailMessage Model](#emailmessage-model)
   - [Feedback Model](#feedback-model)
4. [Field Descriptions](#field-descriptions)
5. [Meta Class](#meta-class)
6. [String Representation](#string-representation)

---

## Overview

The `models.py` file defines two main models: **EmailMessage** and **Feedback**. These models are used to represent and manipulate email messages and feedback records in the application.

## Imported Modules

```python
from django.db import models
from django.conf import settings
from ryvals.core.enumerators import Regex
from ryvals.core.models import TimeStampModel
from django.core.validators import RegexValidator
from django.contrib.postgres.fields import ArrayField
from django.utils.translation import gettext_lazy as _
```
- **Django Modules**: These provide the necessary classes and functions to define and work with models.
- **Custom Modules**: Includes custom enumerators and models like `TimeStampModel` and `Regex` for specific functionalities.

## Models Defined

### EmailMessage Model

The **EmailMessage** model is designed to store details about email communications:

| **Field**         | **Type**                   | **Description**                                                                 |
|-------------------|----------------------------|---------------------------------------------------------------------------------|
| `from_email`      | `EmailField`               | Email address of the sender; defaults to `settings.EMAIL_DEFAULT`.               |
| `to_email`        | `ArrayField` of `EmailField`| List of recipient email addresses.                                              |
| `cc`              | `ArrayField` of `EmailField`| List of CC email addresses.                                                     |
| `bcc`             | `ArrayField` of `EmailField`| List of BCC email addresses.                                                    |
| `subject`         | `TextField`                | Subject line of the email.                                                      |
| `html_message`    | `TextField`                | HTML content of the email message.                                              |
| `tries`           | `PositiveSmallIntegerField`| Number of attempts made to send the email.                                      |
| `error_detail`    | `CharField`                | Details of any errors encountered.                                              |
| `sent_status`     | `PositiveSmallIntegerField`| Current status of the email (e.g., Pending, Sent, Error).                       |
| `send_date`       | `DateTimeField`            | Date and time when the email was sent.                                          |

- **Type Choices**: An inner class defining different statuses (Pending, In-Progress, Sent, Error) for the email.

### Feedback Model

The **Feedback** model captures user feedback information:

| **Field**  | **Type**   | **Description**                                           |
|------------|------------|-----------------------------------------------------------|
| `name`     | `CharField`| Name of the feedback provider.                            |
| `email`    | `EmailField`| Email address of the feedback provider.                  |
| `phone`    | `CharField`| Phone number of the feedback provider, with validation.   |
| `feedback` | `TextField` | Detailed feedback content.                                |

## Field Descriptions

- **EmailField**: Used to store email addresses.
- **ArrayField**: Stores an array of values, suitable for multiple email addresses.
- **CharField**: Stores string data with a maximum length.
- **TextField**: Stores larger text data.
- **PositiveSmallIntegerField**: Stores small positive integers.
- **DateTimeField**: Stores date and time information.
- **RegexValidator**: Validates input based on a regular expression pattern.

## Meta Class

```python
class Meta:
    verbose_name = _('Email Message')
    verbose_name_plural = _('Email Messages')
```

- Provides a human-readable singular and plural name for the **EmailMessage** model.

## String Representation

```python
def __str__(self):
    return f'{self.id}'
```

- The `__str__` method returns a string representation of the model instance, typically used for display purposes.

---

This concludes the detailed documentation for `models.py`. Each model and its fields are carefully designed to facilitate the management of email data and user feedback within the application. 🎉