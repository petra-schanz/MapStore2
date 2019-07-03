# LDAP integration with MapStore

The purpose of this guide is explain how to configure MapStore to allow users to login using LDAP credentials and setup maps permissions based on LDAP user groups.

## General

Configuring MapStore to use LDAP means to synchronize it's back-end users database with LDAP.

MapStore back-end is also known as [GeoStore](https://github.com/geosolutions-it/geostore).
To configure LDAP with GeoStore you can follow the [Wiki page](https://github.com/geosolutions-it/geostore/wiki/LDAP-Authentication) editing a file called `geostore-spring-security.xml`.

The easier way to configure it in mapstore is to follow the [instructions]((https://github.com/geosolutions-it/geostore/wiki/LDAP-Authentication)) linked above for GeoStore editing the `geostore-spring-security.xml` file inside the final war file.

All the following considerations regard the possibility to set-up LDAP configuration in a custom project and externalizing your secrets credentials.

## Override configuration

MapStore uses the [maven-war-plugin](https://maven.apache.org/plugins/maven-war-plugin/) to include GeoStore as back-end. This means that it merges all the resources coming from the geostore.war with the files generated by it's pom (as configured in `src/pom.xml`), included `geostore-spring-security.xml`.

To overwrite the spring security file coming from geostore you have simply to save your new `geostore-spring-security.xml`, modified using the guide above, in `web/src/resources`. Running the build your final war package will contain your new file instead of the GeoStore's one.

Some advanced configuration can use maven's copy-resources + filters to replace secrets stored in an external file and set username and password inside the spring-security context.
This is a typical setup when you need to use version control (git) + continuous integration.