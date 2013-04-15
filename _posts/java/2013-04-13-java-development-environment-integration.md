---
layout: post
title: "Java Development Environment Integration"
description: "The purpose of this article is to establish a continuous integrated java development environment. The main tools include JDK, Jenkins, Maven, Tomcan, Mysql, and SVN."
category: java
tags: [java, jdk, jre, development environment, jenkins, maven, tomcat, mysql, svn]
---
{% include JB/setup %}

The purpose of this article is to establish a continuous integrated java development environment. The main tools include JDK, Jenkins, Maven, Tomcan, Mysql, and SVN.

## Java Development Environment Configuration

First, downloads [Java SE 6](http://www.oracle.com/technetwork/java/javasebusiness/downloads/java-archive-downloads-javase6-419409.html#jdk-6u22-oth-JPR), choose the stable version--[jdk1.6.0_32](http://download.oracle.com/otn/java/jdk/6u32-b05/jdk-6u32-linux-i586.bin).
    
Second, make directory /java/jdk, and unzip dk-6u32-linux-i586.bin to jdk, then you will get jdk1.6.0_32.

    cbay@ubuntu:~$ sudo mkdir /java                 # make java folder
    cbay@ubuntu:~$ sudo chown cbay:cbay /java       # change the owner and group of /java to cbay
    cbay@ubuntu:~$ mkdir /java/jdk                  # make jdk folder in java
    cbay@ubuntu:~$ cp ~/Downloads/jdk-6u32-linux-i586.bin /java/jdk
    cbay@ubuntu:~$ cd /java/jdk
    cbay@ubuntu:/java/jdk$ tar -zxvf jdk-6u32-linux-i586.bin    # Extract all files
    
Third, edit /etc/profile to append some environment variables, save it and exit.

    cbay@ubuntu:~$ sudo gedit /etc/profile
    append the following to the bottom.
    # configure jdk environment
    export JAVA_HOME=/java/jdk/jdk1.6.0_32
    export JRE_HOME=/java/jdk/jdk1.6.0_32/jre
    export CLASSPATH=.:$JAVA_HOME/lib:$JRE_HOME/lib:$CLASSPATH
    export PATH=$JAVA_HOME/bin:$JRE_HOME/bin:$PATH

Finally, source /etc/profile to make it take effect immediately, without having to restart the system.

Type java, and press Enter, you'll see:

    cbay@ubuntu:~$ java
    Usage: java [-options] class [args...]
           (to execute a class)
    or  java [-options] -jar jarfile [args...]
           (to execute a jar file)

    where options include:
    -d32          use a 32-bit data model if available

    -d64          use a 64-bit data model if available
    -client	  to select the "client" VM
    -server	  to select the "server" VM
    -hotspot	  is a synonym for the "client" VM  [deprecated]
                  The default VM is client.
                  
    -cp <class search path of directories and zip/jar files>
    -classpath <class search path of directories and zip/jar files>
                  A : separated list of directories, JAR archives,
                  and ZIP archives to search for class files.
    -D<name>=<value>
                  set a system property
    -verbose[:class|gc|jni]
                  enable verbose output
    -version      print product version and exit
    -version:<value>
                  require the specified version to run
    -showversion  print product version and continue
    -jre-restrict-search | -jre-no-restrict-search
                  include/exclude user private JREs in the version search
    -? -help      print this help message
    -X            print help on non-standard options
    -ea[:<packagename>...|:<classname>]
    -enableassertions[:<packagename>...|:<classname>]
                  enable assertions
    -da[:<packagename>...|:<classname>]
    -disableassertions[:<packagename>...|:<classname>]
                  disable assertions
    -esa | -enablesystemassertions
                  enable system assertions
    -dsa | -disablesystemassertions
                  disable system assertions
    -agentlib:<libname>[=<options>]
                  load native agent library <libname>, e.g. -agentlib:hprof
                    see also, -agentlib:jdwp=help and -agentlib:hprof=help
    -agentpath:<pathname>[=<options>]
                  load native agent library by full pathname
    -javaagent:<jarpath>[=<options>]
                  load Java programming language agent, see java.lang.instrument
    -splash:<imagepath>
                  show splash screen with specified image

If you can see the above contents, congratulations! It means that you successfully configured the Java development environment.


