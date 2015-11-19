OSGEye provides management tools for your OSGi platform. For installation information and platform requirements see the [installation guide](InstallationGuide.md). OSGEye currently provides remote access for management through a command line client and JMX.

## OSGEye Bundle ##

The server piece of OSGEye is an OSGi bundle that must be installed into your OSGi runtime. Once installed, OSGEye starts up a network server that remote hosts (like the command line client) can connect to.  OSGEye bundle supports the following configuration properties:

  * host - The network host to accept client requests from. If not specified OSGEye will listen on all interfaces.

  * port- The network port to accept client requests from. If not specified OSGEye will attempt to use the default port 9999.

  * user - The user name used to authenticate client requests. If both user and password are specified authentication will be activated and clients will be required to pass these credentials before accessing the server services. **This does not secure JMX access. If you have activated remote JMX access in your system you must add security independent of OSGEye**.

  * password - The password used to authenticate client requests. If both user and password are specified authentication will be activated and clients will be required to pass these credentials before accessing the server services. **This does not secure JMX access. If you have activated remote JMX access in your system you must add security independent of OSGEye**.

The OSGEye bundle uses the configuration interfaces provided by the OSGi specification to receive this configuration. At startup, the bundle registers a [ManagedService](http://www.osgi.org/javadoc/r4v41/org/osgi/service/cm/ManagedService.html) with the service pid:

`org.osgeye.server.osgi-${bundle version`}

