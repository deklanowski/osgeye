format:

`manifest <bundle name pattern>? <pretty|raw>? <version range>? <file pipe>?`

options:

  * `<bundle name pattern>` - The optional pattern used to match against bundles' symbolic name. All matched bundles will be included in the output. If no pattern is specified or `*` all bundles will be used. For details on what regular expression rules can be used see http://java.sun.com/j2se/1.5.0/docs/api/java/util/regex/Pattern.html#sum.

  * `<pretty|raw>` - The type of output for the manifest file. If "pretty" is specified the manifest file will be cleaned up to make it more readable. If "raw" is specified the manifest file will be printed out exactly as it was found in the bundle. If not specified "pretty" will be used by default.

  * `<version range>` - The optional version range that matched bundle versions must fall within to be included in the output. If no version range is specified or `*` all bundle versions will be used. The version range can include a floor and a ceiling (ex. "[2.2.3,3.1.0)") that bundle versions must fall within to be included or just a version value (ex. "2.2.3") that bundle version must equal to be included.

  * `<file pipe>` - The output of this command can be piped to a file by using the syntax "> file path" as the last argument.

output:

For each bundle that matches the given parameters the following will be printed:

  * Bundle Symbolic Name & Version Number

  * MANIFEST FILE

examples:
```
    > manifest org.osgeye
    
    org.osgeye 0.0.1

    Manifest-Version: 1.0
    Bundle-Name: org.osgeye
    Created-By: 1.5.0_16 (Apple Inc.)
    Private-Package:
        org.osgeye.domain
        org.osgeye.domain.manifest
        org.osgeye.events
        org.osgeye.messages
        org.osgeye.server
        org.osgeye.server.jmx
        org.osgeye.server.network
        org.osgeye.server.osgi
        org.osgeye.server.osgi.servicewrappers
        org.osgeye.server.osgi.utils
        org.osgeye.utils
    Bundle-Activator: org.osgeye.server.osgi.BundleActivator
    Import-Package:
        javax.management
        javax.naming
        org.osgi.framework
        org.osgi.service.cm
        org.osgi.service.log
        org.osgi.service.packageadmin
        org.osgi.service.startlevel
        org.slf4j
    Bundle-ManifestVersion: 2
    Bundle-SymbolicName: org.osgeye
    Tool: Bnd-0.0.249
    Bnd-LastModified: 1260158693752
    Bundle-Version: 0.0.1
    
    > manifest org.osgeye raw

    org.osgeye 0.0.1
    
    Manifest-Version: 1.0
    Bundle-Name: org.osgeye
    Created-By: 1.5.0_16 (Apple Inc.)
    Private-Package: org.osgeye.domain,org.osgeye.domain.manifest,org.osge
     ye.events,org.osgeye.messages,org.osgeye.server,org.osgeye.server.jmx
     ,org.osgeye.server.network,org.osgeye.server.osgi,org.osgeye.server.o
     sgi.servicewrappers,org.osgeye.server.osgi.utils,org.osgeye.utils
    Bundle-Activator: org.osgeye.server.osgi.BundleActivator
    Import-Package: javax.management,javax.naming,org.osgi.framework,org.o
     sgi.service.cm,org.osgi.service.log,org.osgi.service.packageadmin,org
     .osgi.service.startlevel,org.slf4j
    Bundle-ManifestVersion: 2
    Bundle-SymbolicName: org.osgeye
    Tool: Bnd-0.0.249
    Bnd-LastModified: 1260158693752
    Bundle-Version: 0.0.1
```