# 📝 Documentation for `tasks.py` 📬

### Overview
The `tasks.py` file is an integral part of a Django application, utilizing the Celery task queue for asynchronous task management. The primary purpose of this file is to handle the task of sending emails asynchronously using the SendGrid API. This ensures that the email sending process doesn't block the main application flow and can be retried upon failure.

### Table of Contents
- [Imports](#imports)
- [Logging Setup](#logging-setup)
- [Task: `send_email`](#task-send_email)

---

### Imports
```python
import logging
from celery import shared_task
from django.conf import settings
from emails.models import EmailMessage
from sendgrid import SendGridAPIClient
from sendgrid.helpers.mail import Mail
from django.core.mail import EmailMessage as DjangoMail
```

- **logging**: Used to log messages, which helps in tracking the execution flow and errors.
- **celery.shared_task**: A decorator that marks the function as a Celery task.
- **django.conf.settings**: Access Django settings, particularly for SendGrid API key.
- **emails.models.EmailMessage**: The EmailMessage model stores information about each email.
- **sendgrid.SendGridAPIClient & sendgrid.helpers.mail.Mail**: Classes from the SendGrid library to send emails.
- **django.core.mail.EmailMessage**: Django's core email functionality, imported but unused here.

### Logging Setup
```python
logger = logging.getLogger('django')
```
- Sets up a logger to record information, warnings, and errors. This is crucial for monitoring the application's behavior, especially in production environments.

### Task: `send_email`
```python
@shared_task(bind=True, max_retries=3)
def send_email(self, email_id):
    ...
```

#### Description
The `send_email` function is a Celery task designed to send emails using the SendGrid service. It fetches an email object from the database, constructs the email, and attempts to send it. If it encounters an error, it retries the operation up to three times.

#### Parameters
- **self**: Represents the task instance itself, allowing access to methods like `retry`.
- **email_id**: The primary key of the `EmailMessage` object to be sent.

#### Execution Flow
1. **Logging Start Message**: Logs the start of the email sending process.
   ```python
   logger.info(f'app.send_email STARTED {str(email_id)}')
   ```

2. **Fetch Email Object**: Retrieves the `EmailMessage` object from the database using the `email_id`.
   ```python
   email_obj = EmailMessage.objects.filter(pk=email_id).first()
   ```

3. **Prepare Email Data**: Constructs the email using `Mail` from SendGrid.
   ```python
   message = Mail(
       from_email=email_obj.from_email,
       to_emails=to_email,
       cc=email_obj.cc,
       bcc=email_obj.bcc,
       subject=str(email_obj.subject),
       html_content=email_obj.html_message
   )
   ```

4. **Send Email**: Utilizes `SendGridAPIClient` to send the constructed email.
   ```python
   sg = SendGridAPIClient(settings.SENDGRID_API_KEY)
   sg.send(message)
   ```

5. **Update Status**: Marks the email status as `SENT` upon successful sending.
   ```python
   email_obj.sent_status = EmailMessage.Type.SENT.value
   email_obj.save()
   ```

6. **Exception Handling**: In case of errors, logs the error and retries the task.
   ```python
   except Exception as exc:
       logger.error(f'app.send_email ERROR')
       ...
       self.retry(exc=exc, countdown=60)
   ```

#### Return Value
- Returns a dictionary containing the email data and the result status (`success` or `failed`).

### Conclusion
The `tasks.py` file plays a crucial role in managing email dispatches in a non-blocking, efficient manner. Using Celery for task queuing and SendGrid for email delivery ensures that the application remains responsive and reliable in handling email communications.