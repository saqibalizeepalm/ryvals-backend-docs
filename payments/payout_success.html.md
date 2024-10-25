# Documentation for `payout_success.html`

## Overview

The `payout_success.html` file is an HTML email template used to notify users about the successful completion of a payout transaction. This document provides a comprehensive breakdown of the structure, purpose, and key elements within the template.

## Table of Contents

1. [Purpose](#purpose)
2. [Structure](#structure)
3. [Template Variables](#template-variables)
4. [Static Resources](#static-resources)
5. [Contact Information](#contact-information)

## Purpose

The primary purpose of the `payout_success.html` template is to inform users when their payout request has been successfully processed. It includes essential details about the transaction and advises users to contact support if they did not initiate the payout.

## Structure

The HTML template is structured as follows:

- **DOCTYPE Declaration**: Specifies the document type and version.
- **HTML Tags**: The root element wrapping the entire content.
- **Head Section**: Contains metadata and viewport settings for responsive design.
- **Body Section**: Encloses the main content of the email.

### Main Sections

1. **Header**: Displays the Ryvals logo on a banner background.
2. **Greeting**: Personalized message addressing the user by their username.
3. **Transaction Details**: Information about the payout type, amount, and completion date.
4. **Support Information**: Contact details for user support.
5. **Footer**: Includes company information and links to social media.

## Template Variables

The template utilizes several Django template variables to dynamically populate user-specific and transaction-specific data:

- `{{username}}`: The user's name, used to personalize the greeting.
- `{{type}}`: The type of payout (e.g., "Instant" or "Standard").
- `{{amount}}`: The amount of money successfully paid out.
- `{{date}}`: The date when the transaction was completed.

## Static Resources

The template references several static resources for styling and branding:

- **Images**: 
  - Ryvals logo: Loaded from static files.
  - Social media icons: Links to Ryvals' social media pages.

The static paths are constructed using Django's `{% static %}` tag to ensure correct URLs are generated based on the application's host and scheme.

## Contact Information

The email provides a contact link for users who require assistance or did not initiate the payout:

- **Support Email**: `support@ryvals.com` is provided as a mailto link for easy access.

## Example Usage

Here is a hypothetical example of how the template might be rendered with context data in Django:

```django
context = {
    'username': 'John Doe',
    'type': 'Instant',
    'amount': '150.00',
    'date': '2023-02-15',
    'request': request,  # Passed to generate correct static URLs
}

rendered_email = render_to_string('payout_success.html', context)
```

This example would produce an email notifying the user "John Doe" of an instant payout of $150.00 on February 15, 2023.

## Conclusion

The `payout_success.html` template is a crucial component in maintaining effective communication with users regarding their financial transactions on the Ryvals platform. By ensuring the template is correctly populated and rendered, the company can enhance user trust and satisfaction.