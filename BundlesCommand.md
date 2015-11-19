format:

`bundles <bundle name pattern>? <version range>? <file pipe>?`

options:

  * `<bundle name pattern>` - The optional pattern used to match against bundles' symbolic name. All matched bundles will be included in the output. If no pattern is specified or `*` all bundles will be used. For details on what regular expression rules can be used see http://java.sun.com/j2se/1.5.0/docs/api/java/util/regex/Pattern.html#sum.

  * `<version range>` - The optional version range that matched bundle versions must fall within to be included in the output. If no version range is specified or `*` all bundle versions will be used. The version range can include a floor and a ceiling (ex. "[2.2.3,3.1.0)") that bundle versions must fall within to be included or just a version value (ex. "2.2.3") that bundle version must equal to be included.

  * `<file pipe>` - The output of this command can be piped to a file by using the syntax "> file path" as the last argument.

output:

A summary of each matching bundle.

  * Bundle Symbolic Name & Version Number
    * Type - Either Normal or Fragment
    * State - The bundle state (one of Active, Resolved, Installed, Uninstalled, Starting, Stopping)
    * Last Modified - The time this bundle was last changed.
    * Location - The location on the remote server that this bundle has been deployed from.
    * Start Level - The assigned start level value for the specified bundle.
    * Attached Fragments - A (optional) list of fragment bundles that have attached to this bundle.
    * Bundle Hosts - A (optional) list of bundles that this fragment bundle has attached to.
    * Services - A (optional) list of interfaces this bundle has exported as services.
    * Exported Packages - A (optional) list of packages (each with its version) this bundle exports.
    * Imported Packages - A (optional) list of packages (each with its version range) this bundle imports. A "?" is included on the end of optional package imports.

examples:

```
  bundles commons-httpclient
  
  commons-httpclient 3.0.1
      ID: 35
      Type: Normal
      State: Active
      Last Modified: 12/06/09 10:05:55
      Location: file:////Users/baswerc/libs/commons-httpclient-3.0.1.jar
      Start Level: 20
      Exported Packages:
          org.apache.commons.httpclient.protocol 3.0.1
          org.apache.commons.httpclient.auth 3.0.1
          org.apache.commons.httpclient.methods 3.0.1
          org.apache.commons.httpclient.cookie 3.0.1
          org.apache.commons.httpclient.params 3.0.1
          org.apache.commons.httpclient.util 3.0.1
          org.apache.commons.httpclient.methods.multipart 3.0.1
          org.apache.commons.httpclient 3.0.1
      Imported Packages:
          javax.crypto 0.0.0
          javax.crypto.spec 0.0.0
          javax.net 0.0.0
          javax.net.ssl 0.0.0
          org.apache.commons.codec [1.3.0,2)
          org.apache.commons.codec.binary [1.3.0,2)
          org.apache.commons.codec.net [1.3.0,2)
          org.apache.commons.httpclient 3.0.1
          org.apache.commons.httpclient.auth 3.0.1
          org.apache.commons.httpclient.cookie 3.0.1
          org.apache.commons.httpclient.methods 3.0.1
          org.apache.commons.httpclient.methods.multipart 3.0.1
          org.apache.commons.httpclient.params 3.0.1
          org.apache.commons.httpclient.protocol 3.0.1
          org.apache.commons.httpclient.util 3.0.1
          org.apache.commons.logging 0.0.0

  bundles org.osgeye
  
  org.osgeye 0.0.1
      ID: 13
      Type: Normal
      State: Active
      Last Modified: 12/06/09 10:05:53
      Location: file:////Users/baswerc/libs/org.osgeye-0.0.1.jar
      Start Level: 3
      Services:
          org.osgi.service.cm.ManagedService
          org.osgi.service.cm.ConfigurationListener
      Imported Packages:
          javax.management 0.0.0
          javax.naming 0.0.0
          org.osgi.framework 0.0.0
          org.osgi.service.cm 0.0.0
          org.osgi.service.log 0.0.0
          org.osgi.service.packageadmin 0.0.0
          org.osgi.service.startlevel 0.0.0
          org.slf4j 0.0.0
```
