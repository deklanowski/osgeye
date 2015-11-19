format:

`missing <bundle name pattern>? <version range>? <type>? <file pipe>?`

options:

  * `<bundle name pattern>` - The optional pattern used to match against bundles' symbolic name. All matched bundles will be included in the output. If no pattern is specified or `*` all bundles will be used. For details on what regular expression rules can be used see http://java.sun.com/j2se/1.5.0/docs/api/java/util/regex/Pattern.html#sum.

  * `<version range>` - The optional version range that matched bundle versions must fall within to be included in the output. If no version range is specified or `*` all bundle versions will be used. The version range can include a floor and a ceiling (ex. "[2.2.3,3.1.0)") that bundle versions must fall within to be included or just a version value (ex. "2.2.3") that bundle version must equal to be included.

  * `<type>` - The resolution to include for missing packages. If "optional" then only missing package with a resolution of optional will be printed. If "mandator" then only missing packages with a resolution of required will be printed. If "all" (the default) then both types will be printed.

  * `<file pipe>` - The output of this command can be piped to a file by using the syntax "> file path" as the last argument.

output:

Each bundle that matches the given the parameters and has missing packages will be printed out. Underneath each bundle a list of packages that are missing (i.e. aren't wired) will be listed.

  * Bundle Symbolic Name, Bundle Version Number, "(" Bundle State ")"
    * Missing Import Package, Import Version Range, "?" (if import is optional)

examples:
```
    > missing ojdbc14 
    
    ojdbc14 10.2.0.4 (ACTIVE)
        oracle.i18n.text 0.0.0 ?
        oracle.i18n.text.converter 0.0.0 ?
        oracle.ons 0.0.0 ?
        oracle.security.pki 0.0.0 ?

    > missing * * mandatory 
    
    org.test.core.api 2.1.1 (INSTALLED)
        org.test.util.collections 0.0.0
    
    org.test.core.impl 2.0.2 (INSTALLED)
        org.test.core [2.0.0,3.0.0)
        org.test.core.configuration [2.0.0,3.0.0)
        org.test.core.context [2.0.0,3.0.0)
        org.test.core.data.access.jdbc [2.0.0,3.0.0)
        org.test.core.data.models [2.0.0,3.0.0)
        org.test.core.data.registries [2.0.0,3.0.0)
        org.test.core.util.time [2.0.0,3.0.0)
        org.test.util [1.0.0,2.0)
        org.test.util.cipher [1.0.0,2.0)
        org.test.util.data [1.0.0,2.0)
```