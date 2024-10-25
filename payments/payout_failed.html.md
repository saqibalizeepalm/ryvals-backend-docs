# Documentation for `payout_failed.html`

The `payout_failed.html` file is an HTML email template used to notify users about a failed payout attempt. This template is designed to provide users with essential information regarding the failed transaction and offers guidance on what steps to take next. Below is a detailed breakdown of the structure and elements within this template.

## Table of Contents
1. [HTML Structure](#html-structure)
2. [Template Variables](#template-variables)
3. [Styling and Layout](#styling-and-layout)
4. [Usage](#usage)

---

## HTML Structure

The HTML structure of the `payout_failed.html` template is defined using standard HTML5 elements. The layout is primarily composed of nested tables to ensure compatibility across various email clients, which often have limited CSS support.

```html
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
                <!-- Main email container -->
                <table bgcolor="#f5faf5" width="600" border="0" align="center" cellpadding="0" cellspacing="0">
                    <tr>
                        <!-- Header with logo -->
                        <td height="89" style="background-image: url('{{ request.scheme }}://{{request.get_host}}/static/images/banner.png'); background-repeat: no-repeat; background-size: cover; background-color: #191919;">
                            <img src="{{ request.scheme }}://{{ request.get_host }}{% static 'images/ryvals.png' %}" style="display:block; margin:auto; width:150px; height:38px;" />
                        </td>
                    </tr>
                    <!-- Body content -->
                    <tr>
                        <td width="600">
                            <!-- Greeting -->
                            <table width="600" bgcolor="#191919" border="0" align="center" cellpadding="0" cellspacing="0">
                                <tr>
                                    <td height="31"></td>
                                </tr>
                                <tr>
                                    <td width="27"></td>
                                    <td width="516" style="font-family: Arial; font-size: 18px; font-weight: bold; color: #fff;">Dear {{username}},</td>
                                    <td width="57"></td>
                                </tr>
                            </table>
                            <!-- Payout failed message -->
                            <table width="600" bgcolor="#191919" border="0" align="center" cellpadding="0" cellspacing="0">
                                <tr>
                                    <td width="27"></td>
                                    <td width="516" style="font-family: Arial; font-size: 16px; color: #fff;">{{type}} payout of ${{amount}} failed on {{date}}.</td>
                                    <td width="57"></td>
                                </tr>
                            </table>
                            <!-- Contact information -->
                            <table width="600" bgcolor="#191919" border="0" align="center" cellpadding="0" cellspacing="0">
                                <tr>
                                    <td width="27"></td>
                                    <td width="516" style="font-family: Arial; font-size: 16px; color: #fff;">If this wasn't you or if you need further assistance, please contact us at <a href="mailto:support@ryvals.com" style="color:#009fc7; text-decoration:none;">support@ryvals.com</a>.</td>
                                    <td width="57"></td>
                                </tr>
                            </table>
                            <!-- Closing -->
                            <table width="600" bgcolor="#191919" border="0" align="center" cellpadding="0" cellspacing="0">
                                <tr>
                                    <td width="27"></td>
                                    <td width="516" style="font-family: Arial; font-size: 16px; color: #fff;">Thank you,</td>
                                    <td width="57"></td>
                                </tr>
                            </table>
                            <!-- Footer -->
                            <table width="600" bgcolor="#191919" border="0" align="center" cellpadding="0" cellspacing="0">
                                <tr>
                                    <td width="27"></td>
                                    <td width="516" style="font-family: Arial; font-size: 16px; color: #fff;">Ryvals</td>
                                    <td width="57"></td>
                                </tr>
                            </table>
                        </td>
                    </tr>
                    <tr height="356"></tr>
                    <!-- Social media icons -->
                    <tr width="600">
                        <td width="600">
                            <table width="600" bgcolor="#141414" border="0" align="center" cellpadding="0" cellspacing="0">
                                <tr height="16"></tr>
                                <tr>
                                    <td width="33"></td>
                                    <td width="170" style="opacity: 0.69; font-family: Arial; font-size: 10px; color: #fff;">© 2023 RYVALS. All Rights Reserved.</td>
                                    <td width="226"></td>
                                    <td><img src="{{ request.scheme }}://{{ request.get_host }}{% static 'images/template-twitter.png' %}" style="width:14px; height:11px" /></td>
                                    <td width="15"></td>
                                    <td><img src="{{ request.scheme }}://{{ request.get_host }}{% static 'images/template-facebook.png' %}" style="width:7px; height:14px" /></td>
                                    <td width="15"></td>
                                    <td><img src="{{ request.scheme }}://{{ request.get_host }}{% static 'images/template-instagram.png' %}" style="width:14px; height:14px" /></td>
                                    <td width="15"></td>
                                    <td><img src="{{ request.scheme }}://{{ request.get_host }}{% static 'images/template-youtube.png' %}" style="width:14px; height:14px" /></td>
                                    <td width="15"></td>
                                    <td><img src="{{ request.scheme }}://{{ request.get_host }}{% static 'images/template-hangouts.png' %}" style="width:14px; height:14px" /></td>
                                    <td width="15"></td>
                                    <td><img src="{{ request.scheme }}://{{ request.get_host }}{% static 'images/template-twoi.png' %}" style="width:14px; height:14px" /></td>
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
</body>
</html>
```

## Template Variables

The template utilizes several dynamic variables that are filled in with user-specific data when the email is generated:

- **{{username}}**: The username of the recipient.
- **{{type}}**: The type of payout (e.g., "Instant" or "Standard").
- **{{amount}}**: The amount of money that was attempted to be paid out.
- **{{date}}**: The date when the payout was attempted and failed.

## Styling and Layout

- The email is styled with a dark theme using background colors `#191919` and `#141414` for the main content and footer, respectively.
- Text is displayed using the Arial font, with white text color (`#fff`) for contrast against the dark background.
- Social media icons are included at the bottom, providing links to Ryvals' social media pages.

## Usage

This template is typically used by the system to inform users about a failed payout. It provides necessary details on the transaction and encourages users to contact support if the transaction was not initiated by them or if they require further assistance. This email helps maintain transparency and trust by notifying users of errors in financial transactions promptly.

The template employs Django's template language, allowing dynamic content to be inserted into the email based on server-side data. The use of Django's `static` template tag allows for the inclusion of static files like images, ensuring that brand elements such as the company logo and social media icons are displayed correctly.