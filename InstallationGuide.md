# OSGEye Installation Guide #

OSGEye is a set of management tools for <a href='http://www.osgi.org/Main/HomePage'>OSGi</a> based platforms. Once installed OSGEye features can be accessed from a command line or <a href='http://java.sun.com/javase/technologies/core/mntr-mgmt/javamanagement/'>JMX</a>.

## Installing The OSGEye Bundle ##

Installing the OSGEye server is accomplished by deploying and starting the OSGEye bundle (org.osgeye-${version}.jar) into your OSGi runtime. Once this bundle starts up it will startup the network server that the command line client can connect to. It will also add OSGEye MBeans for JMX management to the platform's default <a href='http://java.sun.com/j2se/1.5.0/docs/api/javax/management/MBeanServer.html'>MBeanServer<a />.<br>
<br>
<h3>Bundle Requirements</h3>

The OSGEye bundle requires a 5.0 or greater JVM and a 4.1 or greater OSGi implementation. The following OSGi framework services must be available for the bundle to properly function (the bundle will startup fine without these but they must be available for the first client request):<br>
<br>
<ul><li><a href='http://www.osgi.org/javadoc/r4v41/org/osgi/service/cm/ConfigurationAdmin.html'>ConfigurationAdmin</a>
</li><li><a href='http://www.osgi.org/javadoc/r4v41/org/osgi/service/packageadmin/PackageAdmin.html'>PackageAdmin</a>
</li><li><a href='http://www.osgi.org/javadoc/r4v41/org/osgi/service/startlevel/StartLevel.html'>StartLevel</a></li></ul>

The OSGEye bundle has one external requirement (that may not already be supplied by your system bundle) <a href='http://www.slf4j.org/'>SLF4J</a>. If your OSGI runtime does not already export the SLF4J api packages be sure to install the slf4j-api-1.5.10.jar and slf4j-simple-1.5.10 bundles before you install the OSGEye bundle (these are part of the OSGEye download distribution).<br>
<br>
<h2>Installing The Command Line Client</h2>

The command line client is a self contained executable jar file org.osgeye.console-${version}.jar. To execute this client run the command:<br>
<br>
<code>java -jar org.osgeye.console-${version}.jar</code>

<h3>Command Line Client Requirements</h3>

The OSGEye command line client requires a 5.0 or greater JVM to run in.