# Documentation for `redeem-standard-stripe.html`

## Overview

The `redeem-standard-stripe.html` file is a template used for generating email notifications to users when they successfully redeem money from their Ryvals wallet to their Stripe account using the standard payout option. This HTML template is specifically designed to inform users about the details of their transaction, ensuring they are aware of the status and the next steps regarding their redeemed balance.

## Template Structure

### HTML Document Structure

- **DOCTYPE and HTML Declaration**: Declares the document as an HTML 1.0 Transitional document.
- **Head Section**: Sets the character encoding and viewport settings.
- **Body Section**: Contains the main content of the email, structured using HTML tables for layout purposes.

### Sections Breakdown

1. **Header**
   - Contains a banner with the Ryvals logo.
   - Styled with a background image and color for aesthetic appeal and brand consistency.

2. **Greeting**
   - A personalized greeting that addresses the user by their username, enhancing the user experience through personalization.

3. **Main Content**
   - **Transaction Confirmation**: Notifies the user that they have successfully redeemed a specified amount from their Ryvals wallet to their Stripe account.
   - **Processing Time**: Specifies that the standard payout request will be processed within 2 to 7 days.
   - **Wallet Balance**: Updates the user on their new wallet balance after the transaction.

4. **Contact Information**
   - Provides a contact email for Ryvals support, encouraging users to reach out if they have not initiated the transaction or require further assistance.

5. **Closing and Footer**
   - A closing statement thanking the user for using Ryvals.
   - A footer section with a copyright notice and social media icons to promote engagement.

## Email Template Details

- **Dynamic Content**: Uses placeholders (e.g., `{{username}}`, `{{amount}}`, `{{date}}`, `{{wallet_balance}}`) to dynamically insert user-specific data into the email content.
- **Styling**: Utilizes inline CSS for styling elements such as fonts, colors, and layout, ensuring the email renders consistently across various email clients.
- **Social Media Icons**: Includes icons for Twitter, Facebook, Instagram, YouTube, Hangouts, and an unspecified platform, facilitating easy access to Ryvals' social media channels.

## Usage

This template is typically rendered by backend processes, which populate the placeholders with actual data before sending the email to the user. It is a crucial part of the user experience, providing transparency and clarity regarding financial transactions on the Ryvals platform.