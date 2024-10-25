# Documentation for `inactivity-charges-reminder.html` 📄

This document provides a comprehensive overview of the `inactivity-charges-reminder.html` template file. This HTML document is part of an email notification system intended to remind users about potential inactivity charges on their Ryvals account.

## Overview

The `inactivity-charges-reminder.html` is an HTML email template designed to notify users of impending inactivity charges due to lack of activity on their Ryvals account. It encourages users to engage with the platform to avoid such charges.

## Structure and Components

### HTML Structure

The HTML document follows the standard structure for an HTML email:

- **DOCTYPE Declaration**: Specifies HTML 1.0 Transitional as the document type.
- **HTML Element**: The main container for the email content.
- **Head Element**: Contains meta tags to ensure proper rendering and responsiveness across different email clients.
- **Body Element**: Contains the visual and textual content of the email.

### Key Sections

| Section           | Description                                                                                                               |
|-------------------|---------------------------------------------------------------------------------------------------------------------------|
| **Header**        | Displays the Ryvals logo and a banner image.                                                                              |
| **Greeting**      | Personalizes the email with the user's name.                                                                              |
| **Main Content**  | Informs the user of their account inactivity and the associated inactivity charges.                                       |
| **Note Section**  | Provides additional details about the inactivity charges policy.                                                          |
| **Footer**        | Contains a thank you message, Ryvals brand mention, and social media icons for engagement.                                |

### Template Variables

The template uses several Django template variables to personalize and adapt the content dynamically:

- `{{username}}`: Placeholder for the user's name.
- `{{last_enrollment_date}}`: The last activity date of the user.
- `{{inactivity_charges}}`: The amount charged as an inactivity fee.
- `{{inactivity_days}}`: Number of days after which the inactivity charge is applied.
- `{{img_path}}`: Directory path for loading images.

### Style and Presentation

The email is styled to maintain brand consistency with a dark theme (`#191919` background) and white text (`#fff`). It uses inline CSS for styling due to email client compatibility constraints.

- **Font**: Arial, used consistently across the email for a clean and professional look.
- **Color Scheme**: Dark background with white text, punctuated by blue links (`#009fc7`).
- **Images**: Logo and social media icons are included to reinforce brand identity.

### Responsiveness

The email is designed to be responsive, ensuring it displays correctly on various devices by using the `<meta name="viewport" content="width=device-width, initial-scale=1.0" />` tag.

## Usage

This template is intended to be used in a Django application where the email is rendered with context-specific data passed from the backend. It should be sent as part of a scheduled task or trigger when a user approaches the inactivity threshold.

## Conclusion

The `inactivity-charges-reminder.html` file is a crucial part of user engagement and retention strategy, reminding users of their inactivity in a visually appealing manner that aligns with the Ryvals brand. Proper utilization of this template can help reduce churn by encouraging users to return to the platform.

For any further questions or customization requests, please refer to the email design guidelines or contact the development team.