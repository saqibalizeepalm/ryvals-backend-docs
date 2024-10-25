# Documentation for **monthly-enrollment-reminder.html**

## Overview

The `monthly-enrollment-reminder.html` file is a Django template used for sending monthly reminders via email to users whose accounts have been inactive for a specified period. The template is crafted to alert users about potential inactivity charges if they do not engage with the Ryvals platform.

## HTML Structure

### DOCTYPE and HTML Tag
- The document is declared as an XHTML 1.0 Transitional type, ensuring compatibility with older browsers while still maintaining support for more modern features.
- The HTML tag specifies the XML namespace.

### Head Section
- **Meta Tags**:
  - `Content-Type`: Sets the character encoding to UTF-8.
  - `Viewport`: Configured for responsive design, allowing the content to adjust to different screen sizes.

### Body Section
- The body consists of a centered table that acts as the main container for the email's content.
- The email content is divided into several sections using nested tables, each with a specific purpose.

### Main Content Areas

#### Header
- **Banner Image**: Displays a banner image with the Ryvals logo centered. The background includes a custom banner image specified by the `img_path` variable.

#### Greeting
- Personalized greeting using the variable `{{username}}` to address the recipient.

#### Inactivity Notification
- Informs the user about their account's inactivity since the last recorded enrollment date (`{{last_enrollment_date}}`).
- Encourages the user to enroll in a Ryvals' lobby to avoid inactivity fees.

#### Conditional Content
- Uses an `if` template tag to conditionally display additional content based on whether the user has enrolled:
  - **Enrollment Prompt**: If the user is not enrolled, a prompt to enroll is displayed.
  - **Signup Date**: If the user is enrolled, the signup date is shown.

#### Inactivity Fee Note
- Clearly states the monthly inactivity fee (`${{inactivity_charges}}/mo`) and the conditions under which it applies, i.e., if the account has been inactive for more than `{{inactivity_days}}` days.

#### Footer
- **Thank You Note**: A polite closing thanking the user.
- **Company Signature**: The company name, Ryvals, is reiterated.

#### Social Media Links
- Icons for various social media platforms (Twitter, Facebook, Instagram, YouTube, Hangouts) are included, providing visual links to the Ryvals' social media pages.

#### Copyright
- A small footer note indicating that all rights are reserved by Ryvals, reflecting the year 2023.

## Styling

- The template employs inline CSS for styling, ensuring consistent appearance across email clients that may not support external stylesheets.
- It uses a dark theme with a black (#191919) background and white (#fff) text for a sleek and modern look.

## Variables and Localization

- **Template Variables**: Utilizes Django template variables such as `{{username}}`, `{{last_enrollment_date}}`, `{{inactivity_charges}}`, and `{{inactivity_days}}` to dynamically insert user-specific data.
- **Translation**: The template is prepared for translation with `{% load i18n %}` and uses `{% autoescape off %}` for safe HTML rendering.

## Use Case

This email template is particularly useful for user engagement, serving as a gentle nudge for users to re-engage with the platform and avoid additional charges. It helps in maintaining an active user base and reducing customer churn.

### How It Works

1. **Trigger**: This template is triggered as part of a scheduled task that checks for inactive accounts.
2. **Dynamic Content**: Variables are populated with the respective user's data before the email is dispatched.
3. **Localization Support**: Ready to support multiple languages to cater to a diverse user base.