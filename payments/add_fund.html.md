# 📄 Documentation for `add-funds.html`

## Overview
The `add-funds.html` file is a Django HTML template that is used to generate an email notification for users when they successfully add funds to their Ryvals wallet. This template ensures that users receive confirmation of their transaction and provides them with details about their updated wallet balance. 

## HTML Structure
The template is structured to provide a clean and professional layout with a focus on user experience. Below is a breakdown of the key components and their functionalities:

### Meta Information
- **Charset and Viewport**: The document uses UTF-8 character encoding and is responsive to different screen sizes.

```html
<meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
```

### Header
- **Logo and Banner**: Displays the Ryvals logo centered within a header banner. The banner is styled with a background image.

```html
<td height="89" style="background-image: url('{{ request.scheme }}://{{request.get_host}}/static/images/banner.png'); ...">
    <img src="{{ request.scheme }}://{{ request.get_host }}{% static 'images/ryvals.png' %}" style="display:block; margin:auto; ..."/>
</td>
```

### Content Body
- **Greeting**: Begins with a personalized greeting using the user's username.

```html
<td width="516" style="...; color: #fff;">Dear {{username}}</td>
```

- **Transaction Details**: Informs the user about the successful addition of funds and provides the updated wallet balance with a timestamp.

```html
<td width="516" style="...; color: #fff;">You have successfully added ${{amount}} to your Ryvals wallet on {{date}} ET. Your wallet balance now: ${{wallet_balance}}.</td>
```

- **Support Contact**: Provides a contact email for support in case the user did not authorize the transaction or requires further assistance.

```html
<td width="516" style="...; color: #fff;">If this wasn't you or if you need further assistance, please contact us at <a href="mailto:support@ryvals.com" style="color:#009fc7; text-decoration:none;">support@ryvals.com</a>.</td>
```

### Closing 
- **Sign-off**: A simple thank you note followed by the brand name.

```html
<td width="516" style="...; color: #fff;">Thank you,</td>
...
<td width="516" style="...; color: #fff;">Ryvals</td>
```

### Footer
- **Social Media Icons**: Includes icons for various social media platforms to encourage users to connect with Ryvals on these platforms.

```html
<td><img src="{{ request.scheme }}://{{ request.get_host }}{% static 'images/template-twitter.png' %}" style="width:14px; height:11px" /></td>
...
<td><img src="{{ request.scheme }}://{{ request.get_host }}{% static 'images/template-twoi.png' %}" style="width:14px; height:14px" /></td>
```

- **Copyright Notice**: Displays a copyright statement.

```html
<td width="170" style="...; color: #fff;">© 2023 RYVALS. All Rights Reserved.</td>
```

## Key Features
- **Personalization**: Uses Django template variables to personalize the email content with user-specific details like username, amount added, date, and wallet balance.
- **Responsive Design**: Ensures that the email displays correctly across different devices and email clients.
- **Security**: Uses Django's `static` template tag to load static files securely.

## Template Tags and Variables
- **`{% load static %}`**: Used to load static files within the template.
- **`{{username}}`, `{{amount}}`, `{{date}}`, `{{wallet_balance}}`**: Template variables to dynamically insert user and transaction data.

## Conclusion
The `add-funds.html` template is a crucial component for user communication, providing confirmation and details about transactions in a user-friendly and visually appealing format. By leveraging Django's templating system, it ensures that emails are both dynamic and consistent with the Ryvals brand.