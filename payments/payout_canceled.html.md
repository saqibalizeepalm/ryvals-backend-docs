# Documentation for `payout_canceled.html`

## Overview

The `payout_canceled.html` file is an HTML email template used to inform users about the cancellation of a payout. This email provides the details of the payout and offers guidance on what to do if the transaction was unauthorized or if further assistance is needed. This document provides an overview of the structure, styling, and dynamic content of the template.

### Structure

The template follows a standard HTML structure with a `<table>` layout commonly used in email templates to ensure consistent rendering across different email clients.

### Dynamic Content

Several placeholders are used to insert dynamic content into the template, allowing for personalized communication with the user.

- **`{{username}}`**: This placeholder is replaced with the user's name to personalize the email.
- **`{{type}}`**: Indicates the type of payout (e.g., instant or standard).
- **`{{amount}}`**: Displays the amount of the payout that was canceled.
- **`{{date}}`**: Shows the date when the payout was canceled.

### Static Assets

- **Logo and Banner**: The email includes a banner and a Ryvals logo for branding consistency, using images hosted on the server.
  - **Logo**: Displayed at the top of the email with dimensions specified for consistency.
  - **Banner**: A background image that enhances the visual appeal of the header section.

### Styling

The template uses inline CSS, which is a common practice for email templates to ensure styles are applied consistently across different email clients. Key styling elements include:

- **Font**: Arial is used for its readability and broad compatibility.
- **Colors**: A dark theme with white text (`#fff`) on a dark background (`#191919`) is used for modern aesthetics.
- **Spacing**: Padding and margins are applied to table cells to ensure proper spacing and layout.

### Social Media Icons

The footer contains icons linking to various social media platforms, enhancing the Ryvals brand's presence and engagement.

- **Icons included**: Twitter, Facebook, Instagram, YouTube, Hangouts, and an additional icon.
- **Styling**: Each icon is displayed with a fixed size to ensure uniformity.

### Footer

The footer section includes a copyright notice indicating ownership by Ryvals and the current year, enhancing the legitimacy and professionalism of the communication.

## Code Example

Below is a snippet of the HTML structure showcasing the dynamic elements:

```html
<tr>
  <td width="27"></td>
  <td width="516" style="font-family: Arial; font-size: 18px; font-weight: bold; color: #fff;">
    Dear {{username}},
  </td>
  <td width="57"></td>
</tr>
<tr>
  <td width="27"></td>
  <td width="516" style="font-family: Arial; font-size: 16px; color: #fff;">
    {{type}} payout of ${{amount}} cancelled on {{date}}.
  </td>
  <td width="57"></td>
</tr>
```

### Usage

This email template is triggered within the Ryvals payment system when a payout is canceled. It ensures that users are promptly informed of changes to their account, maintaining transparency and trust.

### Legal Notice

The footer includes a legal notice to protect the brand's intellectual property and ensure users are aware of the terms associated with the email content.

## Conclusion

The `payout_canceled.html` template is a crucial component of the Ryvals payment notification system, delivering timely and personalized information to users about payout cancellations. Its consistent styling and dynamic content placeholders ensure clear communication and maintain the brand's professional image.