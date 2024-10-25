# Task Management with Celery in `tasks.py` 📋

The `tasks.py` file is a critical component of a Django-based application where asynchronous tasks are defined and managed using Celery. This file handles various tasks related to transaction processing, user notifications, and inactivity management. Below is a detailed explanation of the code in `tasks.py`.

## Table of Contents 📚
1. [Imports and Initial Setup](#imports-and-initial-setup)
2. [Utility Functions](#utility-functions)
   - [if_no_payout_response](#if_no_payout_response)
3. [Celery Tasks](#celery-tasks)
   - [redeem_player_request](#redeem_player_request)
   - [monthly_enrollment_reminder](#monthly_enrollment_reminder)
   - [inactivity_charges_deduction_reminder](#inactivity_charges_deduction_reminder)
   - [inactivity_charges_deduction](#inactivity_charges_deduction)
4. [Constants](#constants)

---

## Imports and Initial Setup 📦

The code begins by importing necessary libraries and modules:

```python
import pytz
import stripe
import logging
from itertools import chain
from ryvals.celery import app
from emails.utils import Email
from twilio.rest import Client
from django.conf import settings
from django.db.models import Max, F
from nimda.models import Logs, Config
from app.utils import UtilityMethods
from django.utils import timezone
from accounts.models import Profile, Player
from datetime import datetime, timedelta
from players.models import TransactionDetail, StripeTransfer, StripeAccount
from ryvals.core.discord import paypal_payment_process
from accounts.models import User, RyvalsAdmin
from players.models import PlayerLobby
from payments.messages import PAYMENT_SUCCESS, SUBJECT_REDEEM_BALANCE, REDEEM_BALANCE_MSG, REDEEM_BALANCE_FAIL_MSG, MONTHLY_ENROLLMENT_REMINDER, INACTIVITY_CHARGES_DEDUCTION_REMINDER, INACTIVITY_CHARGES_DEDUCTED
```

### Key Imported Modules:
- **pytz**: For timezone management.
- **stripe**: For handling payment processes via Stripe.
- **logging**: To log information or errors.
- **itertools.chain**: For chaining iterables.
- **Celery**: For defining asynchronous tasks.
- **Twilio**: For sending messages/alerts.
- **Django ORM**: For database queries and management.

---

## Utility Functions 🛠

### if_no_payout_response

A function that notifies the admin when a payout transaction fails and hasn't already been notified.

```python
def if_no_payout_response(transaction):
    if not transaction.admin_notify:
        Email(settings.ADMIN_EMAIL, REDEEM_BALANCE_FAIL_MSG).message_from_template('email/redeem-balance-transaction-fail.html', {
            'transaction_id': transaction.transaction_number,
            'amount': transaction.amount,
            'username': transaction.receiver.username,
            'date': timezone.now().astimezone(pytz.timezone(US_EAST_TIMEZONE_CONST)).strftime(DATE_TIME_STRING_FORMAT_CONST),
            'img_path': settings.REQUEST_URL + STATIC_IMAGE_PATH_CONST
        }, None).send()
        transaction.admin_notify = True
        transaction.save()
    else:
        logger.error(f'Payout failed, Admin already notified.: {transaction.transaction_number}')
```

---

## Celery Tasks ⏳

### redeem_player_request

Handles the logic for processing player redemption requests via PayPal after a defined period.

```python
@app.task
def redeem_player_request():
    try:
        pending_transactions = TransactionDetail.objects.filter(status=TransactionDetail.Status.PENDING, type=TransactionDetail.Type.REDEEM_BALANCE, amount__gt=0, has_paypal_api_hit=False)
        current_date_time = timezone.now()
        for transaction in pending_transactions:
            transaction_time = transaction.create_date
            release_time = transaction_time + timedelta(hours=24)
            if current_date_time >= release_time and transaction.payment_method == TransactionDetail.PaymentMethod.PAYPAL:
                receiver = Profile.objects.get(user=transaction.receiver)
                transaction_amount = transaction.amount
                deductions = transaction.transaction_fee
                try:
                    payout_response = paypal_payment_process(round(float(transaction_amount) - deductions, 2), receiver.paypal_id, receiver.noti_email)
                except Exception as e:
                    logger.error(e)
                if payout_response:
                    transaction.transaction_number = payout_response['transaction_id']
                    transaction.has_paypal_api_hit = True
                    transaction.save()
                else:
                    if_no_payout_response(transaction)
        logger.info('pending payouts released')
        return "pending payouts released"
    except Exception as e:
        logger.info(f"redeem players request Error >>> {str(e)}")
```

### monthly_enrollment_reminder

Sends reminders to players about monthly enrollments and potential inactivity charges.

```python
@app.task
def monthly_enrollment_reminder():
    # Function logic
    return 'monthly enrollment reminder sent!'
```

### inactivity_charges_deduction_reminder

Reminds players about upcoming inactivity charges.

```python
@app.task
def inactivity_charges_deduction_reminder():
    # Function logic
    return 'inactivity charges deduction reminder sent!'
```

### inactivity_charges_deduction

Deducts inactivity charges from players who haven’t participated in games for a specified duration.

```python
@app.task
def inactivity_charges_deduction():
    # Function logic
    return 'inactivity charges deducted!'
```

---

## Constants ⚙️

Several constants are defined to standardize formatting and paths:

- **US_EAST_TIMEZONE_CONST**: `'US/Eastern'`
- **DATE_TIME_STRING_FORMAT_CONST**: `'%m/%d/%y %H:%M:%S %p'`
- **STATIC_IMAGE_PATH_CONST**: `"/static/images/"`
- **DATE_STRING_FORMAT_CONST**: `"%Y-%m-%d"`
- **GAMES_PATH_CONST**: `"/games"`

---

## Conclusion 🎉

The `tasks.py` file efficiently orchestrates various asynchronous operations in the application, significantly improving the application's performance and user experience by processing tasks in the background without blocking the main thread. This documentation provides a comprehensive understanding of the functionality and purpose of each component within the file.