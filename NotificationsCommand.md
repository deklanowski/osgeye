format:

`notifications <on|off> <notification type>?`

options:

  * `<on|off>` - "on" or "off".

  * `<notification type>` - List of one or more notification types that includes:
    * bundles - Lifecycle notification events for bundles.
    * services - Lifecycle notification events for service.
    * framework - Framework notification events.

output:

When turned on, asynchronous notifications will be printed to the console.

examples:
```
    > notifications on 
   
    ...
   
    Notification: Bundle bundlec 1.0.0 installed.
    
    Notification: Bundle bundlec 1.0.0 resolved.
    
    Notification: Bundle bundlec 1.0.0 started.
```