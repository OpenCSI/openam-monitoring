# OpenAM Monitoring 

This project is a WAR file to deploy on the **same container** than OpenAM.
The goal is to send JVM and OpenAM metrics to [Graphite](http://graphite.wikidot.com), which include:

* Tomcat servlets (for Tomcat 6 and 7)
* JVM Memory
* JVM Garbage collector
* OpenAM authentication (success and failures)
* OpenAM sessions

# Configuration

By default, data will be sends to localhost, port 2003. Console appender is disabled.

## Graphite

To configure where send data, create (or modify) ```$TOMCAT_HOME/bin/setenv.sh``` (make it executable) to have:

    CATALINA_OPTS+="-Dgraphite.host=graphite.example.com -Dgraphite.port=2003"

You can modify the [namePrefix](https://github.com/jmxtrans/embedded-jmxtrans/wiki/Graphite-Writer), default is ```jmx.#hostname#.``` 
If needed, you can disable graphite appender with ```-Dgraphite.enabled=false```.

## Console appender

To enable console appender (mainly for debug purposes), add ```-Dconsole.enabled=true``` to ```CATALINA_OPTS```. On Tomcat, logs will appears in ```catalina.log```. 

# Integration

![Grafana dashboard](https://github.com/OpenCSI/openam-monitoring/raw/master/src/site/screenshot.png)

## Grafana

Import the [dashboard](https://raw.githubusercontent.com/OpenCSI/openam-monitoring/master/src/site/grafana-openam-dashboard.json) into your kibana and adjust data to match your server or edit the file to replace ```jmx.sso``` by the correct prefix, like ```java.server```.
