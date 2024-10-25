# Activity Log Service Documentation

This document provides detailed information about the `activity_log_service.py` file, its purpose, and how it functions within the application. It is intended for developers and system administrators who need to understand the logging mechanism used in the application.

## Overview

The `activity_log_service.py` file is responsible for managing the logging of user activities within the application. It implements a threaded service that periodically processes and stores log entries in a database. This service is designed to handle a high volume of log data efficiently.

## Components

### Imports

- **threading**: Standard Python library for thread-based concurrency.
- **time**: Provides time-related functions.
- **Queue**: A thread-safe FIFO implementation from the `queue` module.
- **Thread**: Base class for creating new threads.
- **logging**: Provides logging capabilities.
- **settings**: Django settings module for accessing configuration variables.

### Logger Configuration

```python
logger = logging.getLogger('django')
```

This sets up a logger instance named `django`, which is used to log any errors or important events within the service.

## Class: `ActivityThreadService`

### Description

The `ActivityThreadService` class is a subclass of `Thread` that manages a queue of log entries. It periodically processes these entries and inserts them into a database.

### Initialization

```python
def __init__(self):
```

- **Attributes:**
  - `DRF_LOGGER_INTERVAL`: Time interval (in seconds) for processing the queue. Defaults to 60 seconds but can be configured via Django settings.
  - `LOGS_QUEUE_MAX_SIZE`: Maximum size of the queue. Defaults to 50 but can be configured via Django settings.
  - `_queue`: An instance of `Queue` with a maximum size set by `LOGS_QUEUE_MAX_SIZE`.

### Methods

#### `run()`

```python
def run(self) -> None:
```

Starts the queue processing by invoking `start_queue_process`.

#### `start_queue_process()`

```python
def start_queue_process(self):
```

Continuously checks the queue at intervals defined by `DRF_LOGGER_INTERVAL` and processes log entries if the queue size exceeds `LOGS_QUEUE_MAX_SIZE`.

#### `put_log_data()`

```python
def put_log_data(self, user, email, username, ip, message, action, vpn, extras):
```

- **Parameters:**
  - `user`: The user associated with the log entry.
  - `email`: Email of the user.
  - `username`: Username of the user.
  - `ip`: IP address of the user.
  - `message`: Log message.
  - `action`: Action taken by the user.
  - `vpn`: VPN status.
  - `extras`: Any additional data.

Adds a new log entry to the queue. If the queue size exceeds `LOGS_QUEUE_MAX_SIZE`, it triggers bulk insertion.

#### `_start_bulk_insertion()`

```python
def _start_bulk_insertion(self):
```

Processes and inserts log entries from the queue into the database in bulk.

### Static Method: `_insert_into_data_base()`

```python
@staticmethod
def _insert_into_data_base(bulk_item):
```

- **Parameters:**
  - `bulk_item`: List of log entries to be inserted.

Inserts the bulk of log entries into the database and handles exceptions during insertion.

## Usage

The `ActivityThreadService` can be used to log user activities efficiently. It is designed to handle concurrent log entries and store them in a database without blocking the main application thread.

## Configuration

The service can be configured using Django settings:
- `DRF_LOGGER_INTERVAL`: Configures the interval for processing the queue.
- `LOGS_QUEUE_MAX_SIZE`: Sets the maximum size of the log queue.

## Conclusion

The `activity_log_service.py` file provides a robust and efficient logging mechanism for tracking user activities. By using a threaded approach and bulk operations, it minimizes the performance impact on the application while ensuring that log data is stored reliably.