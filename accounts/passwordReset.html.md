# Documentation for `password_reset_email.html`

This HTML file is a template used for sending password reset emails to users of the Ryvals application. It is designed to provide a user-friendly and secure method for users to reset their passwords when requested. The email informs the user about the password reset request and provides a link to facilitate the process. Below is a detailed breakdown of the file and its components.

## File Structure

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
                                                <td width="516" style=" font-family: Arial; font-size: 16px; font-weight: normal; font-stretch: normal; font-style: normal; line-height: 1.5; letter-spacing: normal; color: #fff;">We received a password reset request for your account. To reset your password, please click on the link provided below. Please note this link is only valid for 15 minutes.</td>
                                                <td width="57"></td>
                                            </tr>
                                        </table>
                                    </td>
                                </tr>
                                {% block reset_link %}
                                <tr height="20"></tr>
                                <tr width="600">
                                    <td width="600">
                                        <table width="600" bgcolor="#191919" border="0" align="center" cellpadding="0" cellspacing="0">
                                            <tr>
                                                <td width="27"></td>
                                                <td width="516" style=" font-family: Arial; font-size: 16px; font-weight: normal; font-stretch: normal; font-style: normal; line-height: 1.5; letter-spacing: normal; color: #009fc7;"><a href="{{changepassword_link}}" style="color:#009fc7; text-decoration: none;">Click here to enter new password</a></td>
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
                                                <td width="516" style=" font-family: Arial; font-size: 16px; font-weight: normal; font-stretch: normal; font-style: normal; line-height: 1.5; letter-spacing: normal; color: #ffffff;">Or</td>
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
                                                <td width="516" style=" font-family: Arial; font-size: 16px; font-weight: normal; font-stretch: normal; font-style: normal; line-height: 1.5; letter-spacing: normal; color: #009fc7; "><a href="{{changepassword_link}}" style="color:#009fc7; text-decoration: none;">{{changepassword_link}}</a></td>
                                                <td width="57"></td>
                                            </tr>
                                        </table>
                                    </td>
                                </tr>
                                {% endblock %}
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

## Key Components

1. **Structure and Styling**:
    - The email is designed to be responsive, utilizing tables for layout which is common in email design.
    - The background and text colors are chosen to fit the Ryvals branding, with a dark theme and highlights in blue.

2. **Content Blocks**:
    - **Header**: Displays the Ryvals logo and a background banner.
    - **Greeting**: Personalizes the email with the user's first and last names.
    - **Message Body**: Informs the user of the password reset request and contains a link to reset the password.
    - **Reset Link**: The link is provided twice; once as a clickable text and once as the full URL for manual entry.
    - **Contact Information**: Provides the support email for assistance if the user did not initiate the request.

3. **Dynamic Content**:
    - Uses Django's template language to dynamically insert user-specific information such as `first_name`, `last_name`, and `changepassword_link`.

4. **Security Considerations**:
    - The password reset link is valid for only 15 minutes to enhance security.

5. **Footer**:
    - Contains social media icons and a copyright notice, reinforcing the brand.

## Usage

This template is used in conjunction with Django's email sending functionalities. When a user requests a password reset, this template is rendered with the appropriate context (user details and reset link) and sent to the user's email.

## Conclusion

The `password_reset_email.html` template is a crucial part of user account security, providing a seamless and secure method for users to reset their passwords. Its design and content ensure that users are well-informed and guided through the process easily.