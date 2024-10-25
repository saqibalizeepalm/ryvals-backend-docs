# 📜 Documentation for `models.py` File

The `models.py` file is an integral part of the Django application, serving as the backbone for the database structure of the app. This file defines the models, which are essentially Python classes that Django uses to create and manipulate database tables. In this specific file, we focus on models related to payment gateways and their association with countries.

## Table of Contents
1. [Overview](#overview)
2. [Models](#models)
   - [PaymentGateway](#paymentgateway)
   - [CountryPaymentGateway](#countrypaymentgateway)
3. [Usage](#usage)
4. [Meta Options](#meta-options)

---

## Overview

The `models.py` file contains the following two models:
- **PaymentGateway**: Represents different payment gateway options available within the system.
- **CountryPaymentGateway**: Establishes a relationship between payment gateways and countries, indicating which gateways are available in which countries.

These models utilize Django's ORM to handle database interactions seamlessly and provide a structured way to manage payment-related data.

## Models

### PaymentGateway

The `PaymentGateway` model is used to define different payment gateway options.

| **Field**        | **Type**   | **Description**                                            |
|------------------|------------|------------------------------------------------------------|
| `name`           | CharField  | The name of the payment gateway, maximum 100 characters.   |
| `slug`           | SlugField  | A short label for the payment gateway, used in URLs.       |
| `is_default`     | BooleanField | Indicates if this gateway is the default option.         |
| `responsible_class` | CharField | The class responsible for handling the payment logic.    |

#### Methods

- `__str__`: Returns a string representation of the model, which is the name of the payment gateway.

### CountryPaymentGateway

The `CountryPaymentGateway` model establishes a link between a country and a payment gateway.

| **Field**             | **Type**   | **Description**                                                |
|-----------------------|------------|----------------------------------------------------------------|
| `payment_gateway`     | ForeignKey | A foreign key to the `PaymentGateway` model.                   |
| `country`             | ForeignKey | A foreign key to the `Country` model from `cities_light`.      |

#### Methods

- `__str__`: Returns a string representation, showing the country name and the associated payment gateway name.

## Usage

These models are used to:
- Define available payment gateways and their configuration options.
- Specify which payment gateways are available in specific countries.

The `CountryPaymentGateway` model is particularly useful for applications that operate in multiple countries, allowing for localized payment options.

## Meta Options

Both models use the `Meta` class to specify metadata:

- **PaymentGateway Meta**:
  - `verbose_name_plural`: Sets the plural name as "Payment Gateways" for more readable administration interfaces.

- **CountryPaymentGateway Meta**:
  - `verbose_name_plural`: Sets the plural name as "Country - Payment Gateways", which helps in differentiating it in the admin interface.

---

These models form a crucial part of the payment processing framework within the application. By defining clear relationships and attributes, they ensure that payment operations can be conducted smoothly and efficiently across different regions. 🏦✨