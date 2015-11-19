format:

`set <type> <level value> <bundle name pattern>? <version range>?`

options:

  * `<type>` - The type to set. One of:
    * startlevel - The framework start level.
    * initbundlelevel - The initial start level for bundles.
    * bundlelevel - A bundle(s) start level. This can be optional followed by the bundle name and version pattern.

  * `<level value>` - The integer value.

  * `<bundle name pattern>` - This sub-command only applies when setting the bundle level. The optional pattern used to match against bundles' symbolic name. All matched bundles will be included in this action. If no pattern is specified or `*` all bundles will be used. For details on what regular expression rules can be used see http://java.sun.com/j2se/1.5.0/docs/api/java/util/regex/Pattern.html#sum.

  * `<version range>` - This sub-command only applies when setting the bundle level. The optional version range that matched bundle versions must fall within to be included in the output. If no version range is specified or `*` all bundle versions will be used. The version range can include a floor and a ceiling (ex. "[2.2.3,3.1.0)") that bundle versions must fall within to be included or just a version value (ex. "2.2.3") that bundle version must equal to be included.

see:

http://www.osgi.org/javadoc/r4v41/org/osgi/service/startlevel/StartLevel.html#setStartLevel(int)

http://www.osgi.org/javadoc/r4v41/org/osgi/service/startlevel/StartLevel.html#setInitialBundleStartLevel(int)

http://www.osgi.org/javadoc/r4v41/org/osgi/service/startlevel/StartLevel.html#setBundleStartLevel(org.osgi.framework.Bundle,%20int)

output:

Once this command is entered a confirmation will be given before the set operation is executed. When setting the bundle level a list of all the bundles that are about to be acted on will be displayed (the other two set operations are at the framework level). If the action is not confirmed the command prompt will return with no action taken. If the action is confirmed then the set operation will be executed. If the set operation failed an error message will be returned to the screen otherwise on a success the command prompt will return for the next command.

examples:
```
    > set startlevel 200     
    
    Confirm setting start level to 200 (N) Y
    Setting start level...
    
    > set initbundlelevel 50
    
    Confirm setting initial bundle start level to 50 (N) Y
    Setting initial bundle start level...

    > set bundlelevel 250 wsdl4j 
    
    The following bundles will be acted on:
        wsdl4j 1.6.1
    
    Confirm setting start level to 250 on the above bundles (N) Y
    Setting bundles start level...

    >
```