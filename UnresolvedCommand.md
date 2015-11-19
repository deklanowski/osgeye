format:

`unresolved <bundle name pattern>? <version range>? <type>? <file pipe>?`

options:

  * `<bundle name pattern>` - The optional pattern used to match against bundles' symbolic name. All matched bundles will be included in the output. If no pattern is specified or `*` all bundles will be used. For details on what regular expression rules can be used see http://java.sun.com/j2se/1.5.0/docs/api/java/util/regex/Pattern.html#sum.

  * `<version range>` - The optional version range that matched bundle versions must fall within to be included in the output. If no version range is specified or `*` all bundle versions will be used. The version range can include a floor and a ceiling (ex. "[2.2.3,3.1.0)") that bundle versions must fall within to be included or just a version value (ex. "2.2.3") that bundle version must equal to be included.

  * `<file pipe>` - The output of this command can be piped to a file by using the syntax "> file path" as the last argument.


see:

> http://blog.springsource.com/2008/10/20/understanding-the-osgi-uses-directive

output:

For each unresolved bundle that matches the given parameters its missing (mandatory) package imports and possible uses conflicts will be printed. The list of missing packages is formatted identical to the output from the missing command. For each possible uses conflict the first line will contain an import from the unresolved bundle. This is the import that a correctly versioned exported package was found for (but whose uses declaration caused trouble). Beneath the import line the "Exporting Bundle" and "Exported Package" describe the exported package for the import wiring. The "Exported Package Uses" describes a package used by the exported package that conflicts with the importing bundle's import list. The "Conflicting Import" is the import statement from the importing bundle that clashes with the exported package's uses statement. Hopefully you already understand this problem otherwise I'm sure this description won't make any sense.

  * Unresolved Bundle Symbolic Name, Unresolved Bundle Version Number
    * Missing Mandatory Package Imports:
      * Import Package Name, Import Package Version Range
    * Possible Uses Conflicts:
      * Import Package Name, Import Package Version Range
        * Exporting Bundle
        * Exported Package
        * Exported Package Uses
        * Conflicting Import

examples:
```
    > unresolved

    bundled 1.0.0
        Possible Uses Conflicts:
            org.test2 [1.0.0,2.0.0)
                Exporting Bundle: bundlec 1.0.0
                Exported Package: org.test2 1.0.0
                Exported Package Uses: org.test 1.0.0
                Conflicting Import: org.test [2.0.0,3.0.0)
    
    org.test.core.api 2.1.1
        Missing Package Imports:
            org.test.util.collections 0.0.0
    
    org.test.core.impl 2.0.2
        Missing Package Imports:
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