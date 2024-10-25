# Documentation for `serializers.py` 📄

**File Overview**:  
The `serializers.py` file is a crucial part of a Django REST Framework (DRF) application. This file contains classes that are used to serialize and deserialize data, allowing complex data types such as querysets and model instances to be converted to native Python data types. This conversion facilitates rendering into JSON or other content types suitable for client-side consumption.

## Table of Contents
- [Import Statements](#import-statements)
- [Classes and Their Purpose](#classes-and-their-purpose)
  - [ListStaticPageSerializer](#liststaticpageserializer)
  - [DetailStaticPageSerializer](#detailstaticpageserializer)
  - [QuestionListSerializer](#questionlistserializer)
  - [ListFAQSerializer](#listfaqserializer)
  - [ListTopicSerializer](#listtopicserializer)

## Import Statements 🚀

```python
from rest_framework import serializers
from pages.models import Question, StaticPage, Topic
from django.utils.translation import gettext_lazy as _
```

### Explanation:
- **`rest_framework.serializers`**: This module provides the base class for creating serializers in DRF.
- **`pages.models`**: Importing the `Question`, `StaticPage`, and `Topic` models to define the structure of data being serialized.
- **`gettext_lazy`**: Used for internationalization, allowing strings to be translated.

## Classes and Their Purpose 🎯

### 1. `ListStaticPageSerializer`
```python
class ListStaticPageSerializer(serializers.ModelSerializer):
    ''' List Static Page Serializer '''
    class Meta:
        model = StaticPage
        fields = ['id', 'title', 'slug']
```
- **Purpose**: This serializer is used to represent the essential details of a `StaticPage` model, specifically listing its `id`, `title`, and `slug`.

### 2. `DetailStaticPageSerializer`
```python
class DetailStaticPageSerializer(serializers.ModelSerializer):
    ''' Detail Static Page Serializer '''
    class Meta:
        model = StaticPage
        fields = ['id', 'title', 'slug', 'content']
```
- **Purpose**: Provides a detailed representation of a `StaticPage`, including its `content` field in addition to `id`, `title`, and `slug`.

### 3. `QuestionListSerializer`
```python
class QuestionListSerializer(serializers.ModelSerializer):
    class Meta:
        model = Question
        fields = ['id', 'question', 'answer', 'topic', 'status', 'sort_order']
```
- **Purpose**: Serializes the `Question` model, covering all fields necessary for listing FAQs: `id`, `question`, `answer`, `topic`, `status`, and `sort_order`.

### 4. `ListFAQSerializer`
```python
class ListFAQSerializer(serializers.ModelSerializer):
    ''' List Frequently Asked Questions '''
    category = serializers.SerializerMethodField('get_question')

    def get_question(self, obj):
        response = {'name': obj.name, 'slug': obj.slug, 'questions': None}
        questions = Question.objects.filter(topic=obj, status=Question.Status.ACTIVE)
        if questions:
            question_list = QuestionListSerializer(questions, many=True).data
            response['questions'] = question_list
        return response

    class Meta:
        model = Topic
        fields = ['id', 'category', 'sort_order', 'type']
```
- **Purpose**: This serializer focuses on listing FAQs by topics. It customizes the output using a method field `get_question` to include active questions related to each topic.

### 5. `ListTopicSerializer`
```python
class ListTopicSerializer(serializers.ModelSerializer):
    ''' List Topic Serializer '''
    class Meta:
        model = Topic
        fields = ['id', 'name', 'sort_order', 'slug', 'type']
```
- **Purpose**: Provides a concise representation of the `Topic` model, including its `id`, `name`, `sort_order`, `slug`, and `type`.

---

Each class in `serializers.py` is tailored to convert model instances into a format that can be easily rendered into JSON, ensuring that data can be effectively communicated between the backend and frontend of a Django application. These serializers also encapsulate the logic needed to include related data, handle nested structures, and manage data validation, playing a pivotal role in the API's functionality.