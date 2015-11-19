format:

`refresh <bundle name pattern>? <version range>?`

options:

  * `<bundle name pattern>` - The optional pattern used to match against bundles' symbolic name. All matched bundles will be included in this action. If no pattern is specified or `*` all bundles will be used. For details on what regular expression rules can be used see http://java.sun.com/j2se/1.5.0/docs/api/java/util/regex/Pattern.html#sum.

  * `<version range>` - The optional version range that matched bundle versions must fall within to be included in the output. If no version range is specified or `*` all bundle versions will be used. The version range can include a floor and a ceiling (ex. "[2.2.3,3.1.0)") that bundle versions must fall within to be included or just a version value (ex. "2.2.3") that bundle version must equal to be included.

see:

http://www.osgi.org/javadoc/r4v41/org/osgi/service/packageadmin/PackageAdmin.html#refreshPackages(org.osgi.framework.Bundle[])

note:

Refreshing the packages on the OSGEye bundle will cause the console to get disconnected.

output:

Once this command is entered a confirmation will be given before the refresh packages is executed. This confirmation will list all bundles that are about to be acted on (refreshed). If the action is not confirmed the command prompt will return with no action taken. If the action is confirmed then the refresh will be executed. You will need to do a reload after this command to see the results.

examples:
```
    > refreshpacks org.test.*
    
    The following bundles will be acted on:
        org.test.api 2.1.1
        org.test.impl 2.1.1
    
    Confirm refreshpacks on the above bundles (N) Y
    Sending refresh packages request...
    
    >
```