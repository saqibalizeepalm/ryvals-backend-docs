# Documentation for `inactivity-charges-deducted.html`

This document provides a detailed overview of the `inactivity-charges-deducted.html` file, which is an HTML email template used to notify users about the deduction of inactivity charges from their Ryvals account.

## Overview

- **Purpose**: The HTML file serves as an email template notifying users about the deduction of inactivity fees due to prolonged inactivity in their Ryvals account.
- **Structure**: The template includes personalized messages, key details about inactivity, and links for re-engagement with the Ryvals platform.

## HTML Structure

The HTML file is structured to deliver a visually appealing and informative email. Below is a breakdown of its components:

### HTML and Meta Tags

```html
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
    <meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
</head>
```

- **DOCTYPE**: Specifies the HTML version, ensuring compatibility and proper rendering.
- **Meta Tags**: Define character encoding and viewport settings for responsiveness.

### Body and Main Table

```html
<body>
    <table width="100%">
        <tr>
            <td class="wrapper" width="600" align="center">
                <table bgcolor="#f5faf5" width="600" border="0" align="center" cellpadding="0" cellspacing="0">
```

- **Wrapper Table**: Centers the email content and sets a fixed width for consistent layout across different email clients.
- **Background Color**: Uses a light background color `#f5faf5` for the main table to ensure readability.

### Header Section

```html
<tr>
    <td height="89" style="background-image: url('{{img_path}}banner.png'); background-repeat: no-repeat; background-size: cover; background-color: #191919;">
        <img src="{{img_path}}ryvals.png" style="display:block; margin:auto; width:150px; height:38px;" />
    </td>
</tr>
```

- **Header Image**: Displays the Ryvals logo, ensuring brand recognition. The logo is centered with a dark background for contrast.

### Personalized Greeting

```html
<tr width="600">
    <td width="600">
        <table width="600" bgcolor="#191919" border="0" align="center" cellpadding="0" cellspacing="0">
            <tr>
                <td width="27"></td>
                <td width="516" style="font-family: Arial; font-size: 18px; font-weight: bold; color: #fff;">Dear {{username}}</td>
                <td width="57"></td>
            </tr>
        </table>
    </td>
</tr>
```

- **Greeting**: Addresses the user personally, using the `{{username}}` variable, to create a personalized experience.

### Message Body

```html
<td width="516" style="font-family: Arial; font-size: 16px; font-weight: normal; color: #fff;">
    Your Ryvals' account has been inactive for {{inactive_days_count}} days Last activity: {{last_enrollment_date}} ET. Your wallet has been debited a ${{inactivity_charges}} inactivity fee.
</td>
```

- **Inactivity Notification**: Informs the user about their inactivity period and the consequent deduction from their wallet.
- **Variables**: Utilizes template variables such as `{{inactive_days_count}}`, `{{last_enrollment_date}}`, and `{{inactivity_charges}}` to dynamically insert pertinent information.

### Call to Action

```html
<td width="516" style="font-family: Arial; font-size: 16px; font-weight: normal; color: #fff;">
    To avoid further deductions, click <a href="{{game_lobbies}}" style="color:#009fc7; text-decoration: none;">here</a> to enroll and play in a Ryvals' lobby.
</td>
```

- **Re-engagement Link**: Encourages users to visit the Ryvals game lobbies to prevent future inactivity charges. The link is styled in a contrasting color for visibility.

### Footer

```html
<td width="516" style="font-family: Arial; font-size: 16px; font-weight: normal; color: #fff;">Thank you,</td>
<td width="516" style="font-family: Arial; font-size: 16px; font-weight: normal; color: #fff;">Ryvals</td>
```

- **Closing Remarks**: Thanks the user and signs off with the Ryvals brand name.

### Social Media Icons

```html
<td><img src="{{img_path}}template-twitter.png" style="width:14px; height:11px" /></td>
```

- **Social Media**: Displays icons for various social media platforms, providing links to Ryvals’ social profiles to enhance engagement.

## Styling

- **Colors**: The template predominantly uses a dark theme (`#191919`) with white text (`#fff`), ensuring contrast and readability.
- **Font**: Arial is used consistently for a clean and professional look.
- **Responsive Design**: The template uses percentage widths and media settings for adaptability across devices.

## Conclusion

This email template is crucial for effectively communicating with users regarding inactivity charges while also encouraging re-engagement with the platform. By combining personalized messaging with clear calls to action and brand consistency, the template serves its purpose efficiently.