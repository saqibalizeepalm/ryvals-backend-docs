# 📜 Documentation: `urls.py`

The `urls.py` file is an essential component in Django projects, responsible for mapping URL patterns to views. This file acts as a router, directing incoming HTTP requests to the appropriate view based on the URL path. Below, we delve into the specifics and purpose of the code found in the `urls.py` file.

## 🗂️ Index

1. [Import Statements](#import-statements)
2. [Application Name](#application-name)
3. [URL Patterns](#url-patterns)
   - [List Static Pages](#list-static-pages)
   - [Retrieve Static Page](#retrieve-static-page)
   - [List FAQs](#list-faqs)
4. [Summary](#summary)

## Import Statements

```python
from django.urls import path
from pages.api.views import ListFAQAPIView, ListStaticPageAPIView, RetrieveStaticPageAPIView
```

- **`django.urls.path`**: This function is used to define URL patterns. It takes a route, a view, and an optional name.
- **View Imports**: The `ListFAQAPIView`, `ListStaticPageAPIView`, and `RetrieveStaticPageAPIView` are imported from the `pages.api.views` module. These views correspond to the URL paths defined later in the file.

## 🔖 Application Name

```python
app_name = 'api_admin_v1'
```

- **`app_name`**: This variable sets a namespace for the application. It helps in uniquely identifying the URLs in case of multiple apps, avoiding conflicts.

## 🌐 URL Patterns

The `urlpatterns` list contains path instances that map URLs to views. Each path is defined with a specific route, view, and name.

```python
urlpatterns = [
    path('static/', ListStaticPageAPIView.as_view(), name='list_static_page'),
    path('static/<slug:slug>/', RetrieveStaticPageAPIView.as_view(), name='retrieve_static_page'),
    path('faqs/', ListFAQAPIView.as_view(), name='list_faq'),
]
```

### List Static Pages

- **Path**: `static/`
- **View**: `ListStaticPageAPIView.as_view()`
- **Name**: `'list_static_page'`

This entry maps the URL path `static/` to the `ListStaticPageAPIView`, which is responsible for listing all static pages.

### Retrieve Static Page

- **Path**: `static/<slug:slug>/`
- **View**: `RetrieveStaticPageAPIView.as_view()`
- **Name**: `'retrieve_static_page'`

This pattern captures a slug from the URL path and maps it to the `RetrieveStaticPageAPIView`. This view retrieves the content of a specific static page based on the slug provided.

### List FAQs

- **Path**: `faqs/`
- **View**: `ListFAQAPIView.as_view()`
- **Name**: `'list_faq'`

This URL maps to the `ListFAQAPIView`, which serves to list all Frequently Asked Questions (FAQs).

## 📝 Summary

The `urls.py` file in this project is dedicated to defining URL routes for API endpoints related to static pages and FAQs. It includes:

- Listing and retrieving static pages.
- Listing FAQs.

By organizing these patterns neatly, the application can efficiently handle requests and direct them to the appropriate views, ensuring a seamless experience for API consumers. This modular approach enhances maintainability and scalability within the Django framework.