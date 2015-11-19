format:

`configs <filter>? <file pipe>?`

options:

  * `<filter>` - The filter string used to retrieve matching bundle configurations. This is the same filter used on the ConfigurationAdmin.listConfigurations and should be an LDAP type filter with the properties as parameters. If not specified all bundle configurations will be displayed.

  * `<file pipe>` - The output of this command can be piped to a file by using the syntax "> file path" as the last argument.

see:

<a href='http://www.osgi.org/javadoc/r4v41/org/osgi/service/cm/ConfigurationAdmin.html#listConfigurations(java.lang.String)'><code>http://www.osgi.org/javadoc/r4v41/org/osgi/service/cm/ConfigurationAdmin.html#listConfigurations(java.lang.String)</code></a>

output:

The details of each matching configuration.

  * PID - The PID for this configuration
  * Bundle Location - The bundle location this configuration is for.
  * Properties - List of properties for this configuration

examples:
```
    > configs

    PID: org.bundlea.Service-2.0.2
    Bundle Location: file:////usr/local/libs/bundlea-2.0.2.jar
    Properties:
        JDBC_USERNAME = usera
        MIN_POOL_SIZE = 1
        JDBC_URL = jdbc:oracle:thin:@database.com:1521:DB1
        JDBC_PASSWORD = passworda
        MAX_POOL_SIZE = 1
        JDBC_DRIVER_CLASS = oracle.jdbc.driver.OracleDriver
        service.pid = org.test.servicea-2.0.2
        SCHEMA_OWNER = schema

    PID: org.bundleb.Service-2.0.2
    Bundle Location: file:////usr/local/libs/bundleb-2.0.2.jar
    Properties:
        JDBC_USERNAME = userb
        MIN_POOL_SIZE = 1
        JDBC_URL = jdbc:oracle:thin:@database.com:1521:DB1
        JDBC_PASSWORD = passwordb
        MAX_POOL_SIZE = 1
        JDBC_DRIVER_CLASS = oracle.jdbc.driver.OracleDriver
        service.pid = org.test.serviceb-2.0.2
        SCHEMA_OWNER = schema

    > configs (&(JDBC_USERNAME=usera)(JDBC_PASSWORD=passworda))
    
    PID: org.bundlea.Service-2.0.2
    Bundle Location: file:////usr/local/libs/bundlea-2.0.2.jar
    Properties:
        JDBC_USERNAME = usera
        MIN_POOL_SIZE = 1
        JDBC_URL = jdbc:oracle:thin:@database.com:1521:DB1
        JDBC_PASSWORD = passworda
        MAX_POOL_SIZE = 1
        JDBC_DRIVER_CLASS = oracle.jdbc.driver.OracleDriver
        service.pid = org.test.service-2.0.2
        SCHEMA_OWNER = schema
```