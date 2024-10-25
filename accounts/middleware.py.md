# 📄 Middleware Documentation: `middleware.py`

Welcome to the documentation for the `middleware.py` file of the Django project. This file includes a custom middleware class `VPNCheckMiddleware` designed to enhance security by detecting VPN connections for certain requests. Let's delve deeper into its components and functionalities. 🚀

---

## 🌟 Overview

**Middleware** in Django is a way to process requests globally before they reach the view or after the view has processed them. It acts as a framework of hooks into Django's request/response processing. The `VPNCheckMiddleware` in this file is specifically used to detect and restrict VPN usage for specific endpoints as defined in the configuration.

---

## 🔍 Detailed Breakdown

### 📚 Imports

```python
from django.http import JsonResponse
import logging
import requests
from django.conf import settings
```

- **`django.http.JsonResponse`**: Used to return JSON responses when a VPN is detected.
- **`logging`**: Provides a way to configure and use logging.
- **`requests`**: A simple library to make HTTP requests.
- **`django.conf.settings`**: Access project settings.

### 🏗️ `VPNCheckMiddleware` Class

#### **Purpose:**
This middleware is implemented to check whether requests are coming from a VPN and block them if they are, based on specific endpoints.

#### **Components:**

- **Initialization (`__init__`)**:
  - Sets up the middleware with the `get_response` callable to maintain the standard middleware signature.
  - Initializes `ip` and `url` as empty strings.

  ```python
  def __init__(self, get_response):
      self.get_response = get_response
      self.ip = ''
      self.url = ''
  ```

- **Main Callable (`__call__`)**:
  - **Process Request**: Retrieves the visitor's IP address.
  - **Logging**: Logs the retrieved IP using the configured logger.
  - **VPN Check**: Checks if the request's path is in the specified `urls_list` and evaluates VPN status using the IPQualityScore API.
  - **Response**: If a VPN is detected with a high fraud score, a JSON response is returned, prompting the user to deactivate the VPN.

  ```python
  def __call__(self, request):
      try:
          response = self.get_response(request)
          ip = self.visitor_ip_address(request)
          logger.info('IP is :')
          logger.info(ip)
          url = settings.IPQUALITYSCOREURL.replace('<user_ip>', ip)

          if eval(settings.VPN_ENABLED):
              urls_list = [...]
          else:
              urls_list = []

          if request.path in urls_list:
              ...
              res = requests.get(url=url).json()
              logger.info(res)

              if res['vpn'] and res['fraud_score'] >= 75:
                  logger.info("inside VPN condition")
                  return JsonResponse({
                      'message': 'Please deactivate the VPN',
                      'status': 400
                  }, status=406)
      except Exception as e:
          self.process_exception(request, e)
      return response
  ```

- **Helper Method - `visitor_ip_address`**:
  - **Purpose**: Extracts the client's IP address from the request.
  - **Method**: Checks for IP in `HTTP_X_FORWARDED_FOR` header; falls back to `REMOTE_ADDR`.

  ```python
  def visitor_ip_address(self, request):
      x_forwarded_for = request.META.get('HTTP_X_FORWARDED_FOR')
      if x_forwarded_for:
          ip = x_forwarded_for.split(',')[0]
      else:
          ip = request.META.get('REMOTE_ADDR')
      return ip
  ```

- **Exception Handling - `process_exception`**:
  - **Purpose**: Logs exceptions encountered during request processing.

  ```python
  def process_exception(self, request, exception):
      logger.info(exception.__class__.__name__)
      logger.info(exception)
      return None
  ```

---

## ⚙️ Configuration

Before using this middleware, ensure the following settings are configured:

- **`IPQUALITYSCOREURL`**: Template URL for the IPQualityScore API, with a placeholder for `<user_ip>`.
- **`VPN_ENABLED`**: Boolean flag (string) to enable or disable VPN checks.

---

## 🌈 Conclusion

The `VPNCheckMiddleware` provides a robust mechanism to enhance security by preventing VPN-based access to sensitive endpoints. By integrating it with logging and exception handling, it ensures that any issues during request processing are captured and logged efficiently. Use and configure it wisely to safeguard your Django applications! 🛡️