# Documentation for `username_reset_email.html`

This document provides detailed documentation for the `username_reset_email.html` file, which is part of the Django application for sending username recovery emails. This template is utilized when a user requests their forgotten username. The email is designed to be responsive and visually appealing.

## Overview

The `username_reset_email.html` file is a Django template used to generate an HTML email for users who have requested to recover their username. The email contains the user's username and instructions on what to do if they did not make this request.

## File Structure

Here is the structure of the template:

```html
{% load i18n %}
{% autoescape off %}
{% load static %}
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
    <meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
</head>
<body>
    <table width="100%">
        <tr>
            <td class="wrapper" width="600" align="center">
                <table bgcolor="#f5faf5" width="600" border="0" align="center" cellpadding="0" cellspacing="0">
                    <tr>
                        <td height="89" style="background-image: url('{{ request.scheme }}://{{request.get_host}}/static/images/banner.png'); background-repeat: no-repeat; background-size: cover; background-color: #191919;">
                            <img src="{{ request.scheme }}://{{request.get_host}}{% static 'images/ryvals.png' %}" style="display:block; margin:auto; width:150px; height:38px;" />
                        </td>
                    </tr>
                    <tr>
                        <td width="600">
                            <table width="600" bgcolor="#191919" border="0" align="center" cellpadding="0" cellspacing="0">
                                <tr>
                                    <td height="31"></td>
                                </tr>
                                <tr width="600">
                                    <td width="600">
                                        <table width="600" bgcolor="#191919" border="0" align="center" cellpadding="0" cellspacing="0">
                                            <tr>
                                                <td width="27"></td>
                                                <td width="516" style="font-family: Arial; font-size: 18px; font-weight: bold; font-stretch: normal; font-style: normal; line-height: 1.89; letter-spacing: normal; color: #fff;">Dear {{first_name}} {{last_name}}</td>
                                                <td width="57"></td>
                                            </tr>
                                        </table>
                                    </td>
                                </tr>
                                <tr height="20"></tr>
                                <tr width="600">
                                    <td width="600">
                                        <table width="600" bgcolor="#191919" border="0" align="center" cellpadding="0" cellspacing="0">
                                            <tr>
                                                <td width="27"> </td>
                                                <td width="516" style=" font-family: Arial; font-size: 16px; font-weight: normal; font-stretch: normal; font-style: normal; line-height: 1.5; letter-spacing: normal; color: #fff;">We received a request that you forgot your username.</td>
                                                <td width="57"></td>
                                            </tr>
                                        </table>
                                    </td>
                                </tr>
                                {% block reset_link %}
                                {% endblock %}
                                <tr height="20"></tr>
                                <tr width="600">
                                    <td width="600">
                                        <table width="600" bgcolor="#191919" border="0" align="center" cellpadding="0" cellspacing="0">
                                            <tr>
                                                <td width="27"></td>
                                                <td width="516" style=" font-family: Arial; font-size: 16px; font-weight: normal; font-stretch: normal; font-style: normal; line-height: 1.5; letter-spacing: normal; color: #ffffff;"><b>{{username}}</b> is your username to login.</td>
                                                <td width="57"></td>
                                            </tr>
                                        </table>
                                    </td>
                                </tr>
                                <tr height="20"></tr>
                                <tr width="600">
                                    <td width="600">
                                        <table width="600" bgcolor="#191919" border="0" align="center" cellpadding="0" cellspacing="0">
                                            <tr>
                                                <td width="27"></td>
                                                <td width="516" style=" font-family: Arial; font-size: 16px; font-weight: normal; font-stretch: normal; font-style: normal; line-height: 1.5; letter-spacing: normal; color: #fff;">If you did not make this request, please contact <a href="mailto:support@ryvals.com" style="color:#009fc7; text-decoration:none;">support@ryvals.com</a> immediately.</td>
                                                <td width="57"></td>
                                            </tr>
                                        </table>
                                    </td>
                                </tr>
                                <tr height="20"></tr>
                                <tr width="600">
                                    <td width="600">
                                        <table width="600" bgcolor="#191919" border="0" align="center" cellpadding="0" cellspacing="0">
                                            <tr>
                                                <td width="27"></td>
                                                <td width="516" style=" font-family: Arial; font-size: 16px; font-weight: normal; font-stretch: normal; font-style: normal; line-height: 1.5; letter-spacing: normal; color: #fff;">Thank you,</td>
                                                <td width="57"></td>
                                            </tr>
                                        </table>
                                    </td>
                                </tr>
                                <tr height="5"></tr>
                                <tr width="600">
                                    <td width="600">
                                        <table width="600" bgcolor="#191919" border="0" align="center" cellpadding="0" cellspacing="0">
                                            <tr>
                                                <td width="27"></td>
                                                <td width="516" style=" font-family: Arial; font-size: 16px; font-weight: normal; font-stretch: normal; font-style: normal; line-height: 1.5; letter-spacing: normal; color: #fff;">Ryvals</td>
                                                <td width="57"></td>
                                            </tr>
                                        </table>
                                    </td>
                                </tr>
                                <tr height="356"></tr>
                                <tr width="600">
                                    <td width="600">
                                        <table width="600" bgcolor="#141414" border="0" align="center" cellpadding="0" cellspacing="0">
                                            <tr height="16"></tr>
                                            <tr>
                                                <td width="33"></td>
                                                <td width="170" style=" opacity: 0.69; font-family: Arial; font-size: 10px; font-weight: normal; font-stretch: normal; font-style: normal; line-height: normal; letter-spacing: normal; color: #fff;">© 2023 RYVALS. All Rights Reserved.</td>
                                                <td width="226"></td>
                                                <td><img src="{{ request.scheme }}://{{request.get_host}}{% static 'images/template-twitter.png' %}" style="width:14px; height:11px" /></td>
                                                <td width="15"></td>
                                                <td><img src="{{ request.scheme }}://{{request.get_host}}{% static 'images/template-facebook.png' %}" style="width:7px; height:14px" /></td>
                                                <td width="15"></td>
                                                <td><img src="{{ request.scheme }}://{{request.get_host}}{% static 'images/template-instagram.png' %}" style="width:14px; height:14px" /></td>
                                                <td width="15"></td>
                                                <td><img src="{{ request.scheme }}://{{request.get_host}}{% static 'images/template-youtube.png' %}" style="width:14px; height:14px" /></td>
                                                <td width="15"></td>
                                                <td><img src="{{ request.scheme }}://{{request.get_host}}{% static 'images/template-hangouts.png' %}" style="width:14px; height:14px" /></td>
                                                <td width="15"></td>
                                                <td><img src="{{ request.scheme }}://{{request.get_host}}{% static 'images/template-twoi.png' %}" style="width:14px; height:14px" /></td>
                                                <td width="16"></td>
                                            </tr>
                                            <tr height="16"></tr>
                                        </table>
                                    </td>
                                </tr>
                            </table>
                        </td>
                    </tr>
                </table>
            </td>
        </tr>
    </table>
</body>
</html>
{% endautoescape %}
```

