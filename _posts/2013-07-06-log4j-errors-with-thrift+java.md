---
layout: post
title: "Log4j errors with thrift+java"
excerpt: "Updated thrift recently, and found that afterwards"
tags: 
- development
- java-thrift
published: true
---

We updated thrift recently and found that afterwards some Java code was raising errors. It turns out that the latest Thrift release/head requires `log4j` but _doesn't_ complain about it.

### How we fixed it

Log4J can be obtained from: http://logging.apache.org/log4j/1.2/

    $ curl {LOG4J_MIRROR}/apache-log4j-1.2.15.tar.gz | tar zx
    $ mv apache-log4j-1.2.15 $JAVA_LIBS_DIR
    $ ln $JAVA_LIBS_DIR/apache-log4j-1.2.15 \
      $JAVA_LIBS_DIR/apache-log4j-latest
    $ ln $JAVA_LIBS_DIR/apache-log4j-latest/log4j-1.2.15.jar \
      $JAVA_LIBS_DIR/apache-log4j-latest/log4j.jar

Then set `$LOG4J_HOME` to the above folder and add the `$LOG4J_HOME/log4j.jar` to your `CLASSPATH`.

    $ cd ~/thrift
    $ echo "thrift.extra.cpath = $JAVA_LIBS_DIR/apache-log4j-latest/log4j.jar" \
      > ~/.thrift-build.properties
    $ ./bootstrap
    $ ./configure
    $ make && make install

`$JAVA_LIBS_DIR` is where we keep all our java libraries (`/opt/java/{pkg}`).
