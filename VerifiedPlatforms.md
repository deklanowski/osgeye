In theory OSGEye will work on any 4.1 compliant OSGi implementation running in a 5.0 JVM that supplies the following framework services:

  * [ConfigurationAdmin](http://www.osgi.org/javadoc/r4v41/org/osgi/service/cm/ConfigurationAdmin.html)
  * [PackageAdmin](http://www.osgi.org/javadoc/r4v41/org/osgi/service/packageadmin/PackageAdmin.html)
  * [StartLevel](http://www.osgi.org/javadoc/r4v41/org/osgi/service/startlevel/StartLevel.html)

In practice OSGEye has been verified on the following OSGi implementations:

  * [Equinox](http://www.eclipse.org/equinox/) - This is the platform that OSGEye has been tested on the most through the [Spring DM Server](http://www.springsource.com/products/dmserver) and by running equinox directly.
  * [Felix](http://felix.apache.org/site/index.html) - Has been verified through [ServiceMix4](http://servicemix.apache.org/SMX4/index.html) but not to the extent of equinox.