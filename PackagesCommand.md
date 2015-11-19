format:

`packages <package name pattern>? <file pipe>?`

options:

  * `<package name pattern>` -  The optional pattern used to match against package names. All matched packages will be included in the output. If no pattern is specified or `*` all packages will be used. For details on what regular expression rules can be used see http://java.sun.com/j2se/1.5.0/docs/api/java/util/regex/Pattern.html#sum.

  * `<file pipe>` - The output of this command can be piped to a file by using the syntax "> file path" as the last arguments.

output:

A list of all exported packages whose package name matches the given pattern. Under each exported package will be a list of the bundles that are currently wired to this exported package (if any). Bundles that import a matching package but are not wired to any other bundle for this package will be displayed last under the "NOT WIRED" header.

  * Package Name
    * Exported Package Version - Exporting Bundle Symbolic Name, Exporting Bund Version
      * Wired Importing Bundle Symbolic Name, Wired Importing Bundle Version, Wired Import Version Range

examples:
```
    > packages oracle.jdbc.driver                
    
    oracle.jdbc.driver
        10.2.0.4 - ojdbc14 10.2.0.4
            org.test.bundlea 2.0.2 [10.2.0.1,11)
            c3p0 0.9.1 [10.2.0.1,10.3)
        NOT WIRED
            org.test.bundleb 1.0.0 [10.2.0.1,10.3)
```