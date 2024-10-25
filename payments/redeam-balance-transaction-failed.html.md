# Documentation for `redeem-balance-transaction-fail.html`

This documentation provides an overview of the `redeem-balance-transaction-fail.html` template file used in the Ryvals application. This HTML template serves as a notification email to inform administrators when a PayPal payout transaction has failed. Below is a detailed explanation of the structure and purpose of each part of the template.

## Table of Contents
1. [Purpose](#purpose)
2. [File Structure](#file-structure)
3. [Components](#components)
4. [Template Variables](#template-variables)
5. [Styling](#styling)
6. [Utilities](#utilities)

## Purpose

The `redeem-balance-transaction-fail.html` file is an HTML template designed to notify administrators about a failed PayPal payout transaction. It outlines the transaction details such as the transaction number, username, amount, and date of the transaction. This email helps in promptly addressing any issues with failed transactions.

## File Structure

The file is structured as an HTML document with embedded Django template tags. It is designed to be rendered server-side with specific transaction data and then sent as an email. The document adheres to the XHTML 1.0 Transitional standard.

## Components

### HTML Structure

- **Doctype and HTML Tags**: The document begins with the `<!DOCTYPE>` declaration for XHTML 1.0 Transitional, followed by the `<html>` tag with XML namespaces.

- **Head Section**: Contains meta tags for character set and viewport settings.

- **Body Section**: The main content of the email is structured using HTML tables for layout.

### Main Sections

1. **Header**: Includes a banner image and the Ryvals logo.
   ```html
   <td height="89" style="background-image: url('{{ request.scheme }}://{{request.get_host}}/static/images/banner.png'); ...">
       <img src="{{ request.scheme }}://{{ request.get_host }}{% static 'images/ryvals.png' %}" ... />
   </td>
   ```

2. **Greeting**: Begins with a salutation addressed to "Admin."
   ```html
   <td width="516" style="...">Hello Admin,</td>
   ```

3. **Transaction Details**: Displays the failed transaction information.
   - **Transaction Number**
   - **Username**
   - **Transaction Amount**
   - **Date of Transaction**

4. **Footer**: Concludes the email with a closing thank you and company name.
   ```html
   <td width="516" style="...">Thank you,</td>
   <td width="516" style="...">Ryvals</td>
   ```

5. **Social Media Icons**: Provides links to Ryvals’ presence on social media.
   ```html
   <td><img src="{{ request.scheme }}://{{ request.get_host }}{% static 'images/template-twitter.png' %}" ... /></td>
   ```

## Template Variables

The template uses several Django template variables to dynamically insert content:

- `{{ request.scheme }}`: The request's scheme (http or https).
- `{{ request.get_host }}`: The current host.
- `{{ transaction_id }}`: The unique identifier of the failed transaction.
- `{{ username }}`: The username associated with the transaction.
- `{{ amount }}`: The transaction amount.
- `{{ date }}`: The date the transaction was attempted.

## Styling

The email uses inline CSS for styling, ensuring compatibility across various email clients. It predominantly uses a dark theme with white text, ensuring readability.

- **Font**: Arial, with different styles and weights for headers and body text.
- **Color Scheme**: A dark background (#191919) with white text (#fff) for contrast.
- **Layout**: Tables are used for layout, a common practice for email templates to maintain consistent formatting across different email clients.

## Utilities

- **Static Files**: The `{% static %}` tag is used to load images from the static files directory, ensuring they are served correctly in the email.
- **Django Template Language (DTL)**: Utilize DTL for inserting dynamic content and handling static files.

This template plays a crucial role in keeping the administrative team informed about transaction failures, allowing them to take necessary actions to resolve issues efficiently.