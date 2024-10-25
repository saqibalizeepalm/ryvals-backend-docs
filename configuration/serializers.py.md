# 📄 `serializers.py` Documentation

Welcome to the documentation for the `serializers.py` file! This file is an integral part of a Django REST Framework (DRF) application. It handles the conversion of complex data types, like Django model instances, into native Python data types that can then be easily rendered into JSON or XML. Serializers also provide deserialization, allowing parsed data to be converted back into complex types, after first validating the incoming data.

### 📑 Index

1. [Introduction](#introduction)
2. [Dependencies](#dependencies)
3. [Serializer Classes](#serializer-classes)
   - [CountrySerializer](#countryserializer)
   - [RegionSerializer](#regionserializer)
   - [CitySerializer](#cityserializer)
4. [Usage](#usage)
5. [Conclusion](#conclusion)

---

## 🎉 Introduction

In Django REST Framework, serializers are used for defining the API representation. This file provides serializers for three models: `Country`, `Region`, and `City`. Each serializer specifies which fields to include in the API response and any additional methods or validation logic that is needed.

## 📦 Dependencies

```python
from rest_framework import serializers
from cities_light.models import (Country, Region, City)
```

- **Django REST Framework's `serializers`**: Provides a powerful mechanism to transform model instances into data types.
- **cities_light.models**: Imports `Country`, `Region`, and `City` models that are to be serialized.

## 📘 Serializer Classes

### 🌍 `CountrySerializer`

```python
class CountrySerializer(serializers.ModelSerializer):
    phone = serializers.SerializerMethodField('get_phone')

    def get_phone(self, obj):
        return f'+{obj.phone}'

    class Meta:
        model = Country
        fields = ['name', 'id', 'code2', 'phone']
```

- **Description**: This serializer converts the `Country` model into JSON format. It includes an additional custom field `phone` which is formatted with a '+' prefix.
- **Fields**:
  - `name`: Name of the country.
  - `id`: Unique identifier for the country.
  - `code2`: Two-letter country code.
  - `phone`: Custom field that formats the phone number with a '+'.

### 🌐 `RegionSerializer`

```python
class RegionSerializer(serializers.ModelSerializer):
    class Meta:
        model = Region
        fields = ['name', 'id']
```

- **Description**: This serializer converts the `Region` model into a JSON format.
- **Fields**:
  - `name`: Name of the region.
  - `id`: Unique identifier for the region.

### 🏙️ `CitySerializer`

```python
class CitySerializer(serializers.ModelSerializer):
    class Meta:
        model = City
        fields = ['name', 'id']
```

- **Description**: This serializer converts the `City` model into a JSON format.
- **Fields**:
  - `name`: Name of the city.
  - `id`: Unique identifier for the city.

## 🚀 Usage

To use these serializers, you can instantiate them with model instances or querysets and call methods to serialize or deserialize data. Here's a simple example:

```python
# Serializing a single instance
country_instance = Country.objects.get(id=1)
serializer = CountrySerializer(country_instance)
json_data = serializer.data  # This will be JSON-ready data

# Serializing a queryset
countries = Country.objects.all()
serializer = CountrySerializer(countries, many=True)
json_data = serializer.data  # This will be a list of JSON-ready data
```

## 🏁 Conclusion

The `serializers.py` file is a critical component for handling the representation of your data in a Django REST Framework application. By defining how `Country`, `Region`, and `City` models should be serialized, the file facilitates seamless data exchange between your server and clients.

These serializers make it easy to work with model data in API endpoints by transforming model instances into JSON and validating incoming data during creation or update operations. 🎉

Feel free to extend these serializers with additional methods or custom fields to suit your application's needs! 🌟