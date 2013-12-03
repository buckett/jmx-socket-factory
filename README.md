# jmx-socket-factory #

This is basically a way of binding the default JMX RMI server so that it listens on a specified interfaces rather than
all interfaces which is currently the default. To get this JAR to be used you need to add it to your bootclasspath.
Then you can specify the host that the RMI server should listen on.

    -Xbootclasspath/p:jmx-socket-factory.jar -Dcom.sun.management.jmxremote.host=127.0.0.1

