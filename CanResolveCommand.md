format:

`canresolve <manifest or bundle file>`

options:

  * `<manifest or bundle file>` - The path to either a manifest file or a bundle jar file that contains a manifest file.

see:

> http://blog.springsource.com/2008/10/20/understanding-the-osgi-uses-directive

output:

If no conflicts were found for the given manifest file then a message will be printed that the bundle should be able to resolve. If missing packages or uses conflicts were found the following is printed out:

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
    > canresolve ../../Bundles/bundleD.jar 
    
    The following conflicts where found for bundleD
    
        Possible Uses Conflicts:
            org.test2 [1.0.0,2.0.0)
                Exporting Bundle: bundlec 1.0.0
                Exported Package: org.test2 v1.0.0
                Exported Package Uses: org.test v1.0.0
                Conflicting Import: org.test [2.0.0,3.0.0)

    > canresolve ../../Manifests/BundleE-MANIFEST.MF                 
    
    The following conflicts where found for bundleE
    
        Missing Mandatory Package Imports:
            org.yoyo.word 0.0.0

    > canresolve ../../Manifests/BundleA-MANIFEST.MF            
    
    No conflicts found. The bundle should resolve.
```