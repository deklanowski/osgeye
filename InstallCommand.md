format:

`install <bundle file path>`

options:

  * `<bundle file path>` - The relative or absolute path for the bundle to install.

output:

Once this command is entered a confirmation will be given before the install is executed. This confirmation will list the path to the jar file that is about to be acted on (installed). If the action is not confirmed the command prompt will return with no action taken. If the action is confirmed then the install will be executed. If the install failed an error message will be returned to the screen otherwise on a message indicating the install was success will be displayed.

examples:
```
    > install ./bundlea_1.0.0.jar 
    
    Confirm bundle installation ./bundlea_1.0.0.jar (N) Y
    Sending bundle to install...
    Bundle bundlea 1.0.0 installed.

    >
```