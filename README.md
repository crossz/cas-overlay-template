My Customization:

* cas-overlay-template
    https://github.com/crossz/cas-overlay-template
* docker using cas-overlay-template
    https://github.com/apereo/cas/tree/dockerized-caswebapp

### Notes:

1. build and run: mvn clean package jetty:run-forked
2. customized config in: 
    a) src/main/webapp/WEB-INF/ (for beans and property files location etc.)
    b) pom.xml ( for adding other jars: mysql-connector; cas-server-support-jdbc)

    this is the way of "mvn package", which will override these xml/proerties files in the war (cas-server-webapp is declared in the pom.xml); 

    So we just change the "src/main/webapp/WEB-INF/deployerConfigContext.xml" , then mvn clean package to create a new war and corresponding webapp.

3. copy own "etc" directory into /etc/cas, /etc/cas/jetty



CAS Overlay Template
============================

Generic CAS maven war overlay to exercise the latest versions of CAS. This overlay could be freely used as a starting template for local CAS maven war overlays. The CAS services management overlay is available [here](https://github.com/Jasig/cas-services-management-overlay).

# Versions
```xml
<cas.version>4.2.2</cas.version>
```

# Requirements
* JDK 1.7+

# Configuration

The `etc` directory contains the configuration files that need to be copied to `/etc/cas`.

Current files are:

* `cas.properties`
* `log4j2.xml`

# Build

```bash
mvnw clean package
```

or

```bash
mvnw.bat clean package
```

# Deployment

## Embedded Jetty

* Create a Java keystore at `/etc/cas/jetty/thekeystore` with the password `changeit`.
* Import your CAS server certificate inside this keystore.

```bash
mvnw jetty:run-forked
```

CAS will be available at:

* `http://cas.server.name:8080/cas`
* `https://cas.server.name:8443/cas`

## External
Deploy resultant `target/cas.war` to a Servlet container of choice.
