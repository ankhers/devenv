[comment]: # (Do not edit this file as it is autogenerated. Go to docs/individual-docs if you want to make edits.)


[comment]: # (Please add your documentation on top of this line)

## services\.kafka\.enable



Whether to enable Apache Kafka\.



*Type:*
boolean



*Default:*
` false `



*Example:*
` true `



## services\.kafka\.package



The apacheKafka package to use\.



*Type:*
package



*Default:*
` pkgs.apacheKafka `



## services\.kafka\.configFiles\.log4jProperties

Kafka log4j property configuration file path



*Type:*
path



*Default:*
` "pkgs.writeText \"log4j.properties\" cfg.log4jProperties" `



## services\.kafka\.configFiles\.serverProperties



Kafka server\.properties configuration file path\.
Defaults to the rendered ` settings `\.



*Type:*
path



## services\.kafka\.defaultMode



Which defaults to set for the mode Kafka should run in

 - ` kraft ` (default): Run Kafka in KRaft mode, Which requires no extra configuration\.
 - ` zookeeper `: Run Kafka in Zookeeper mode, this requires more configuration\.



*Type:*
one of “zookeeper”, “kraft”



*Default:*
` "kraft" `



## services\.kafka\.formatLogDirs



Whether to format log dirs in KRaft mode if all log dirs are
unformatted, ie\. they contain no meta\.properties\.



*Type:*
boolean



*Default:*
` true `



## services\.kafka\.formatLogDirsIgnoreFormatted



Whether to ignore already formatted log dirs when formatting log dirs,
instead of failing\. Useful when replacing or adding disks\.



*Type:*
boolean



*Default:*
` true `



## services\.kafka\.jre



The JRE with which to run Kafka



*Type:*
package



*Default:*
` pkgs.apacheKafka.passthru.jre `



## services\.kafka\.jvmOptions



Extra command line options for the JVM running Kafka\.



*Type:*
list of string



*Default:*
` [ ] `



*Example:*

```
[
  "-Djava.net.preferIPv4Stack=true"
  "-Dcom.sun.management.jmxremote"
  "-Dcom.sun.management.jmxremote.local.only=true"
]
```



## services\.kafka\.log4jProperties



Kafka log4j property configuration\.



*Type:*
strings concatenated with “\\n”



*Default:*

```
''
  log4j.rootLogger=INFO, stdout
  
  log4j.appender.stdout=org.apache.log4j.ConsoleAppender
  log4j.appender.stdout.layout=org.apache.log4j.PatternLayout
  log4j.appender.stdout.layout.ConversionPattern=[%d] %p %m (%c)%n
''
```



## services\.kafka\.settings



[Kafka broker configuration](https://kafka\.apache\.org/documentation\.html\#brokerconfigs)
` server.properties `\.

Note that \.properties files contain mappings from string to string\.
Keys with dots are NOT represented by nested attrs in these settings,
but instead as quoted strings (ie\. ` settings."broker.id" `, NOT
` settings.broker.id `)\.



*Type:*
lazy attribute set of (null or boolean or signed integer or string or list of (boolean or signed integer or string))



*Default:*
` { } `



## services\.kafka\.settings\."broker\.id"



Broker ID\. -1 or null to auto-allocate in zookeeper mode\.



*Type:*
null or signed integer



*Default:*
` null `



## services\.kafka\.settings\.listeners



Kafka Listener List\.
See [listeners](https://kafka\.apache\.org/documentation/\#brokerconfigs_listeners)\.
If you change this, you should also update the readiness probe\.



*Type:*
list of string



*Default:*

```
[
  "PLAINTEXT://localhost:9092"
]
```



## services\.kafka\.settings\."log\.dirs"



Log file directories\.



*Type:*
list of path



*Default:*

```
[
  "/home/runner/work/devenv/devenv/.devenv/state/kafka/logs"
]
```