### Key Elements

- **Meta Information**: The template starts with meta tags to set the character set and viewport for mobile responsiveness.

- **Static and Dynamic Content**: 
  - Utilizes Django's `{% load static %}` and `{% load i18n %}` template tags to handle static content and translations.
  - Incorporates dynamic content using Django template variables such as `{{first_name}}`, `{{last_name}}`, and `{{username}}`.

- **Styling**: 
  - Inline CSS is used for styling the email. The background color and text color are set to maintain a consistent look with the Ryvals branding.
  - Uses `Arial` font, ensuring a clean and professional appearance.

- **Email Content**:
  - Begins with a greeting addressing the user by their first and last name.
  - States the purpose of the email, confirming a request for a forgotten username.
  - Displays the user's username prominently.
  - Provides a contact email for Ryvals support in case the user did not make the request.

- **Footer**: 
  - Includes social media icons linking to Ryvals' social media pages (Twitter, Facebook, Instagram, YouTube, Hangouts, etc.).
  - Displays a copyright notice.

### Usage

- **Purpose**: This template is specifically used for sending emails to users who have forgotten their username. It assists in account recovery by reminding users of their login credentials.

- **Integration**: It is integrated with Django's email sending mechanism and relies on context data provided by the Django views to populate dynamic content.

### Customization

- To change the branding or styling, update the inline CSS or replace the images with new assets.
- To add additional information or modify the existing text, update the HTML content inside the `<body>` tag.

### Conclusion

The `username_reset_email.html` template is a vital component of the user account management system within the Ryvals application. It ensures that users have a seamless experience in recovering their account credentials, maintaining user engagement and satisfaction.