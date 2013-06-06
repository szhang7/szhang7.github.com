---
layout: post
title: "Configuring the Development Environment"
description: "The purpose of this article is to establish a continuous integrated development environment. The main tools include JDK, Jenkins, Maven, Tomcan, Mysql, and SVN."
category: ubuntu
tags: [ubuntu, java, jdk, jre, development environment, jenkins, maven, tomcat, mysql, svn]
---
{% include JB/setup %}

# Configuring the Development Environment

The purpose of this article is to establish a continuous integrated development environment. The main tools include JDK, Jenkins, Maven, Tomcan, Mysql, and SVN.

## Java Development Environment Configuration

First, downloads [Java SE 6](http://www.oracle.com/technetwork/java/javasebusiness/downloads/java-archive-downloads-javase6-419409.html#jdk-6u22-oth-JPR), choose the stable version--[jdk1.6.0_32](http://download.oracle.com/otn/java/jdk/6u32-b05/jdk-6u32-linux-i586.bin).
    
Second, make directory /java/jdk, and unzip dk-6u32-linux-i586.bin to jdk, then you will get jdk1.6.0_32.

    $ sudo mkdir /java                 # make java folder
    $ sudo chown cbay:cbay /java       # change the owner and group of /java to cbay
    $ mkdir /java/jdk                  # make jdk folder in java
    $ cp ~/Downloads/jdk-6u32-linux-i586.bin /java/jdk
    $ cd /java/jdk
    cbay@ubuntu:/java/jdk$ tar -zxvf jdk-6u32-linux-i586.bin    # Extract all files
    
Third, edit /etc/profile to append some environment variables, save it and exit.

    $ sudo gedit /etc/profile
    append the following to the bottom.
    # configure jdk environment
    export JAVA_HOME=/java/jdk/jdk1.6.0_32
    export JRE_HOME=/java/jdk/jdk1.6.0_32/jre
    export CLASSPATH=.:$JAVA_HOME/lib:$JRE_HOME/lib:$CLASSPATH
    export PATH=$JAVA_HOME/bin:$JRE_HOME/bin:$PATH

Finally, source /etc/profile to make it take effect immediately, without having to restart the system.

Type java, and press Enter, you'll see:

    $ java
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

## Maven Environment Configuration

    $ tar -xzvf apache-maven-3.0.4-bin.tar.gz       # unzip the package
    $ sudo gedit /etc/profile                       # setup environment variable
    export MAVEN_HOME=/data/ubuntu/maven/apache-maven-3.0.4
    export MAVEN_OPTS="-Xms256m -Xmx512m"
    export PATH=$JAVA_HOME/bin:$MAVEN_HOME/bin:$PATH
    $ source /etc/profile                           # 
    $ mvn -version                                  # verify that the configuration was successful.
(Read more: <http://blog.csdn.net/s_niper/article/details/6621019>)

## Mysql Installation

To install and use a MySQL binary distribution, the basic command sequence looks like this:

    $ groupadd mysql
    $ useradd -r -g mysql mysql
    $ cd ~
    $ tar zxvf /path/to/mysql-VERSION-OS.tar.gz
    $ ln -s full-path-to-mysql-VERSION-OS mysql
    $ cd mysql
    $ mkdir tmp
    $ sudo chown -R mysql .
    $ sudo chgrp -R mysql .
    $ sudo scripts/mysql_install_db --user=mysql    # database empty
    $ sudo scripts/mysql_install_db --user=mysql --basedir=/home/zhang/mysql --datadir=/home/zhang/mysql/data       # Initialize database with user root
    $ sudo chown -R root .
    $ sudo chown -R mysql data tmp
    # Next command is optional
    $ sudo cp support-files/my-medium.cnf /etc/my.cnf
    $ sudo bin/mysqld_safe --user=mysql &
    # Next command is optional
    $ sudo cp support-files/mysql.server /etc/init.d/mysqld
    
    $ sudo bin/mysqld_safe --user=mysql &       # start mysql or
    $ sudo service mysqld start                 # start mysql
    $ ps -A | grep mysql                        # list mysql processes
    $ netstat -atln                             # check ip port
    
    $ sudo bin/mysqladmin -u root password 'new-password'
    $ sudo bin/mysql -u root -p
    mysql>CREATE USER 'cbay'@'localhost' IDENTIFIED BY 'cbay';
    mysql>GRANT ALL PRIVILEGES ON *.* TO 'cbay'@'localhost' WITH GRANT OPTION;
    mysql>CREATE USER 'cbay'@'%' IDENTIFIED BY 'cbay';
    mysql>GRANT ALL PRIVILEGES ON *.* TO 'cbay'@'%' WITH GRANT OPTION;
    mysql>exit
    
    mysql GUI
    $ sudo apt-get install emma                         # Install emma
    $ sudo gedit /usr/share/emma/emmalib/__init__.py    # emma configure file
    "db_encoding": "latin1" --> "db_encoding": "utf8"   # change to utf8
    
Readmore:
- <http://dev.mysql.com/doc/refman/5.5/en/binary-installation.html>
- <http://lingshaohuprose.blog.163.com/blog/static/16957978220122844024875>
- <http://www.linuxidc.com/Linux/2012-08/68615.htm>
- <http://www.linux265.com/blog/index.php/archives/453>
- <http://blog.csdn.net/lcz_ptr/article/details/7798510>

**Q&A**
    1. bin/mysqld: error while loading shared libraries: libaio.so.1: cannot open shared object file: No such file or directory
    $ sudo apt-get install libaio-dev
    
    2. emma: Can't connect to local MySQL server through socket '/var/run/mysqld/mysqld.sock'
    $ sudo mkdir /var/run/mysqld
    $ sudo ln -s /tmp/mysql.sock  /var/run/mysqld/mysqld.sock
    
    (Read more: <http://www.2cto.com/kf/201305/210034.html>)
    
**Appendix**
    my.cnf
    
    [client]
    #password	= your_password
    port		= 7077
    socket		= /tmp/mysql.sock
    default-character-set=utf8

    # Here follows entries for some specific programs

    # The MySQL server
    [mysqld]
    basedir = /home/zhang/mysql
    datadir = /home/zhang/mysql/data
    log-error = /home/zhang/mysql/data/error.log
    pid-file = /home/zhang/mysql/data/mysql.pid
    tmpdir = /home/zhang/mysql/tmp
    user = mysql
    collation-server=utf8_unicode_ci
    character-set-server=utf8
    #bind-address = 127.0.0.1
    bind-address = 0.0.0.0

    port		= 7077
    socket		= /tmp/mysql.sock
    skip-external-locking
    key_buffer_size = 16M
    max_allowed_packet = 1M
    table_open_cache = 64
    sort_buffer_size = 512K
    net_buffer_length = 8K
    read_buffer_size = 256K
    read_rnd_buffer_size = 512K
    myisam_sort_buffer_size = 8M
    
## SVN Client

    $ sudo apt-get install rapidsvn
    $ sudo apt-get install scite kdiff3
    View-->Preferences-->Programs
    Standard Editor: /usr/bin/SciTE
    Standard Explorer: /usr/bin/nautilus
    Diff Tool: /usr/bin/kdiff3
    Merge Tool: /usr/bin/kdiff3
    
(Read more: <http://www.cnblogs.com/end/archive/2012/11/22/2782241.html>)


