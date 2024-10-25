# Country Data JSON Documentation

This document provides a detailed explanation of the `country_data.json` file, which stores information about various countries. This JSON file is used in applications to manage and retrieve data regarding countries, their codes, geographical locations, and other relevant details. The data is structured in a way to support applications that need geographic and demographic information for different purposes.

## Table of Contents
- [File Structure](#file-structure)
- [Fields Description](#fields-description)
- [Usage](#usage)
- [Example](#example)

## File Structure

The `country_data.json` file is structured as a list of dictionaries, where each dictionary represents a country. The fields within each dictionary provide specific details about the country.

```json
[
    {
        "model": "cities_light.country",
        "pk": 1,
        "fields": {
            "name": "Andorra",
            "name_ascii": "Andorra",
            "slug": "andorra",
            "geoname_id": 3041565,
            "alternate_names": "Principality of Andorra",
            "code2": "AD",
            "code3": "AND",
            "continent": "EU",
            "tld": "ad",
            "phone": "376"
        }
    },
    ...
]
```

## Fields Description

Here is a detailed description of each field in the JSON file:

| Field             | Description                                                                 |
|-------------------|-----------------------------------------------------------------------------|
| **model**         | The model name under which the country data is stored, e.g., `cities_light.country`. |
| **pk**            | The primary key for the country entry, used for identification. |
| **fields**        | A nested dictionary containing detailed information about the country. |
| **name**          | The full name of the country.                                               |
| **name_ascii**    | The ASCII version of the country name, without special characters.          |
| **slug**          | A URL-friendly version of the country name, used for slugs in URLs.         |
| **geoname_id**    | The GeoNames database ID for the country, useful for geographic applications. |
| **alternate_names** | Other names or descriptions the country is known by.                       |
| **code2**         | The ISO 3166-1 alpha-2 code of the country.                                 |
| **code3**         | The ISO 3166-1 alpha-3 code of the country.                                 |
| **continent**     | The continent code (e.g., EU for Europe, AS for Asia) where the country is located. |
| **tld**           | The top-level domain (TLD) associated with the country.                     |
| **phone**         | The international dialing code for the country.                             |

## Usage

This JSON file is used to provide a comprehensive set of data for each country that can be utilized in applications requiring geographic information. It can be loaded into databases or used directly by applications to provide country-specific services, such as determining phone number formats, displaying country-specific information, and supporting internationalization.

## Example

Here is a sample entry from the `country_data.json` file:

```json
{
    "model": "cities_light.country",
    "pk": 1,
    "fields": {
        "name": "Andorra",
        "name_ascii": "Andorra",
        "slug": "andorra",
        "geoname_id": 3041565,
        "alternate_names": "Principality of Andorra",
        "code2": "AD",
        "code3": "AND",
        "continent": "EU",
        "tld": "ad",
        "phone": "376"
    }
}
```

In this example, the entry provides detailed information about the country Andorra, including its codes, geographic identifiers, and more. This data can be used in various contexts, such as mapping applications, data analysis, and more.