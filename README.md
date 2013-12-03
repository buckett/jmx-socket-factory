# jmx-socket-factory #

This is basically a way of binding the default JMX RMI server so that it listens on a specified interfaces rather than
all interfaces which is currently the default. To get this JAR to be used you need to add it to your bootclasspath.
Then you can specify the host that the RMI server should listen on.

    -Xbootclasspath/p:jmx-socket-factory.jar -Dcom.sun.management.jmxremote.host=127.0.0.1

## JDK 7 ##

On JDK 7 you get the option to specify the port with `-Dcom.sun.management.jmxremote.rmi.port`. Locking the port allows
you to tunnel the JMX connection over a SSH tunnel. So if you specify both `-Dcom.sun.management.jmxremote.rmi.port`
and -Dcom.sun.management.jmxremote.port you are all good.

## Changes in IP ##

On JDK 6 when the IP address changes on the machine running the JVM I am unable to connect to JMX through RMI.
Presumably because the IP referenced in the RMI connection is no longer valid. From [StackOverflow][1] it looks like:

> java.rmi.server.hostname: Hostname string; default value is the local host's IP address in "dotted-quad" format ...
> which is embedded into remote stubs created by this JVM when remote objects are exported. This can be used to control
> the effective IP address of RMI servers exported by multi-homed hosts. This property is read exactly once in the life
> of the JVM.

So the alternative way to fix the generated hostname for a laptop is to specify `-Djava.rmi.server.hostname`.

[1]: http://stackoverflow.com/questions/10173834/java-rmi-djava-rmi-server-hostname-localhost-still-opens-a-socket-listening-on 

