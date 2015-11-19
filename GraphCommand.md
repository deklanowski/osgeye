format:

`graph <type> bundle name pattern> <version range> <report file>`

options:

  * `<type>` - Type type of graph to generate. One of:
    * fragments - Generates a graph showing bundle fragments dependencies.
    * packagewiring - Generates a graph showing package wiring dependencies between bundles.

  * `<bundle name pattern>`  The optional pattern used to match against bundles' symbolic name. All matched bundles will be included in the output. If no pattern is specified or `*` all bundles will be used. For details on what regular expression rules can be used see http://java.sun.com/j2se/1.5.0/docs/api/java/util/regex/Pattern.html#sum.

  * `<version range>` - The optional version range that matched bundle versions must fall within to be included in the output. If no version range is specified or `*` all bundle versions will be used. The version range can include a floor and a ceiling (ex. "[2.2.3,3.1.0)") that bundle versions must fall within to be included or just a version value (ex. "2.2.3") that bundle version must equal to be included.

  * `<report file>` - The dot file to generate.

see:

http://en.wikipedia.org/wiki/DOT_language

http://graphviz.org/

output:

Generates a dot file that can viewed by Graphviz (http://www.graphviz.org)

examples:
```
    > graph packagewiring org.* * report.dot 
```