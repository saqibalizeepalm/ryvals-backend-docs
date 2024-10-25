# 📄 `views.py` Documentation

This documentation provides an in-depth look at the `views.py` file used in a Django application. This file contains several API views for handling requests related to static pages, FAQs, and topics. The views utilize Django REST framework's generic views to provide streamlined API functionality.

## 🗂️ Table of Contents

1. [Overview](#overview)
2. [Classes and Functionality](#classes-and-functionality)
   - [ListStaticPageAPIView](#liststaticpageapiview)
   - [RetrieveStaticPageAPIView](#retrievestaticpageapiview)
   - [ListFAQAPIView](#listfaqapiview)
   - [ListTopicAPIView](#listtopicapiview)
3. [Summary](#summary)

## 🌟 Overview

The `views.py` file is a crucial part of the Django application, acting as the intermediary between the model layer and the client. It handles HTTP requests and returns appropriate HTTP responses. This file specifically deals with views related to static pages, frequently asked questions (FAQs), and topics.

**Key Imports:**

```python
from rest_framework import generics
from django.db.models.query_utils import Q
from pages.messages import STATIC_PAGE_NOT_FOUND
from rest_framework.exceptions import APIException
from pages.models import Question, StaticPage, Topic
from pages.api.serializers import DetailStaticPageSerializer, ListFAQSerializer, ListStaticPageSerializer, ListTopicSerializer
```

### ⚙️ Key Components:

- **Django REST Framework**: Utilizes built-in classes like `ListAPIView` and `RetrieveAPIView` for API view operations.
- **Custom Messages and Exceptions**: Uses custom error messages and raises exceptions when specific conditions are met.
- **Serializers**: Connects models with views to facilitate data representation.

## 🚀 Classes and Functionality

### 1. `ListStaticPageAPIView`

- **Purpose**: Provides a list view for all static pages.
- **Key Attributes**:
  - `serializer_class`: Uses `ListStaticPageSerializer` to serialize the data.
  - `queryset`: Retrieves all instances of `StaticPage`.

```python
class ListStaticPageAPIView(generics.ListAPIView):
    serializer_class = ListStaticPageSerializer
    queryset = StaticPage.objects.all()
```

### 2. `RetrieveStaticPageAPIView`

- **Purpose**: Retrieves a single static page based on a provided slug.
- **Key Methods**:
  - `get_object`: Fetches the object using the slug; raises `APIException` if not found.

```python
class RetrieveStaticPageAPIView(generics.RetrieveAPIView):
    serializer_class = DetailStaticPageSerializer

    def get_object(self):
        slug = self.kwargs.get('slug')
        try:
            page = StaticPage.objects.get(slug=slug)
        except StaticPage.DoesNotExist:
            raise APIException(STATIC_PAGE_NOT_FOUND)
        return page
```

### 3. `ListFAQAPIView`

- **Purpose**: Lists FAQs filtered by type if specified.
- **Key Methods**:
  - `get_serializer_class`: Returns the `ListFAQSerializer`.
  - `get_queryset`: Dynamically filters topics based on query parameters.

```python
class ListFAQAPIView(generics.ListAPIView):
    
    def get_serializer_class(self):
        return ListFAQSerializer

    def get_queryset(self):
        faq_type = self.request.GET.get('type')
        if faq_type:
            faq_type = faq_type.strip()
            queryset = Topic.objects.filter(type=Topic.Type[faq_type].value).order_by('sort_order')
        else:
            queryset = Topic.objects.all().order_by('sort_order')
        return queryset
```

### 4. `ListTopicAPIView`

- **Purpose**: Provides a list view for all topics.
- **Key Attributes**:
  - `serializer_class`: Uses `ListTopicSerializer` to serialize the data.
  - `queryset`: Retrieves all instances of `Topic`.

```python
class ListTopicAPIView(generics.ListAPIView):
    serializer_class = ListTopicSerializer
    queryset = Topic.objects.all()
```

## 📚 Summary

The `views.py` file in this Django application efficiently handles API requests related to static pages, FAQs, and topics. By leveraging Django REST framework's generic views, it simplifies the process of creating robust and scalable API endpoints. Each class in the file serves a specific purpose, ensuring that the application remains organized and maintainable. The use of serializers and custom exceptions further enhances the application's ability to manage data and error scenarios effectively.