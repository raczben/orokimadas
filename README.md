# Örökimádás / Perpetual Adoration
Framework used for Perpetual Adoration in Hungary - Vác

Production instance is available here: http://orokimadas.magyar.website


## Development

### Requirements:
 - Git
 - Java JDK 17 (the current version) (can be downloaded within from IntelliJ)
 - IntelliJ IDEA Community Edition (can be downloaded from MS Store)
 - PSQL (database) https://www.postgresql.org/download/
 - MS Excel (or Libreoffice)
 - KeyStore Explorer (for generate https keys for local testing) https://keystore-explorer.org/downloads.html

### Set up

#### Setup JAVA

Add the bin directory (of the java runnable) to the PATH. (EX: `$HOME\.jdks\ms-11.0.28\bin`)

Set `JAVA_HOME` to the installed java directory. (EX: `$HOME\.jdks\ms-11.0.28`)

Otherwise, the build will fail with: 
```ERROR: JAVA_HOME is set to an invalid directory: C:\Users\raczb\.jdks\ms-11.0.28asd```

#### Build

Build command for official release: `./gradlew build release -P buildNumber=<build_number>`
Build command for testing: `./gradlew build release`

The build result will be generated in the `release` directory.

#### Run

You can launch the adoration webpage in different ways:
 - From commandline:
   - Enter the release directory (the build will generate it): `cd release`
   - Start the adoration webpage: `java -jar adoration-V2.1.SNAPSHOT.jar adoration.conf.properties`
 - From IntelliJ:
   - Menu -> Run -> Edit Configuration..., and set Path to JAR, Program arguments, and working directory

You will see a `ERROR StatusLogger Log4j2 could not find a logging implementation` error. You can ignore it.

#### Setting up the KeyStore


The adoration webpage uses [`https` protocol](https://www.cloudflare.com/learning/ssl/what-is-an-ssl-certificate/),
this means the launch will fail if you haven't got a valid SSL certificate (at least a locally).

For testing purposes you can bypass the SSL encripion by using a simple http connection:

Set property `isHttpsInUse=false` in `xxx.conf.properties`

For testing purposes you can generate certificate locally: all information can be found in the `./config/security/Readme.md` file.

For official release please contact a public certificate provider or your organisation's IT support.

If the adoration webpage cannot find the certificate, the following error will be printed:

`Application cannot be started: Jetty server cannot be started. Reason: ...\orokimadas\release\put keystore file here is not a valid keystore`

#### Setting up the SQL database

See [database config help](./config/database/README.md) to initialize the PSQL database.

If there is no database this message will be shown:
`ERROR SqlExceptionHelper Connections could not be acquired from the underlying database!`
Actual build status: [![Build](https://github.com/tkohegyi/orokimadas/actions/workflows/main.yml/badge.svg)](https://github.com/website-magyar/orokimadas/actions/workflows/main.yml)

Or if the user is not set well:
`Caused by: org.postgresql.util.PSQLException: FATAL: role "adorApp" is not permitted to log in`

Or if the database is not exist:
`Caused by: org.postgresql.util.PSQLException: FATAL: database "adoration_db" does not exist`

