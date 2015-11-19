format:

`exports <bundle name pattern>? <version range>? <file pipe>?`

options:

  * `<bundle name pattern>` - The optional pattern used to match against bundles' symbolic name. All matched bundles will be included in the output. If no pattern is specified or `*` all bundles will be used. For details on what regular expression rules can be used see http://java.sun.com/j2se/1.5.0/docs/api/java/util/regex/Pattern.html#sum.

  * `<version range>` - The optional version range that matched bundle versions must fall within to be included in the output. If no version range is specified or `*` all bundle versions will be used. The version range can include a floor and a ceiling (ex. "[2.2.3,3.1.0)") that bundle versions must fall within to be included or just a version value (ex. "2.2.3") that bundle version must equal to be included.

  * `<file pipe>` - The output of this command can be piped to a file by using the syntax "> file path" as the last arguments.

output:

For each bundle that matches the exported packages for that bundle will be listed. Underneath each exported package a list of bundles willbe listed that are wired to this exported package (if any).

  * Exporting Bundle Symbolic Name, Exporting Bundle Symbolic Version Number
    * Exported Package Name, Exported Package Version
      * Wired Bundle Symbolic Name, Wired Bundle Version Number, Wired Bundle Import Declaration Version Range

examples:
```
    > exports org.eclipse.osgi
    
    org.eclipse.osgi 0.0.0
        org.eclipse.osgi.event 1.0.0
        org.eclipse.osgi.framework.console 1.0.0
        org.eclipse.osgi.framework.eventmgr 1.1.0
        org.eclipse.osgi.service.resolver 1.2.0
        org.eclipse.osgi.service.urlconversion 1.0.0
        org.eclipse.osgi.storagemanager 1.0.0
        org.eclipse.osgi.util 1.1.0
        org.osgi.framework 1.4.0
            org.eclipse.equinox.cm 1.0.0.v20080509-1800 1.3.0
            org.test.bundlea 1.0.0 [1.4.0,2.0.0)
            org.osgeye 0.0.1 0.0.0
        org.osgi.service.condpermadmin 1.0.0
        org.osgi.service.packageadmin 1.2.0
            org.osgeye 0.0.1 0.0.0
        org.osgi.service.permissionadmin 1.2.0
        org.osgi.service.startlevel 1.1.0
            org.osgeye 0.0.1 0.0.0
        org.osgi.service.url 1.0.0
        org.osgi.util.tracker 1.3.3
            org.eclipse.equinox.cm 1.0.0.v20080509-1800 1.3.1
```