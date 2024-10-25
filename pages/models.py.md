# models.py Documentation 📄

Welcome to the **models.py** documentation! In this document, we will explore the structure and functionality provided by the `models.py` file. This file is crucial in defining the data structure for your Django application, particularly concerning the static pages and FAQs. 🌟

## Table of Contents
1. [Introduction](#introduction)
2. [Imports](#imports)
3. [Classes and Models](#classes-and-models)
   - [StaticPage Model](#staticpage-model)
   - [Topic Model](#topic-model)
   - [Question Model](#question-model)
4. [Key Features](#key-features)
5. [Conclusion](#conclusion)

## Introduction

The `models.py` file is an integral part of a Django application. It defines the database schema and is responsible for creating, retrieving, updating, and deleting records. In this file, models are defined to handle content for static pages, topics, and frequently asked questions (FAQs).

## Imports 📦

```python
from django.db import models
from django.utils.text import slugify
from ryvals.core.models import TimeStampModel
from django.utils.translation import gettext_lazy as _
```

- **`models`**: Provides the base classes for defining database models.
- **`slugify`**: Utility to create URL-friendly representations of titles or names.
- **`TimeStampModel`**: An inherited model presumably providing timestamp fields (`created` and `modified`).
- **`gettext_lazy`**: Utility for lazy translation of strings for internationalization.

## Classes and Models

### StaticPage Model

```python
class StaticPage(TimeStampModel):
    """ Static Page Model
    Will store content for pages like:
    1. Privacy Policy
    2. Terms and Conditions
    """
```

#### Fields
- **`title`**: A `CharField` with a maximum length of 40, unique, and translatable.
- **`content`**: A `TextField` for storing the main content of the static page.
- **`slug`**: A `SlugField` generated from the `title`, unique, and URL-friendly.

#### Methods
- **`__str__`**: Returns the title of the static page.
- **`save`**: Overrides the save method to auto-generate the slug from the title before saving.

#### Meta Options
- `verbose_name`: "Static Page"
- `verbose_name_plural`: "Static Pages"

### Topic Model

```python
class Topic(TimeStampModel):
    """ Topic Model for FAQs """
```

#### Fields
- **`name`**: A `CharField` for the name of the topic.
- **`slug`**: A `SlugField` for a unique URL-friendly representation of the topic name.
- **`sort_order`**: An integer determining the display order of topics.
- **`type`**: An integer field with choices defining the type of topic (PPK or FAQ).

#### Nested Class
- **`Type`**: Defines choices for the topic type.

#### Meta Options
- `verbose_name`: "Topic"
- `verbose_name_plural`: "Topics"
- `ordering`: Orders by `sort_order` then `id`.

#### Methods
- **`save`**: Overrides the save method to auto-generate the slug.
- **`__str__`**: Returns the name of the topic.

### Question Model

```python
class Question(TimeStampModel):
    """ Frequently Asked Questions Model """
```

#### Fields
- **`question`**: A `TextField` for the FAQ question.
- **`answer`**: A `TextField` for the FAQ answer.
- **`topic`**: A `ForeignKey` linking to a `Topic`.
- **`status`**: An integer choice field for the status of the question.
- **`sort_order`**: Determines the display order within the topic.

#### Nested Class
- **`Status`**: Defines if the question is active or inactive.

#### Meta Options
- `verbose_name`: "Frequently Asked Question"
- `verbose_name_plural`: "Frequently Asked Questions"
- `ordering`: Orders by `topic__sort_order`, `sort_order`, then `id`.

#### Methods
- **`__str__`**: Returns the question text.

## Key Features ✨

- **Translation**: All models and fields are prepared for internationalization.
- **Slug Generation**: Automatic slug generation ensures URL-friendly strings.
- **Custom Ordering**: Topics and questions are ordered to enhance display logic.
- **Choices for Enums**: Use of `IntegerChoices` for easily manageable categorical fields.

## Conclusion

The `models.py` file is structured to handle static page content and FAQs efficiently. It leverages Django’s ORM capabilities to simplify database interactions while making provisions for future scaling and internationalization. With clear meta options and methods, this file lays a robust foundation for handling page content dynamically. 🚀

Feel free to explore additional features or customization according to your application's needs!