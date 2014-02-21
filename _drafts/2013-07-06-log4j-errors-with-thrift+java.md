---
layout: post
title: "Log4j errors with thrift+java"
excerpt: "Updated thrift recently, and found that afterwards"
tags: 
- development
- java-thrift
published: true
---

Updated thrift recently, and found that afterwards some Java code borked. Turns out that the latest thrift release/head requires log4j but _doesn't_ complain about it.

This fixed things for me:

Log4J can be obtained from: http://logging.apache.org/log4j/1.2/

    ~# curl {LOG4J_MIRROR}/apache-log4j-1.2.15.tar.gz | tar zx
    ~# mv apache-log4j-1.2.15 $JAVA_LIBS_DIR
    ~# ln $JAVA_LIBS_DIR/apache-log4j-1.2.15 \
       $JAVA_LIBS_DIR/apache-log4j-latest
    ~# ln $JAVA_LIBS_DIR/apache-log4j-latest/log4j-1.2.15.jar \
       $JAVA_LIBS_DIR/apache-log4j-latest/log4j.jar

Then set $LOG4J_HOME to the above folder and add the $LOG4J_HOME/log4j.jar to your CLASSPATH.

    ~# cd ~/thrift
    ~# echo "thrift.extra.cpath = $JAVA_LIBS_DIR/apache-log4j-latest/log4j.jar" \
       > ~/.thrift-build.properties
    ~# ./bootstrap
    ~# ./configure
    ~# make && make install

<code>$JAVA_LIBS_DIR</code> is where I keep all my java libraries (/opt/java/{pkg}).

<del><strong>Update:</strong>
The latest release doesn't look to have this issue. An <code>svn up</code> might fix any issues you're having also.</del>

**Important:**
They have ***not*** removed the dependency, but *changed* it. I'll write up a new post soon with the changed routine, but in the meantime be warned that your java+thrift code will not work.
