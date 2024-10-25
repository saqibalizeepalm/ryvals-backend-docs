# Views.py Documentation 📄

The `views.py` file in a Django application is where you define your application's views. Views are essentially the request handlers. They contain the logic to process user requests, interact with models and serializers, and return responses. This file is often where most of the business logic for handling HTTP requests is located.

## Index

1. [Imports](#imports)
2. [Class-Based Views](#class-based-views)
   - [CountriesView](#countriesview)
   - [RegionsView](#regionsview)
   - [CitiesView](#citiesview)
3. [Utility Functions](#utility-functions)
   - [generate_sas_token](#generate_sas_token)
4. [API Views](#api-views)
   - [SASView](#sasview)

---

### Imports

```python
from django.conf import settings
from rest_framework import generics
from datetime import datetime, timedelta
from rest_framework.views import APIView
from rest_framework.response import Response
from cities_light.models import (Country, Region, City)
from azure.storage.blob import BlockBlobService, ContainerPermissions
from ryvals.core.permissions import PrivateTokenAccessPermission, IsActivated
from configurations.api.serializers import CitySerializer, CountrySerializer, RegionSerializer
```

- **Django Imports**: Used for general configuration and settings.
- **Django REST Framework Imports**: Used for creating API views.
- **Datetime Imports**: Used for handling time-related tasks.
- **Azure Storage Imports**: Used for handling Azure Blob Storage operations.
- **Custom Imports**: Include models, permissions, and serializers specific to this project.

---

### Class-Based Views

#### CountriesView

- **Purpose**: To list all available countries.
- **Inheritance**: Inherits from `generics.ListAPIView`, which provides the `.list()` method.
- **Serializer**: Uses `CountrySerializer` to serialize country data.
- **QuerySet**: Retrieves all country objects.

```python
class CountriesView(generics.ListAPIView):
    serializer_class = CountrySerializer
    queryset = Country.objects.all()
```

#### RegionsView

- **Purpose**: To list regions based on a specific country.
- **Inheritance**: Inherits from `generics.ListAPIView`.
- **Serializer**: Uses `RegionSerializer`.
- **QuerySet**: Filters regions by `country_id` obtained from the request's `kwargs`.

```python
class RegionsView(generics.ListAPIView):
    serializer_class = RegionSerializer

    def get_queryset(self):
        country_id = self.kwargs.get('country_id')
        queryset = Region.objects.filter(country_id=country_id)
        return queryset
```

#### CitiesView

- **Purpose**: To list cities based on a specific region.
- **Inheritance**: Inherits from `generics.ListAPIView`.
- **Serializer**: Uses `CitySerializer`.
- **QuerySet**: Filters cities by `region_id`.

```python
class CitiesView(generics.ListAPIView):
    serializer_class = CitySerializer

    def get_queryset(self):
        region_id = self.kwargs.get('region_id')
        queryset = City.objects.filter(region_id=region_id)
        return queryset
```

---

### Utility Functions

#### generate_sas_token

- **Purpose**: Generates a Shared Access Signature (SAS) token for Azure Blob Storage.
- **Logic**: Uses `BlockBlobService` to create a SAS token with read, write, delete, and list permissions. Token is valid for 10 minutes.

```python
def generate_sas_token():
    blob_service = BlockBlobService(account_name=settings.AZURE_ACC_NAME, account_key=settings.AZURE_PRIMARY_KEY)
    sas_token = blob_service.generate_container_shared_access_signature(
        settings.AZURE_CONTAINER,
        permission=ContainerPermissions.READ + ContainerPermissions.WRITE + ContainerPermissions.DELETE + ContainerPermissions.LIST,
        expiry=datetime.utcnow() + timedelta(minutes=10)
    )
    return sas_token
```

---

### API Views

#### SASView

- **Purpose**: To provide a secure way to generate and expose SAS tokens to clients.
- **Inheritance**: Inherits from `APIView`.
- **Permission Classes**: Uses `PrivateTokenAccessPermission` and `IsActivated` to ensure secure access.
- **HTTP Methods**: Implements the `GET` method to generate and return a SAS token.

```python
class SASView(APIView):
    '''
    https://velog.io/@zlslsp54/How-to-access-azure-storage-files-secure
    '''
    permission_classes = (PrivateTokenAccessPermission, IsActivated)

    def get(self, request):
        token = generate_sas_token()
        return Response({
            'url': 'https://' + settings.AZURE_ACC_NAME + '.blob.core.windows.net/?' + token,
            'token': token
        })
```

---

This documentation provides a comprehensive overview of the `views.py` file. Each section explains the purpose of the code and provides code snippets for clarity. Feel free to add more views or modify existing ones to suit your application's requirements. 📜✨