Use the [ConfigurationAdmin](http://www.osgi.org/javadoc/r4v41/org/osgi/service/cm/ConfigurationAdmin.html) to inject this service with configuration values. Every time OSGEye receives updated configuration information it restarts the network server with these new parameters (this means all connected clients will be disconnected).

## OSGEye Command Line ##

OSGEye provides a command line interface for interacting remotely with the server. The command line interface is contained within the executable jar file _org.osgeye.console-${version}.jar_. The command line interface can be started up by running:

`java -jar org.osgeye.console-${version}.jar <host> <port> <user> <password>`

This executes the main class `org.osgeye.console.OSGEyeConsole`. The arguments passed in include:

  * host - The host name of the server to connect to. This argument is required and if it's not provided the console will prompt you for this.

  * port - The port of the server to connect to. This argument is optional and if not provided the default port 9999 will be used.

  * user - The user name used to authenticate with the server. If not provided anonymous access will be attempted. If the user name is provided a password must be provided too.

  * password - The password used to authenticate with the server. If not provided anonymous success will be attempted.

An example login to the server is:

```
baswerc$ java -jar org.osgeye.console-0.0.1.jar localhost 9999 cbass yoyo    
OSGEye Console v0.0.1
Loading bundles. This may take a second or two...
Bundles are loaded. At anytime enter help for a list of available commands.

cbass@localhost:9999$ 
```

Once logged in you can execute the _help_ command to see what other commands are available.

```
cbass@localhost:9999$ help

OSGEye Console, v0.0.2
usage: <command> <options>
Type 'help <command>' for help on a specific command.

Available commands:
    
    Descrptions
        bundles         Prints details on matching bundles.
        configs         Prints configurations.
        exports         Displays the exported package wiring details for matching bundles.
        framework       Prints the current state of the OSGi framework.
        graph           Generates DOT based graphs.
        imports         Displays the imported package wiring details for matching bundles.
        ls              List the matching bundle or service names.
        manifest        Prints the manifest file for matching bundles.
        notifications   Prints OSGi notifications to the console.
        packages        Displays the wiring details for matching packages.
        services        List the matching service interfaces.
        states          List each bundle under its bundle state.
    
    Actions
        install         Installs a bundle on the remote server.
        refreshpacks    Forces the update (replacement) or removal of packages exported by the specified bundles.
        resolve         Resolves the specified bundles that are currently in the INSTALLED state.
        set             Sets OSGi framework and bundle properties.
        start           Starts the matching bundles.
        stop            Stops the matching bundles.
        uninstall       Uninstalls all matching bundles (after confirmation).
    
    Diagnosis
        canresolve      Attempts to determine if a manifest file can resolve against the current system.
        missing         Displays packages for bundles that are not wired.
        unresolved      Attempts to diagnose why bundles in the INSTALLED state weren't resolved.
    
    Miscellaneous
        clear           Clears the screen.
        exit            Exits from the console.
        help            Prints help for all commands.
        reload          Reloads all state stored by the console from the server.
```

### Tab Completion ###

The first thing the client does after login is to load the current state of the server. Having the full state of the server on the client allows tab completion to be enabled on most of the available commands. This works similar to tab completion in a bash shell where anytime you press tab OSGEye will attempt to complete as much of the remaining operation as it can.

For example, the `bundles` command prints out details about bundles in the system. It takes as its first argument the bundle name pattern to determine which bundles to print out. At the command prompt if you type the character _b_ and press the _tab_ button the console will automatically fill out the _bundles_ command since that's the only command that starts with _b_. If you then type _org_ and press _tab_ you might get something like:

```
cbass@localhost:9999$ bundles org.

org.eclipse.equinox.cm   org.eclipse.osgi         org.osgeye
cbass@localhost:9999$ bundles org.    
```

The first thing that happened was that the console supplied a _._ after the _org_ because all bundles in the system that start with _org_ also start with _org._ It then prints out as options the three bundles in the system that start with _org._ that you have to choose from. If you narrow down the name more by typing {{{org.eclipse}} and pressing _tab_ you will get:

```
cbass@localhost:9999$ bundles org.eclipse.

org.eclipse.equinox.cm   org.eclipse.osgi
cbass@localhost:9999$ bundles org.eclipse.
```

Tab completion works in almost all command scenarios for the console. If your ever unsure what to type next just press _tab_ and see what happens.

Special thanks to the awesome [JLine](http://jline.sourceforge.net/) project that makes the tab completion possible.

### Output To File ###

Many of the commands that print back status can optionally have their output written to a file instead of displayed on the console. This is accomplished by placing a _>_ on the end of the command and the path to the file to write to. For example the `manifest` command prints out the manifest file for matching bundles. If you wanted to print the manifest contents to a file instead of the screen do:

```
cbass@localhost:9999$ manifest org.osgeye > osgeye.mf      
```

This puts the contents of the _org.osgeye_ bundle's manifest file into the _osgeye.mf_ file. Unless an absolute path is specified the path will be relative to the directory that console was started in. Once you type the _>_ tab completion will be enabled for viewing what directories and files. Read the help details on each command to see which ones have this feature enabled (almost all the commands in the Description category supports this).

### Commands ###

The console commands are broken up into the following categories:

  * Descriptions - Commands that are read only that report back the state of the system.

  * Actions - Commands that attempt to change the state of the system.

  * Diagnosis - Commands that attempt to determine problems with the system.

  * Misc - Commands that don't really fall into any of the above categories.

#### Description Commands ####

  * [bundles](BundlesCommand.md)
  * [configs](ConfigsCommand.md)
  * [exports](ExportsCommand.md)
  * [framework](FrameworkCommand.md)
  * [graph](GraphCommand.md)
  * [imports](ImportsCommand.md)
  * [ls](LsCommand.md)
  * [manifest](ManifestCommand.md)
  * [notifications](NotificationsCommand.md)
  * [packages](PackagesCommand.md)
  * [services](ServicesCommand.md)
  * [states](StatesCommand.md)

#### Action Commands ####

  * [install](InstallCommand.md)
  * [refreshpacks](RefreshPacksCommand.md)
  * [resolve](ResolveCommand.md)
  * [set](SetCommand.md)
  * [start](StartCommand.md)
  * [stop](StopCommand.md)
  * [uninstall](UninstallCommand.md)

#### Diagnosis Commands ####
  * [canresolve](CanResolveCommand.md)
  * [missing](MissingCommand.md)
  * [unresolved](UnresolvedCommand.md)

#### Miscellaneous Commands ####

  * [clear](ClearCommand.md)
  * [exit](ExitCommand.md)
  * [help](HelpCommand.md)
  * [reload](ReloadCommand.md)

## OSGEye JMX ##

When the OSGEye bundle starts up it gets a reference to platform's default [MBeanServer](http://java.sun.com/javase/6/docs/api/javax/management/MBeanServer.html) (by calling [this method](http://java.sun.com/javase/6/docs/api/java/lang/management/ManagementFactory.html#getPlatformMBeanServer())) and adds MBeans for monitoring and managing your OSGi platform. OSGEye does not add any type of connectors to this MBeanServer for remote access. Providing remote, secure access to the MBeanServer must be done independently of OSGEye.

OSGEye adds all of its MBeans under the _org.osgeye_ domain. If you connect to a OSGEye managed runtime with JConsole you should see something like:

<br>
<img src='http://osgeye.org/images/jmx1.png' />
<br>

MBeans are provided for the following OSGi types:<br>
<br>
<ul><li>The Framework<br>
</li><li>Bundles<br>
</li><li>Services<br>
</li><li>Configuration</li></ul>

<h3>Framework MBean</h3>

The framework MBean has two readable and writable attributes:<br>
<br>
<ul><li>InitialBundleStartLevel - The start level assigned to newly installed bundles.<br>
</li><li>StartLevel - The currently start level of the framework.</li></ul>

<br>
<img src='http://osgeye.org/images/jmx2.png' />
<br>

<h3>Bundle MBeans</h3>

Every bundle installed in the OSGi runtime will get an associated MBean. The name of the MBean will be the bundle's symbolic name followed by the bundle's version number. Each bundle MBean has the following read only attributes:<br>
<br>
<ul><li>ExportedPackages - A list of packages and version numbers that this bundle exports.</li></ul>

<ul><li>Fragment - Boolean indicator is this bundle is a fragment or not.</li></ul>

<ul><li>Fragments - A list of bundles that are attached to this host bundle.</li></ul>

<ul><li>Headers - A map of strings containing the headers found in the bundle's manifest (see <a href='http://www.osgi.org/javadoc/r4v41/org/osgi/framework/Bundle.html#getHeaders()'>getHeaders()</a>).</li></ul>

<ul><li>Hosts - A list of bundles this fragment bundle is attached to.</li></ul>

<ul><li>Id - The bundle id (see <a href='http://www.osgi.org/javadoc/r4v41/org/osgi/framework/Bundle.html#getBundleId()'>getBundleId()</a>).</li></ul>

<ul><li>ImportedPackages - A list of packages and version ranges that this bundle imports.</li></ul>

<ul><li>LastModified - The date this bundle was last modified (see <a href='http://www.osgi.org/javadoc/r4v41/org/osgi/framework/Bundle.html#getLastModified()'>getLastModified()</a>).</li></ul>

<ul><li>Location - The install location of the bundle (see <a href='http://www.osgi.org/javadoc/r4v41/org/osgi/framework/Bundle.html#getLocation()'>getLocation()</a>).</li></ul>

<ul><li>StartLevel - The bundle's start level (see <a href='http://www.osgi.org/javadoc/r4v41/org/osgi/service/startlevel/StartLevel.html#getBundleStartLevel(org.osgi.framework.Bundle)'>getBundleStartLevel()</a>).</li></ul>

<ul><li>State - The bundle's current state. One of:</li></ul>

<ul><li>INSTALLED<br>
</li><li>RESOLVED<br>
</li><li>STARTING<br>
</li><li>ACTIVE<br>
</li><li>STOPPING</li></ul>

<ul><li>SymbolicName - The bundle's symbolic name (see <a href='http://www.osgi.org/javadoc/r4v41/org/osgi/framework/Bundle.html#getSymbolicName()'>getSymbolicName()</a>).</li></ul>

<ul><li>Version - The bundle's version.</li></ul>

<br>
<img src='http://osgeye.org/images/jmx3.png' />
<br>

Each bundle MBean provides the following operations:<br>
<br>
<ul><li>start() - Attempts to start the bundle if the bundle is not currently active (see <a href='http://www.osgi.org/javadoc/r4v41/org/osgi/framework/Bundle.html#start()'>start</a>).</li></ul>

<ul><li>start(int options) - Attempts to start the bundle with the provided options if the bundle is not currently active (see <a href='http://www.osgi.org/javadoc/r4v41/org/osgi/framework/Bundle.html#start(int)'>start(int)</a>).</li></ul>

<ul><li>stop() - Attempts to stop the bundle if the bundle is currently active (see <a href='http://www.osgi.org/javadoc/r4v41/org/osgi/framework/Bundle.html#stop()'>stop()</a>).</li></ul>

<ul><li>stop(int optiona) - Attempts to stop the bundle with the provided options if the bundle is currently active (see <a href='http://www.osgi.org/javadoc/r4v41/org/osgi/framework/Bundle.html#stop(int)'>stop(int)</a>).</li></ul>

<ul><li>resolve() - Attempts to resolve the bundle if the bundle is currently not resolved (see <a href='http://www.osgi.org/javadoc/r4v41/org/osgi/service/packageadmin/PackageAdmin.html#resolveBundles(org.osgi.framework.Bundle[])'>resolveBundles()</a>).</li></ul>

<ul><li>update() - Updates the bundle from either the <a href='http://www.osgi.org/javadoc/r4v41/org/osgi/framework/Constants.html#BUNDLE_UPDATELOCATION'>update bundle location</a> from the bundle's manifest (if available) or the bundle's original location (see <a href='http://www.osgi.org/javadoc/r4v41/org/osgi/framework/Bundle.html#update()'>update()</a>).</li></ul>

<ul><li>update(String bundleJarLocation) - Updates the bundle from the given path that points to jar file on the server side (see <a href='http://www.osgi.org/javadoc/r4v41/org/osgi/framework/Bundle.html#update(java.io.InputStream)'>update(InputStream)</a>).</li></ul>

<ul><li>refreshPackages() - Forces an update on packages exported by the given bundle (see <a href='http://www.osgi.org/javadoc/r4v41/org/osgi/service/packageadmin/PackageAdmin.html#refreshPackages(org.osgi.framework.Bundle[])'>refreshPackages()</a>).</li></ul>

<ul><li>uninstall() - Uninstalls the bundle (see <a href='http://www.osgi.org/javadoc/r4v41/org/osgi/framework/Bundle.html#uninstall()'>uninstall</a>).</li></ul>

<ul><li>viewManifest() - Returns the string content of the manifest file.</li></ul>

<br>
<img src='http://osgeye.org/images/jmx4.png' />
<br>

<h3>Service MBeans</h3>

Every service registered in the OSGi runtime will get an associated MBean. Underneath the Services folder of the OSGEye domain will be a list of all the interfaces and classes that services are registered with in the system. Underneath each interface or class will be a list of bundles that have registered services with the interface or class. Underneath the bundle name will be a list of the services registered with the service id used as the MBean name.<br>
<br>
Every service MBean will have the following attributes:<br>
<br>
<ul><li>Bundle - The bundle symbolic name that registered this service.</li></ul>

<ul><li>Id - The service ID.</li></ul>

<ul><li>Interface - The interface or class name this service is registered with.</li></ul>

<ul><li>Pid - The service pid used for configuration.</li></ul>

<ul><li>Ranking - The service ranking.</li></ul>

<br>
<img src='http://osgeye.org/images/jmx5.png' />
<br>

Every service MBean will have the following operations:<br>
<br>
<ul><li>description() - The service description.</li></ul>

<br>
<img src='http://osgeye.org/images/jmx6.png' />
<br>