# panic_thread.py
A panic_thread class to force misbehaving scripts to terminate. Useful when developing a script that is called in a way that makes manual termination tricky.

## usage example
```python
from panic_thread import PanicThread
import threading

# Create a PanicThread instance with custom thresholds
panic_thread = PanicThread(
  threading.current_thread(),
  PanicThread.ONE_GIGABYTE,
  PanicThread.ONE_MINUTE)

# Start the panic thread
panic_thread.start()

# Your script goes here
while True:
    pass

# End the panic thread when the script has ended normally
panic_thread.end()
```

IMPORTANT: don't forget to call PanicThread.end() or the execution will not finish until a threshold is passed!

Please note that this script uses the psutil library to monitor memory usage, and the threading library to handle the panic thread. If you haven’t installed psutil, you can do so using pip: pip install psutil.

This script continuously checks if the time or memory threshold is exceeded, and if so, it exits the script. You can adjust the MEMORY_THRESHOLD and TIME_THRESHOLD variables to suit your needs.

Please note that this is a simple example and might not work for complex multi-threaded applications. Also, abruptly exiting a script with os._exit(1) might not be the best approach in a real-world application as it could lead to resources not being cleaned up properly. It’s generally better to have a graceful shutdown process. This script is just to give you an idea of how you could implement a ‘panic’ thread. Always remember to handle resources and errors properly in your scripts.
