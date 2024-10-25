# Documentation for `password_reset_email_import.html`

This document provides a detailed overview of the `password_reset_email_import.html` file, which is a part of your Django application. This file is primarily used for sending password reset emails to users who have imported accounts or pre-registered on the platform. The template is designed to deliver a visually appealing and responsive email.

## File Overview

- **File Type**: HTML Template
- **Purpose**: To create a password reset email specifically for users who have pre-registered or imported their accounts.

## Structure and Components

The email template is structured using HTML and styled with inline CSS to ensure compatibility across various email clients. Let's break down the components of this template:

### HTML Document Structure

- **DOCTYPE Declaration**: The template starts with the XHTML 1.0 Transitional doctype declaration, which ensures the document is rendered in standards-compliant mode.
  
- **HTML and Meta Tags**: The `<html>` tag specifies the XML namespace, and the `<head>` section contains meta tags for character set and viewport settings to ensure responsiveness.

### Inline CSS Styles

- **Responsive Design**: The template employs media queries to adjust styles for different screen sizes, ensuring a seamless experience on both desktop and mobile devices.
  
- **Styling Elements**: The CSS styles are defined for various elements such as tables, images, and text blocks. It includes styles for the wrapper, columns, links, and images to make the email aesthetically pleasing.

### Body Content

- **Wrapper Table**: The main content is wrapped within a table of width 100%, ensuring the email content is centered and fits within the email client window.

- **Background and Logos**: The email features a background image and two logos – one for "ryvals-ppk.png" and another for "ryvals-logo.png". These are displayed prominently at the top of the email.

- **Header and Call-to-Action**: A header message encourages users to play a new game mode, "PPK", and includes styled hashtags and a link to the Ryvals website.

- **Password Reset Note**: A notable section advises users about resetting their passwords if they have pre-registered. This is styled in italic for emphasis.

### Usage of Django Template Tags

- **Static Files**: `{% load static %}` is used to enable the inclusion of static images within the email, ensuring that paths to images are correctly resolved.
  
- **Autoescape**: `{% autoescape off %}` is used to allow HTML content to be inserted without escaping, which is essential for rendering HTML correctly in emails.

## Key Features

- **Responsive Layout**: The design adapts to different screen sizes, enhancing user experience on mobile devices.
  
- **Brand Consistency**: The use of Ryvals logos and consistent brand colors (e.g., #009FC7) helps maintain brand identity.

- **Call-to-Action**: Encourages engagement by directing users to the website and promoting the Ryvals community through hashtags.

## Summary

The `password_reset_email_import.html` template is a well-structured and styled email template designed for informing users about password reset procedures, specifically targeting those with pre-registered accounts. It ensures that users are engaged with clear call-to-actions and maintains brand consistency throughout the design.