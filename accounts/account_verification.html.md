# account_verification.html Documentation

This document provides a detailed description of the `account_verification.html` file, which is a Django HTML template used for sending account verification emails to users. This file is part of a Django web application and is responsible for rendering the content of the verification email sent to users upon registration or account verification requests.

## Overview

The `account_verification.html` file is an HTML email template that is rendered and sent to users for the purpose of account verification. It uses Django template tags and filters to dynamically insert user-specific data, such as their first name, last name, and a verification link. The template also incorporates some styling to ensure the email is visually appealing and consistent with the application's branding.

## Template Structure

The template follows HTML standards and includes the following key sections:

### HTML Document Structure

- **DOCTYPE Declaration**: The template begins with a DOCTYPE declaration for XHTML 1.0 Transitional, which specifies the document type and HTML version.
- **HTML Tag**: The root element of the HTML document, which contains all other elements.
- **Head Section**: Contains meta tags for character set and viewport settings. These ensure proper rendering on various devices.

### Body Content

The body of the email is structured using a series of nested HTML tables, which serve to layout the content in a structured manner. Key elements include:

- **Header Section**: 
  - Displays the Ryvals logo and a background image.
  - The logo is loaded using the Django `{% static %}` tag to ensure correct file path resolution.

- **Greeting Section**: 
  - Includes a personalized greeting using the recipient's first name and last name.

- **Verification Instructions**: 
  - Provides instructions for the user, including a verification link.
  - The content varies slightly depending on whether the email is a resend or an initial registration confirmation.

- **Verification Link**: 
  - A clickable link for the user to verify their account.
  - The link is styled to match the application's branding.

- **Contact Information**: 
  - Offers a contact email for additional support.

- **Footer Section**: 
  - Displays copyright information.
  - Includes social media icons with links for user engagement.

## Dynamic Content

The template uses Django template tags to insert dynamic content:

- **`{{ first_name }}` and `{{ last_name }}`**: User's first and last name.
- **`{{ verification_link }}`**: The URL for account verification.
- **`{{ request.scheme }}` and `{{ request.get_host }}`**: Used for constructing absolute URLs for images and links.

## Styles and Branding

- The email template uses inline CSS for styling. This is necessary for compatibility with various email clients, many of which strip out or do not support external stylesheets.
- The color scheme and fonts are consistent with Ryvals' branding, providing a professional and cohesive appearance.

## Usage

This file is typically used in conjunction with Django's email sending functionality. When a user registers on the platform, the application generates a verification link and uses this template to send an email containing the link to the user's email address.

## Conclusion

The `account_verification.html` file is an essential part of the user registration and verification process in the Django application. It ensures that communication with users is both functional and aesthetically aligned with the brand's identity. The use of Django template tags allows for the dynamic insertion of user-specific information, making the emails personalized and relevant.