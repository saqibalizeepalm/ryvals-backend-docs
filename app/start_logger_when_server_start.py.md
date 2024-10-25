# Documentation for `start_logger_when_server_starts.py`

Welcome to the documentation for the **`start_logger_when_server_starts.py`** file. This file is part of the application's service layer focused on logging activities efficiently by initiating a logging thread when the server starts. Below, you'll find a detailed explanation of its functionality, purpose, and structure.

---

## Table of Contents
- [Overview](#overview)
- [Code Explanation](#code-explanation)
- [Purpose and Functionality](#purpose-and-functionality)
- [How It Works](#how-it-works)
- [Key Variables](#key-variables)

---

## Overview

The `start_logger_when_server_starts.py` file is responsible for ensuring that a background logging service is initiated when the server starts. It integrates with the `ActivityThreadService`, which handles the logging queue and database writes for activity logs.

## Code Explanation

```python
import threading
from app.services.activity_log_service import ActivityThreadService

LOGGER_THREAD = None
LOG_THREAD_NAME = 'insert_log_into_database'
already_exists = False

for t in threading.enumerate():
    if t.name == LOG_THREAD_NAME:
        already_exists = True
        break

if not already_exists:
    t = ActivityThreadService()
    t.daemon = True
    t.name = LOG_THREAD_NAME
    t.start()
    LOGGER_THREAD = t
```

### Purpose and Functionality

- **Thread Initialization**: This script ensures that a dedicated logging thread is running to handle log data asynchronously, preventing it from interfering with the main application processes.
- **Avoiding Duplicate Threads**: It checks if a logging thread already exists to prevent multiple threads from being initiated, which could lead to race conditions or redundant operations.
- **Seamless Server Start**: By starting this logging service at server initialization, it ensures that the logging mechanism is ready to capture and process logs right from the beginning of server activity.

### How It Works

1. **Imports**: 
   - `threading`: Used to handle operations related to thread management.
   - `ActivityThreadService`: Imported from a service module that handles the core functionality of logging activities.

2. **Global Variables**:
   - `LOGGER_THREAD`: Initially set to `None`, it holds a reference to the logging thread once created.
   - `LOG_THREAD_NAME`: Constant string that holds the thread's designated name, ensuring uniqueness.

3. **Thread Evaluation**:
   - The script loops through all existing threads using `threading.enumerate()`.
   - It checks if a thread with the name `insert_log_into_database` already exists.

4. **Thread Creation**:
   - If no such thread exists, it initializes a new `ActivityThreadService` thread.
   - The thread is set as a daemon (`daemon=True`), which means it will run in the background and will not prevent the program from exiting.
   - The thread's name is set, and it is started using the `start()` method.

5. **Thread Assignment**:
   - Once the thread is started, it is assigned to the `LOGGER_THREAD` variable for potential reference elsewhere in the application.

### Key Variables

| Variable Name  | Description                                                                                |
|----------------|--------------------------------------------------------------------------------------------|
| `LOGGER_THREAD`| Holds the reference to the logging thread after initialization.                            |
| `LOG_THREAD_NAME`| A constant string used to identify the logging thread uniquely.                           |
| `already_exists` | Boolean flag to determine if a logging thread is already running.                         |

---

This script is crucial for maintaining efficient and performance-friendly logging operations within the application by ensuring that all activities are logged asynchronously right from the server's start.