format:

`states <bundle state>* <file pipe>?`

options:

  * `<bundle state>` - One or more bundle states to include in the list. If not specified all bundle states will be used which include:
    * Active - The bundle is now running.
    * Starting - The bundle is in the process of starting.
    * Stopping - The bundle is in the process of stopping.
    * Resolved - The bundle is resolved and is able to be started.
    * Installed - The bundle is installed but not yet resolved.
    * Uninstalled - The bundle is uninstalled and may not be used.

  * `<file pipe>` - The output of this command can be piped to a file by using the syntax "> file path" as the last arguments.

output:

States that match a specified bundle state but that do not have bundles in this status will not be printed.

  * Bundle State
    * Bundle Symbolic Name, Bundle Version Number

examples:
```
    > states
    
    Resolved
        fragmentBundle 1.0.0
    
    Installed
        bundleD 1.0.0
    
    Active
        XmlSchema 1.3.2
        annogen-0.1.0 0.1.0
        axiom-api 1.2.5
        axiom-impl 1.2.5
        axis2-kernel 1.3
        bundlea 1.0.0
        bundleb 2.0.0
        bundlec 1.0.0
        c3p0 0.9.1
        com.springsource.edu.emory.mathcs.backport 3.0.0
        com.springsource.javax.el 1.0.0
        com.springsource.javax.jms 1.1.0
        com.springsource.javax.mail 1.4.0
        com.springsource.javax.resource 1.5.0
        com.springsource.javax.servlet 2.5.0
        com.springsource.javax.servlet.jsp 2.1.0
        com.springsource.org.apache.commons.collections 3.2.0
        com.springsource.org.apache.commons.fileupload 1.2.0
        com.springsource.org.apache.commons.io 1.4.0
        commons-codec 1.3
        commons-compress 0.1.0.dev
        commons-httpclient 3.0.1
        jakarta-httpcore 4.0.0.alpha2
        jaxen 1.1.0.beta-8
        neethi 2.0.2
        ojdbc14 10.2.0.4
        org.apache.servicemix.specs.jbi-api-1.0 1.0.0
        org.eclipse.equinox.cm 1.0.0.v20080509-1800
        org.eclipse.osgi 0.0.0
        org.osgeye 0.0.1

    > states Resolved Installed 
    
    Resolved
        fragmentBundle 1.0.0
    
    Installed
        bundleD 1.0.0
```