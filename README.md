# Jetty Weld WAR Example

## Quick Start

### Jetty 12

#### Run

```shell
mvn package cargo:run
```

#### Debug

```shell
mvn package cargo:run -Dcargo.debug=true
```

This will add `-Xdebug -Xrunjdwp:transport=dt_socket,address=8000,server=y,suspend=y`.

#### Test

```shell
mvn verify
```

## Deploy

### Jetty 12

The `JETTY_BASE` needs to be set up with the following with the war deployed at `JETTY_BASE/webapp`.

```shell
cd $JETTY_BASE
java -jar $JETTY_HOME/start.jar --add-modules=http,ee10-deploy,ee10-annotations,ee10-websocket-jakarta,ee10-cdi-decorate
```

Currently Jetty 12 requires a custom `ServletContainerInitializer` to explicitly set the CDI Provider to the `WeldProvider` due to the following issue https://github.com/eclipse/jetty.project/issues/10150 as the presence of the `jakarta.enterprise.cdi-api` library in the Jetty classpath causes the `ServiceLoader` not to find the `WeldProvider`. This is implemented in `WeldServletContainerInitializer`.

## Starting

### Jetty 12

The server can be started with the following.
```shell
cd $JETTY_BASE
java -jar $JETTY_HOME/start.jar
```