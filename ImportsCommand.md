format:

`imports <bundle name pattern>? <version range>? <file pipe>? `

options:

  * `<bundle name pattern>` - The optional pattern used to match against bundles' symbolic name. All matched bundles will be included in the output. If no pattern is specified or `*` all bundles will be used. For details on what regular expression rules can be used see http://java.sun.com/j2se/1.5.0/docs/api/java/util/regex/Pattern.html#sum.

  * `<version range>` - The optional version range that matched bundle versions must fall within to be included in the output. If no version range is specified or `*` all bundle versions will be used. The version range can include a floor and a ceiling (ex. "[2.2.3,3.1.0)") that bundle versions must fall within to be included or just a version value (ex. "2.2.3") that bundle version must equal to be included.

  * `<file pipe>` - The output of this command can be piped to a file by using the syntax "> file path" as the last arguments.

output:

For each bundle that matches the imported packages for that bundle will be listed along with the bundle (if any) that this package is wired to.

  * Importing Bundle Symbolic Name, Importing Bundle Version Number
    * Imported Package Name, Import Version Range, "?" If Import Optional -> Wired Bundle Symbolic Name, Wired Bundle Version Number, "[" Exported Package Version "]"

examples:
```
    > imports org.test.bundle
    
    org.test.bundle 2.0.2
        com.mchange.v2.c3p0 [0.9.1,1.0.0) -> c3p0 0.9.1 [0.9.1]
        com.microsoft.sqlserver.jdbc 0.0.0 ? -> NOT WIRED
        com.mysql.jdbc [3.1.12,4.0.0) ? -> NOT WIRED
        org.test [2.0.0,3.0.0) -> org.test.bundle.api 2.1.1 [2.1.1]
        org.test.one [2.0.0,3.0.0) -> org.test.bundle.api 2.1.1 [2.1.1]
        org.test.two [2.0.0,3.0.0) -> org.test.bundle.api 2.1.1 [2.1.1]
        javax.management 0.0.0 -> org.eclipse.osgi 0.0.0 [0.0.0]
        javax.management.openmbean 0.0.0 -> org.eclipse.osgi 0.0.0 [0.0.0]
        javax.sql 0.0.0 -> org.eclipse.osgi 0.0.0 [0.0.0]
        javax.xml.namespace 0.0.0 -> org.eclipse.osgi 0.0.0 [0.0.0]
        oracle.jdbc.driver [10.2.0.1,11) ? -> ojdbc14 10.2.0.4 [10.2.0.4]
        org.apache.log4j [1.2.15,2) -> org.eclipse.osgi 0.0.0 [1.2.15]
        org.osgi.framework 0.0.0 -> org.eclipse.osgi 0.0.0 [1.4.0]
        org.osgi.service.cm 0.0.0 -> org.eclipse.osgi 0.0.0 [1.2.0]
```