# Celery Periodic Tasks Data JSON Documentation

This documentation provides an overview of the `celery_periodic_tasks_data.json` file used in a Django application that utilizes Celery for task scheduling.

## Overview

The `celery_periodic_tasks_data.json` file is a JSON-based data fixture that defines periodic tasks for Django Celery Beat. Celery Beat is an extension to the Celery task queue that provides periodic task scheduling. This JSON file is used to seed the database with predefined periodic tasks.

## JSON Structure

The JSON file contains an array of objects, where each object represents a periodic task. Here is the structure of each task object:

```json
[
    {
        "model": "django_celery_beat.periodictask",
        "pk": 1,
        "fields": {
            "name": "Update Lobby Times",
            "task": "app.tasks.update_lobby_time",
            "interval": 1,
            "crontab": null,
            "solar": null,
            "clocked": null,
            "args": "[]",
            "kwargs": "{}",
            "queue": null,
            "exchange": null,
            "routing_key": null,
            "headers": "{}",
            "priority": null,
            "expires": null,
            "expire_seconds": null,
            "one_off": false,
            "start_time": "2021-09-15T11:16:59Z",
            "enabled": true,
            "last_run_at": "2021-09-20T13:02:58.608Z",
            "total_run_count": 167,
            "date_changed": "2021-09-20T13:03:03.681Z",
            "description": ""
        }
    }
]
```

### Fields Description

- **model**: Specifies the Django model associated with the data. Here it is `django_celery_beat.periodictask`, which refers to the periodic task model in Django Celery Beat.
- **pk**: The primary key of the record in the database.
- **fields**: A dictionary containing the properties of the periodic task:
  - **name**: A string representing the name of the periodic task. For example, "Update Lobby Times".
  - **task**: The Python path to the task function that should be executed periodically. This should match a task defined in your Django application, e.g., `"app.tasks.update_lobby_time"`.
  - **interval**: A foreign key reference to an interval schedule (defined in a separate fixture, e.g., `celery_intervals_data.json`) that determines how often the task should be run.
  - **crontab**, **solar**, **clocked**: These fields are null in this example, indicating that the task does not use these types of scheduling.
  - **args**: A JSON array of positional arguments to pass to the task. Here, it is an empty array `[]`.
  - **kwargs**: A JSON object of keyword arguments to pass to the task. Here, it is an empty object `{}`.
  - **queue**, **exchange**, **routing_key**, **headers**: These are used for advanced messaging configurations and are null or default in this example.
  - **priority**: The priority of the task, if any.
  - **expires**, **expire_seconds**: These fields specify when the task should cease to be available for execution, which are null in this example.
  - **one_off**: A boolean indicating whether the task should be executed only once. It is `false` here, meaning the task is recurring.
  - **start_time**: The datetime when the task was first scheduled to run.
  - **enabled**: A boolean indicating whether the task is active.
  - **last_run_at**: The last time the task was executed.
  - **total_run_count**: The number of times the task has been executed.
  - **date_changed**: The last time the task was modified.
  - **description**: A text field for additional information about the task.

## Usage

To use this JSON configuration, load it into your Django application's database using the Django management command:

```bash
python manage.py loaddata celery_periodic_tasks_data.json
```

This command will populate the database with the periodic tasks configured in the JSON file, allowing Django Celery Beat to manage and execute these tasks based on the specified schedule.

## Summary

The `celery_periodic_tasks_data.json` file is an essential component for managing periodic tasks in a Django application using Celery. It provides a structured way to define and manage recurring tasks, ensuring that they are executed at the desired intervals. By leveraging this configuration, developers can automate various processes within their applications, improving efficiency and reducing the need for manual intervention.