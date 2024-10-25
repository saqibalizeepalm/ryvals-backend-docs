# Documentation for `pending-redeem.html`

This document provides an overview of the `pending-redeem.html` file, which is an HTML email template used in the Ryvals application to notify users about their pending redemption requests.

## Overview

The `pending-redeem.html` is an email template designed to inform users that they have successfully redeemed a specific amount from their Ryvals wallet and that their PayPal payout request is being processed. The email provides details about the transaction and offers assistance if needed.

### Structure

The email is structured using HTML and styled with inline CSS. It incorporates dynamic content placeholders that are populated with specific data when the email is sent.

### Key Components

- **Header Section:** 
  - Displays the Ryvals logo at the top of the email with a banner background. The logo image is dynamically loaded from the server using Django's static file handling.

- **Greeting:**
  - The email begins with a personalized greeting using the recipient's username.

- **Main Content:**
  - Provides a summary of the transaction, including the redeemed amount, the date of the transaction, and the updated wallet balance.
  - Contains a reminder that the PayPal payout will be processed after 24 hours.

- **Contact Information:**
  - Offers a contact email for support in case the transaction was not initiated by the user or if further assistance is needed.

- **Footer:**
  - Concludes the email with a thank you note.
  - Displays the Ryvals company name.

- **Social Media Links:**
  - Includes icons for various social media platforms (Twitter, Facebook, Instagram, YouTube, Hangouts), linking to Ryvals' profiles.

### Dynamic Content Placeholders

The template uses Django template tags to insert dynamic data into the email:

- `{{username}}`: The name of the user receiving the email.
- `{{amount}}`: The amount that has been redeemed.
- `{{date}}`: The date when the redemption was processed.
- `{{wallet_balance}}`: The user's current wallet balance after the redemption.

### Styling

- The email uses a dark background (#191919) with white text to ensure readability.
- Font styling is consistent across the email, using Arial with varying sizes and weights for emphasis.
  
### Summary

The `pending-redeem.html` file is a crucial part of the Ryvals notification system, ensuring users are informed about their financial transactions within the platform. By providing clear details and support options, it helps build trust and transparency between Ryvals and its users.