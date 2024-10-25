# Documentation for `redeem-instant-stripe.html`

This document serves as comprehensive documentation for the `redeem-instant-stripe.html` file, which is part of the Ryvals application. This HTML template is used for sending notifications to users when they have successfully redeemed funds from their Ryvals wallet to their Stripe account using an instant payout method.

## Overview

The `redeem-instant-stripe.html` is an HTML template designed to be sent as an email to users who have initiated an instant payout from their Ryvals wallet to their Stripe account. The email serves as a confirmation and notification regarding the transaction's success and provides details about the transaction.

## Structure

The email template is structured as follows:

1. **Header Section**: Contains the Ryvals logo and a visually appealing banner.
2. **Body Section**: Provides the main content of the email, including the transaction details.
3. **Footer Section**: Contains a disclaimer and Ryvals' social media icons.

## Detailed Breakdown

### HTML Template

```html
{% load static %}
<!DOCTYPE html>
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
                            <img src="{{ request.scheme }}://{{ request.get_host }}{% static 'images/ryvals.png' %}" style="display:block; margin:auto; width:150px; height:38px;" />
                        </td>
                    </tr>
                    <tr>
                        <td width="600">
                            <table width="600" bgcolor="#191919" border="0" align="center" cellpadding="0" cellspacing="0">
                                <tr>
                                    <td height="31"></td>
                                </tr>
                                <tr height="5"></tr>
                                <tr width="600">
                                    <td width="600">
                                        <table width="600" bgcolor="#191919" border="0" align="center" cellpadding="0" cellspacing="0">
                                            <tr>
                                                <td width="27"></td>
                                                <td width="516" style="font-family: Arial; font-size: 18px; font-weight: bold; color: #fff;">Dear {{username}},</td>
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
                                                <td width="27"> </td>
                                                <td width="516" style="font-family: Arial; font-size: 16px; color: #fff;">
                                                    You have successfully redeemed ${{amount}} from your Ryvals wallet to stripe account on {{date}} and your instant payout request will be processed in 30 minutes to 3 hours. Your wallet balance now: ${{wallet_balance}}.
                                                </td>
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
                                                <td width="516" style="font-family: Arial; font-size: 16px; color: #fff;">
                                                    If this wasn't you or if you need further assistance, please contact us at <a href="mailto:support@ryvals.com" style="color:#009fc7; text-decoration:none;">support@ryvals.com</a>.
                                                </td>
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
                                                <td width="516" style="font-family: Arial; font-size: 16px; color: #fff;">Thank you,</td>
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
                                                <td width="516" style="font-family: Arial; font-size: 16px; color: #fff;">Ryvals</td>
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
            </td>
        </tr>
    </table>
</body>
</html>
```

### Key Components

- **Header**: Displays the Ryvals logo and a banner image. The logo is centrally aligned and serves as a visual reinforcement of the brand.
- **Greeting**: The email starts with a personalized greeting addressing the user by their username.
- **Main Content**: This section informs the user about the successful redemption of funds and provides specific details about the transaction amount, the date, and the new wallet balance.
- **Assistance and Contact Information**: Provides a contact email for support in case the transaction wasn't initiated by the user or if they need further assistance.
- **Footer**: Reiterates the Ryvals brand and includes icons linking to social media pages, enhancing the brand's digital presence.

## Usage

This template is used within the Ryvals application to notify users of successful instant payout transactions through Stripe. The placeholders within the template (e.g., `{{username}}`, `{{amount}}`, `{{date}}`, `{{wallet_balance}}`) are dynamically populated with user-specific data when the email is sent.

## Conclusion

The `redeem-instant-stripe.html` template is a critical component in maintaining clear communication with users regarding financial transactions. It ensures that users are immediately informed about the status of their redeemed funds, providing transparency and fostering trust in the Ryvals platform.