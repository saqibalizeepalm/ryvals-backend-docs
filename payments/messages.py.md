# Documentation for `messages.py` 📄

This file contains a series of message templates used throughout the application. These messages are primarily related to payment transactions and are designed to provide users with relevant feedback and notifications. The messages are internationalized using Django's translation utilities, which allow them to be easily translated into different languages.

## Overview 🌟

The `messages.py` file defines a set of constant message strings that are used to inform users about the status of various payment-related events and actions within the application. These messages are crucial for ensuring that users receive clear and concise communication about the outcomes of their transactions.

## Table of Contents 📚

1. [Imports](#imports)
2. [Payment Success Messages](#payment-success-messages)
3. [Payout Status Messages](#payout-status-messages)
4. [Error Messages](#error-messages)
5. [Redeem and Add Fund Messages](#redeem-and-add-fund-messages)
6. [Stripe and Shift4 Messages](#stripe-and-shift4-messages)

## Imports 📥

```python
from django.utils.translation import gettext_lazy as _
```

This import statement brings in Django's `gettext_lazy` function, which is used to wrap message strings for translation. This allows the application to support multiple languages by providing localized versions of each message.

## Payment Success Messages 💰

These messages inform users about successful payment transactions.

- **`PAYMENT_SUCCESS`**: "Payment transaction successfully completed"
- **`PAYMENT_PENDING`**: "Payment transaction successfully completed after 24 hours."
- **`PAYMENT_CREATED`**: "Payment transaction successfully created, status will update shortly."
- **`PAYMENT_INTENT_PROCESSING`**: "Payment transaction is processing, status will update shortly."

## Payout Status Messages 🏦

These messages provide updates on the status of payout transactions, both instant and standard.

- **Instant Payouts:**
  - **`INSTANT_PAYOUT_SUCCESSFUL_SUBJECT`**: "Instant payout successfully completed"
  - **`INSTANT_PAYOUT_FAILED_SUBJECT`**: "Instant payout failed."
  - **`INSTANT_PAYOUT_CANCELED_SUBJECT`**: "Instant payout was canceled."

- **Standard Payouts:**
  - **`STANDARD_PAYOUT_SUCCESSFUL_SUBJECT`**: "Standard payout successfully completed"
  - **`STANDARD_PAYOUT_FAILED_SUBJECT`**: "Standard payout failed."
  - **`STANDARD_PAYOUT_CANCELED_SUBJECT`**: "Standard payout was canceled."

## Error Messages 🚫

These messages inform users about errors that occur during various transactions, such as adding funds or redeeming balances.

- **`ADD_TO_WALLET_ERROR`**: "We were unable to add funds to your wallet. Please try again."
- **`REDEEM_TO_WALLET_ERROR`**: "Your funds cannot be redeemed at the moment due to some error. Please try again."
- **`REDEEM_TO_WALLET_ERROR_PAYPAL`**: "Your funds cannot be redeemed at the moment due to incorrect Paypal ID."
- **`VALID_FUND_AMOUNT`**: "Please enter a valid amount (eg. $100)"
- **`MIN_LIMIT_ERROR`**: "Please enter a value greater than or equal to $%(amount)d"
- **`MAX_LIMIT_ERROR`**: "You can only redeem funds that total your wallet balance of %(amount)d"
- **`DEPOSIT_LIMIT_EXCEED`**: "Today Money Deposit limit exceed. You can only add $10000 in a day."
- **`PAYMENT_FAILED`**: "Payment transaction failed."
- **`PAYMENT_CANCELLED`**: "Payment transaction cancelled."

## Redeem and Add Fund Messages 💵

These messages provide feedback on actions related to redeeming funds and adding funds to the user's wallet.

- **`SUBJECT_REDEEM_BALANCE`**: "Your Withdrawal from Ryvals.com was Successful!"
- **`SUBJECT_ADD_FUNDS`**: "Your Deposit on Ryvals.com was Successful!"
- **`PAYPAL_ID_NEEDED`**: "Please Update Your Paypal ID"
- **`REDEEM_BALANCE_MSG`**: "You have successfully redeemed $%(amount)s from your Ryvals wallet on %(date)s using PayPal. Please email us at support@ryvals.com if this was not triggered by you."
- **`PENDING_REDEEM_MSG`**: "You have successfully redeemed $%(amount)s from your Ryvals wallet on %(date)s, and your PayPal payout request will be successfully completed after 24 hours. Please email us at support@ryvals.com if this was not triggered by you."
- **`ADD_FUNDS_MSG`**: "You have successfully added $%(amount)d to your Ryvals PPK® wallet. Please contact us at support@ryvals.com if this was not you."

## Stripe and Shift4 Messages 💳

These messages relate to transactions involving Stripe and Shift4 payment gateways.

- **Stripe Messages:**
  - **`STRIPE_INSTANT_PAYOUT_SUCCESSFUL_MSG`**: "Instant payout of $%(amount)s successfully completed on %(date)s. Amount has been transferred to the card. Please contact us at support@ryvals.com if you have any query."
  - **`STRIPE_INSTANT_PAYOUT_FAILED_MSG`**: "Instant payout of $%(amount)s to the card failed on %(date)s. Please contact us at support@ryvals.com if you have any query."
  - **`STRIPE_INSTANT_PAYOUT_CANCELED_MSG`**: "Instant payout of $%(amount)s to the card canceled on %(date)s. Please contact us at support@ryvals.com if you have any query."
  - **`STRIPE_STANDARD_PAYOUT_SUCCESSFUL_MSG`**: "Standard payout of $%(amount)s successfully completed on %(date)s. Please contact us at support@ryvals.com if you have any query."
  - **`STRIPE_STANDARD_PAYOUT_FAILED_MSG`**: "Standard payout of $%(amount)s failed on %(date)s. Please contact us at support@ryvals.com if you have any query."
  - **`STRIPE_STANDARD_PAYOUT_CANCELED_MSG`**: "Standard payout of $%(amount)s canceled on %(date)s. Please contact us at support@ryvals.com if you have any query."
  - **`STRIPE_ADD_TO_WALLET_FAILED`**: "Shift4 Add to wallet failed"

- **Shift4 Messages:**
  - **`I4GO_TOKEN_REQUIRED`**: "Shift4 card token is required."
  - **`I4GO_CARD_EXPIRY_DETAILS_REQUIRED`**: "Shift4 card expiration month and year is required."
  - **`CARD_NUMBER_REQUIRED`**: "Shift4 card number is required."
  - **`CARD_NUMBER_OR_I4GO_TOKEN_REQUIRED`**: "Shift4 card number or card token is required."
  - **`CARD_IS_ALREADY_SAVED`**: "This card is already saved."

By using standardized message templates, the application ensures consistent communication with users, enhancing user experience and understanding of the system's operations. These messages are crucial, especially in financial operations, to maintain transparency and trust.