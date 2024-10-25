# Documentation for `low_paypal_payout_balance.html`

This document provides an overview of the `low_paypal_payout_balance.html` file, which is a part of the Ryvals application. This HTML template is used to notify the admin when the PayPal account balance is low, ensuring that prompt actions can be taken to maintain the necessary funds for payouts.

## Overview

`low_paypal_payout_balance.html` is an email template rendered by the Django server to inform the admin about the low PayPal account balance. It provides detailed information regarding the current balance, available balance, withheld funds, and timestamps for when the balance was last updated. The email is styled using inline CSS for compatibility across various email clients.

## Structure and Components

The HTML file is structured using tables for layout control, which is a common practice in email templates to ensure consistent rendering across different email clients.

### HTML Elements

- **DOCTYPE Declaration**: 
  ```html
  <!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
  ```
  This declaration specifies the HTML version in use, ensuring compatibility with older email clients.

- **HTML Tag and Metadata**:
  ```html
  <html xmlns="http://www.w3.org/1999/xhtml">
  <head>
    <meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  </head>
  ```
  These elements define the character set and viewport settings, making sure the email is responsive and displays correctly.

- **Main Table Layout**:
  ```html
  <body>
    <table width="100%">
      <tr>
        <td class="wrapper" width="600" align="center">
          <table bgcolor="#f5faf5" width="600" border="0" align="center" cellpadding="0" cellspacing="0">
  ```
  The main table wraps the content, centered with a fixed width of 600 pixels for optimal viewing.

- **Header Section**:
  ```html
  <tr>
    <td height="89" style="background-image: url('{{ request.scheme }}://{{request.get_host}}/static/images/banner.png'); background-repeat: no-repeat; background-size: cover; background-color: #191919;">
      <img src="{{ request.scheme }}://{{ request.get_host }}{% static 'images/ryvals.png' %}" style="display:block; margin:auto; width:150px; height:38px;" />
    </td>
  </tr>
  ```
  This section includes the Ryvals logo and a banner background.

- **Message Content**:
  - **Greeting and Introduction**:
    ```html
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
                  <td width="516" style="font-family: Arial; font-size: 18px; font-weight: bold; font-stretch: normal; font-style: normal; line-height: 1.89; letter-spacing: normal; color: #fff;">Hello Admin,</td>
                  <td width="57"></td>
                </tr>
              </table>
            </td>
          </tr>
    ```
    This section starts with a greeting for the admin.

  - **Balance Information**:
    The following sections display the total balance, available balance, withheld balance, and timestamps:
    ```html
    <tr>
      <td width="600">
        <table width="600" bgcolor="#191919" border="0" align="center" cellpadding="0" cellspacing="0">
          <tr>
            <td width="27"> </td>
            <td width="516" style=" font-family: Arial; font-size: 16px; font-weight: normal; font-stretch: normal; font-style: normal; line-height: 1.5; letter-spacing: normal; color: #fff;">Paypal account balance is low, please add money to your paypal account. Here are the details: </td>
            <td width="57"></td>
          </tr>
        </table>
      </td>
    </tr>
    ```
    Each balance detail is enclosed in similar table rows for consistency.

  - **Closing**:
    ```html
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
    ```
    The closing line thanks the admin and signs off with the Ryvals name.

- **Footer Section**:
  ```html
  <tr height="356"></tr>
  <tr width="600">
    <td width="600">
      <table width="600" bgcolor="#141414" border="0" align="center" cellpadding="0" cellspacing="0">
        <tr height="16"></tr>
        <tr>
          <td width="33"></td>
          <td width="170" style=" opacity: 0.69; font-family: Arial; font-size: 10px; font-weight: normal; font-stretch: normal; font-style: normal; line-height: normal; letter-spacing: normal; color: #fff;">© 2023 RYVALS. All Rights Reserved.</td>
          <td width="226"></td>
          <td><img src="{{ request.scheme }}://{{ request.get_host }}{% static 'images/template-twitter.png' %}" style="width:14px; height:11px" /></td>
          <!-- Other social media icons -->
          <td width="16"></td>
        </tr>
        <tr height="16"></tr>
      </table>
    </td>
  </tr>
  ```
  The footer includes a copyright notice and social media icons.

## Usage

- The template is used to send automated notifications to the admin about low PayPal balance.
- It dynamically inserts balance details and timestamps using Django template tags.
- It ensures that the admin is aware of the account status to prevent any disruptions in service due to insufficient funds.

## Customization

- The template can be customized for branding purposes by modifying the colors, fonts, and images.
- The balance thresholds can be adjusted by altering the logic in the backend that triggers this email.

## Conclusion

The `low_paypal_payout_balance.html` template is a vital part of the Ryvals notification system, ensuring the admin is promptly informed about critical financial statuses, thereby maintaining the application's operational integrity.