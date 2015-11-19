format:

`ls <type>? <pattern>?`

options:

  * `<type>` - The type to list. Either "bundles" or "services". If not specified "bundles" will be used as the default.

  * `<pattern>` - The name pattern used to match against. All matched names (either bundle symbolic name or service interface) will be included in the description. If no pattern is specified or `*` all bundles or service interfaces will be displayed. For details on what regular expression rules can be used see http://java.sun.com/j2se/1.5.0/docs/api/java/util/regex/Pattern.html#sum

output:

A list of bundle names or service interfaces. For bundles, each matching bundle's symbolic name and version will be outputed. For services, the class or interface the service was registered with will be outputed.

examples:
```
    > ls
    
    XmlSchema 1.3.2                                          annogen-0.1.0 0.1.0                                      axiom-api 1.2.5
    c3p0 0.9.1                                               com.springsource.edu.emory.mathcs.backport 3.0.0         com.springsource.javax.el 1.0.0
    com.springsource.javax.jms 1.1.0                         com.springsource.javax.mail 1.4.0                        com.springsource.javax.resource 1.5.0
    com.springsource.javax.servlet 2.5.0                     com.springsource.javax.servlet.jsp 2.1.0                 com.springsource.org.apache.commons.collections 3.2.0
    com.springsource.org.apache.commons.fileupload 1.2.0     com.springsource.org.apache.commons.io 1.4.0             commons-codec 1.3
    commons-compress 0.1.0.dev                               commons-httpclient 3.0.1                                 jakarta-httpcore 4.0.0.alpha2
    jaxen 1.1.0.beta-8                                       neethi 2.0.2                                             ojdbc14 10.2.0.4
    org.apache.servicemix.specs.jbi-api-1.0 1.0.0            org.eclipse.equinox.cm 1.0.0.v20080509-1800              org.eclipse.osgi 0.0.0
    org.osgeye 0.0.1                                         oscache-2.1.1 2.1.1                                      woden 1.0.0.M6
    woden-api 1.0.0.M6                                       wsdl4j 1.6.1                                             xercesImpl 2.8.1

    > ls bundles org.*
    
    org.apache.servicemix.specs.jbi-api-1.0 1.0.0   org.eclipse.equinox.cm 1.0.0.v20080509-1800     org.eclipse.osgi 0.0.0 
    org.osgeye 0.0.1

    > ls services

    javax.xml.parsers.SAXParserFactory                                          org.eclipse.osgi.framework.console.CommandProvider
    org.eclipse.osgi.framework.log.FrameworkLog                                 org.eclipse.osgi.internal.provisional.verifier.CertificateVerifierFactory
    org.eclipse.osgi.service.datalocation.Location                              org.eclipse.osgi.service.environment.EnvironmentInfo
    org.eclipse.osgi.service.localization.BundleLocalization                    org.eclipse.osgi.service.pluginconversion.PluginConverter
    org.eclipse.osgi.service.resolver.PlatformAdmin                             org.eclipse.osgi.service.security.TrustEngine
    org.eclipse.osgi.service.urlconversion.URLConverter                         org.eclipse.osgi.signedcontent.SignedContentFactory
    org.osgi.service.cm.ConfigurationAdmin                                      org.osgi.service.cm.ConfigurationListener
    org.osgi.service.cm.ManagedService                                          org.osgi.service.packageadmin.PackageAdmin
    org.osgi.service.startlevel.StartLevel
    
    > ls services javax.* 
    
    javax.xml.parsers.DocumentBuilderFactory   javax.xml.parsers.SAXParserFactory
```