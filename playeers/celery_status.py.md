# Celery Status Management Script Documentation

## Overview
The `celery_status.py` script is a Django management command designed to check the status of a specified Celery service on the server. It helps in monitoring the operational status of the Celery task queue system and can notify administrators via email if the service is not running.

## Features
- Checks the operational status of a specified Celery service.
- Sends an email notification to administrators if the service is not active.
- Provides console output to indicate the current status of the service.

## Usage
This script is executed as a Django management command. Below is the syntax for running the command and its expected behavior.

### Command Syntax
```bash
python manage.py celery_status <file>
```
- `<file>`: The name of the Celery service file you want to check.

### Example
```bash
python manage.py celery_status celery.service
```
This command checks the status of the `celery.service` on the server.

## Script Breakdown

### Imports
- **os**: Used to execute system commands.
- **Email**: Utility for sending email notifications.
- **settings**: Access to Django settings for configuration.
- **BaseCommand**: Django utility for creating custom management commands.

### Class Definition
```python
class Command(BaseCommand):
    help = 'Check the status of celery file'
```
- **Command**: This class extends Django's `BaseCommand` to create a custom command.
- **help**: A brief description of the command's purpose.

### Adding Arguments
```python
def add_arguments(self, parser):
    parser.add_argument('file', type=str, help='Indicates the name of the celery file.')
```
- **add_arguments**: Defines the arguments that the command accepts. In this case, it accepts a single argument `file` which specifies the Celery service file name.

### Handle Method
```python
def handle(self, *args, **kwargs):
    name = kwargs['file']
    output = os.popen(f'sudo systemctl status {name}').read()
    if 'Active: active (running)' in output:
        self.stdout.write(f"Celery status is Active")
    else:
        Email(
            ['deepak.kumar.2@netsolutions.com', 'bhupinder.singh@netsolutions.com'],
            "Celery Status"
        ).message_from_template(
            'email/celery-status.html',
            {'server': settings.AWS_SERVER_NAME},
            None
        ).send()
```

- **handle**: The core method that gets executed when the command is run.
  - Retrieves the Celery service file name from the command arguments.
  - Executes a system command to check the status of the specified Celery service.
  - Parses the command output to determine if the service is active.
  - If the service is active, it prints a message to the console.
  - If the service is not active, it sends an email notification to specified recipients.

### Email Notification
- **Recipients**: `deepak.kumar.2@netsolutions.com`, `bhupinder.singh@netsolutions.com`
- **Email Template**: `email/celery-status.html`
- **Email Context**: Includes the server name from the Django settings.

## Conclusion
The `celery_status.py` management command is a useful tool for system administrators to ensure that the Celery service is running as expected. It provides immediate notifications through email if the service is down, allowing for quick response and resolution.