# Documentation for `redeem-balance.html`

This document provides an overview and detailed explanation of the `redeem-balance.html` file. This file is an HTML email template used to notify users about the successful redemption of funds from their Ryvals wallet through PayPal.

## Overview

The `redeem-balance.html` file is an HTML template designed for sending automated email notifications to users. The email informs users when they have successfully redeemed a specific amount from their Ryvals wallet using PayPal. The template is styled with a consistent format and includes placeholders for dynamic content such as the username, amount, and date.

## Structure and Content

The template uses Django's template language for dynamic content rendering, which includes:

- **Static file loading**: Utilizes `{% load static %}` to manage static files like images.
- **HTML Document Structure**: A standard HTML structure with a head and body section.
- **Table Layout**: Uses tables to ensure the email renders correctly across different email clients.
- **Dynamic Content**: Placeholders for user-specific details.

### HTML Template Breakdown

#### Head Section

```html
<head>
    <meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
</head>
```

- **Meta Tags**: Define character encoding as UTF-8 and ensure the email is responsive on mobile devices.

#### Body Section

The body section is primarily a table structure, ensuring compatibility across various email clients.

1. **Wrapper Table**

   - Contains the overall layout and structure of the email content.
   - Sets the background and dimensions.

2. **Header Section**

   - Displays the Ryvals logo and possibly a banner image.
   - Uses placeholders for the path to static images.

   ```html
   <td height="89" style="background-image: url('{{img_path}}banner.png'); ...;">
       <img src="{{img_path}}ryvals.png" style="display:block; margin:auto; width:150px; height:38px;" />
   </td>
   ```

3. **Content Section**

   - **Greeting**: Personalized greeting using the `{{username}}` placeholder.
   
   ```html
   <td width="516" style="...; color: #fff;">Dear {{username}},</td>
   ```

   - **Redemption Confirmation**: Provides details of the successful redemption amount and date.

   ```html
   <td width="516" style="...; color: #fff;">
       You have successfully redeemed ${{amount}} from your Ryvals wallet on {{date}} using paypal.
   </td>
   ```

   - **Assistance**: Instructions for contacting support if the transaction wasn't initiated by the user.

   ```html
   <td width="516" style="...; color: #fff;">
       If this wasn't you or if you need further assistance, please contact us at <a href="mailto:support@ryvals.com" ...>support@ryvals.com</a>.
   </td>
   ```

4. **Footer Section**

   - **Closing and Signature**: Thanking the user and signed by Ryvals.

   ```html
   <td width="516" style="...; color: #fff;">Thank you,</td>
   <td width="516" style="...; color: #fff;">Ryvals</td>
   ```

   - **Social Media Links**: Icons linking to Ryvals' social media pages.

   ```html
   <td><img src="{{img_path}}template-twitter.png" style="width:14px; height:11px" /></td>
   ```

5. **Legal and Copyright**

   ```html
   <td width="170" style="...; color: #fff;">© 2023 RYVALS. All Rights Reserved.</td>
   ```

## Usage

- **Placeholders**: The template uses Django's templating system to replace placeholders such as `{{username}}`, `{{amount}}`, and `{{date}}` with actual data before sending the email.
- **Static Content**: Images and other static content are managed via Django's static files system, ensuring consistency and ease of maintenance.

## Conclusion

The `redeem-balance.html` is a crucial component of the Ryvals system, providing a user-friendly and consistent notification mechanism for users redeeming funds. The careful use of tables ensures that the email is displayed correctly across various email clients, maintaining a professional appearance and clear communication.