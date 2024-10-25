# utils.py Documentation 📧✨

The `utils.py` file serves as a core utility component for handling email functionalities within the Django application. It encapsulates the creation, customization, and sending of email messages, leveraging both Django's native email capabilities and the SendGrid email service.

---

## 📄 **Overview**

This file defines an `Email` class which is responsible for:
- Creating and storing email data.
- Supporting email customization via HTML templates.
- Sending emails using SendGrid or asynchronously via Celery.

The utility ensures that emails are composed with the correct metadata and content before dispatching.

---

## 📦 **Imports**

```python
from django.conf import settings
from emails.tasks import send_email
from django.template.loader import get_template
from accounts.messages import TEXT_OR_HTML_REQUIRED
from django.core.mail import EmailMessage as DjangoMail
from sendgrid import SendGridAPIClient
from sendgrid.helpers.mail import Mail
from rest_framework.exceptions import APIException
import logging
```

- **Django & Core Libraries**: For settings management, template rendering, exceptions, and logging.
- **SendGrid**: For sending emails via the SendGrid API.
- **Celery**: For task management and asynchronous processing.
  
---

## 🛠️ **Class: Email**

The `Email` class provides a structured way to create, customize, and send email messages. 

### **Attributes**

- `to`: List of recipient email addresses.
- `subject`: Subject of the email.
- `html_message`: HTML content of the email.
- `cc`: List of CC email addresses (optional).
- `bcc`: List of BCC email addresses (optional).
- `from_addr`: Sender's email address (optional).

### **Methods**

#### `__init__(self, to, subject, html_message=None, cc=None, bcc=None, from_addr=None)`
- **Purpose**: Initializes an email object with recipient(s), subject, and optional CC/BCC and sender address.
- **Details**: Ensures `to`, `cc`, and `bcc` are lists for consistent processing.

#### `html(self, html)`
- **Purpose**: Assign HTML content to the email.
- **Return**: `self` for method chaining.

#### `from_address(self, from_address)`
- **Purpose**: Set a custom sender address.
- **Return**: `self` for method chaining.

#### `message_from_template(self, template_name, context, request=None)`
- **Purpose**: Render and set an email message body from a template.
- **Return**: `self` for method chaining.

#### `send(self)`
- **Purpose**: Send the email using either SendGrid or Celery.
- **Details**:
  - Throws an exception if HTML content is missing.
  - Stores the email object in the database.
  - Uses SendGrid for direct sending or Celery for asynchronous processing based on settings.

---

## 🌈 **Usage Example**

```python
email = Email(
    to=['recipient@example.com'],
    subject='Welcome!',
    html_message='<p>Hello, welcome to our service!</p>'
)
email.from_address('no-reply@yourdomain.com').send()
```

- Creates an `Email` instance.
- Customizes the sender's address.
- Sends the email immediately.

---

## ⚙️ **Configuration**

- **SendGrid API**: Requires `SENDGRID_API_KEY` and `SENDGRID_EMAIL` in the Django settings.
- **Celery**: Requires `CELERY_ENABLED` and `EMAIL_ALLOWED` flags for asynchronous sending.

---

## 📝 **Logging**

- Utilizes the `django` logger to capture information and error messages during email processing.

---

**Note**: Ensure all relevant settings and environment variables are correctly configured to enable email functionalities.

---

Feel free to refer to this documentation whenever you need a comprehensive understanding of the `utils.py` file and its role in managing email operations within your Django project! 🚀📬