format:

`services <interface name pattern>? <file pipe>?`

options:

  * `<interface name pattern>` - The optional pattern used to match against services' registered interface (or class) names. All matched interface names will be included in the output. If no pattern is specified or `*` all services will be used. For details on what regular expression rules can be used see http://java.sun.com/j2se/1.5.0/docs/api/java/util/regex/Pattern.html#sum.

  * <file pipe> - The output of this command can be piped to a file by using the syntax "> file path" as the last argument.

output:

For each services that matches the given parameters the implementing bundle(s) will be listed underneath the service interface (or class) name. A list of service properties will be printed underneath the bundle (if the bundle provides those properties).

  * Service Interface Or Class Registered Name
    * Implementing Bundle Symbolic Name, Implementing Bundle Version
      * ID
      * Service PID
      * Description
      * Ranking
      * Vendor

examples:

```
    > services org.osgi.service.cm.ManagedService 
    
    org.osgi.service.cm.ManagedService
        
        org.osgeye 0.0.1
            ID: 25
            Service PID: 0.0.1.org.osgeye.server.osgi.BundleActivator
            Description: org.osgeye.server.osgi.BundleActivator 0.0.1 configuration interface

    > services org.osgi.service.cm.ConfigurationListener 
    
    org.osgi.service.cm.ConfigurationListener
        
        org.eclipse.equinox.cm 1.0.0.v20080509-1800
            ID: 23
        
        org.osgeye 0.0.1
            ID: 26
```