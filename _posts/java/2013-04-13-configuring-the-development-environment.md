---
layout: post
title: "Configuring the Development Environment"
description: "The purpose of this article is to establish a continuous integrated development environment. The main tools include JDK, Jenkins, Maven, Tomcan, Mysql, Mongodb, and SVN."
category: java
tags: [ubuntu, java, jdk, jre, development environment, jenkins, maven, tomcat, mysql,mongodb, svn]
---
{% include JB/setup %}

The purpose of this article is to establish a continuous integrated development environment. The main tools include JDK, Jenkins, Maven, Tomcan, Mysql, Mongodb, and SVN.

#  Ubuntu 12.04 LTS

## Environment Variables

Environment variables provide a way to influence the behaviour of software on the system.

###Setting values to environment variables
    LANG=en_US.UTF-8
    
    EDITOR=nano
    export EDITOR
    
    export EDITOR=nano

###Examining values of enviroment variables
    printenv                    # prints all currently defined environment variables
    printenv TERM               # print TERM
    echo $TERM

###Erasing environment variables
    export LC_ALL=
    unset LC_ALL
    export -n LC_ALL

###Session-wide environment variables
    ~/.profile                  # It gets executed automatically by the DisplayManager during the start-up process desktop session as well as by the login shell when one log-in from the textual console.
    ~/.bash_profile             # whent it is started as a login shell. won't influence a graphical session by default.
    ~/.bashrc                   # this file will be executed in each an every invocation of bash as well as while logging in to the graphical environment.

###System-wide environment variables
    /etc/environment            # Specifically, this file stores the system-wide locale and path settings.
    /etc/profile                # This file gets executed whenever a bash login shell is entered, as well as by the DisplayManager when the desktop session loads.
    /etc/bash.bashrc - This is the system-wide version of the ~/.bashrc file. Ubuntu is configured by default to execute this file whenever a user enters a shell or the desktop environment.

(Read more: <https://help.ubuntu.com/community/EnvironmentVariables>)

## Java Development Environment Configuration

First, downloads [Java SE 6](http://www.oracle.com/technetwork/java/javasebusiness/downloads/java-archive-downloads-javase6-419409.html), choose the stable version--[jdk1.6.0_32](http://download.oracle.com/otn/java/jdk/6u32-b05/jdk-6u32-linux-i586.bin).
    
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

Type java -version, and press Enter, you'll see:

    $ java -version
    java version "1.6.0_32"
    Java(TM) SE Runtime Environment (build 1.6.0_32-b05)
    Java HotSpot(TM) Client VM (build 20.7-b02, mixed mode, sharing)

If you can see the above contents, congratulations! It means that you successfully configured the Java development environment.

## Sonatype Nexus
Download nexus from <http://www.sonatype.org/nexus>.

###Setup environment variable

    $ sudo gedit /etc/profile
    export NEXUS_HOME=/data/ubuntu/nexus/nexus-2.1.1
    export PATH=$NEXUS_HOME/bin:$PATH
    $ source /etc/profile
    
###Run

    $ nexus start
    
###Create system service

    $ cd etc/init.d
    $ sudo cp $NEXUS_HOME/../nexus
    $ sudo update-rc.d nexus
    $ sudo service nexus start

###shell nexus

    # Add some variables
    NEXUS_HOME=/data/ubuntu/nexus/nexus-2.1.1
    JAVA_HOME=/data/ubuntu/jdk/jdk1.6.0_32
    PATH=$JAVA_HOME/bin:$PATH

    # NOTE - This will set the user which is used to run the Wrapper as well as
    #  the JVM and is not useful in situations where a privileged resource or
    #  port needs to be allocated prior to the user being changed.
    RUN_AS_USER=cbay

    # Application
    APP_NAME="nexus"
    APP_LONG_NAME="Sonatype Nexus"

    # Wrapper
    WRAPPER_CMD=$NEXUS_HOME/bin/jsw/linux-x86-32/wrapper
    WRAPPER_CONF=$NEXUS_HOME/bin/jsw/conf/wrapper.conf

    # Priority at which to run the wrapper.  See "man nice" for valid priorities.
    #  nice is only used if a priority is specified.
    PRIORITY=

    # Location of the pid file.
    #PIDDIR="."
    PIDDIR=$NEXUS_HOME/../run

(Read more: <http://www.codesky.net/article/201202/172819.html>)

###Update maven repository index
    1. Downloads http://repo1.maven.org/maven2/.index/nexus-maven-repository-index.gz
    2. Stop nexus
    3. Delete all files in sonatype-work\nexus\indexer\central-ctx
    4. Unzip nexus-maven-repository-index.zip to sonatype-work\nexus\indexer\central-ctx
    5. Restart nexus to update automatically index

(Readmore: <http://blog.sina.com.cn/s/blog_604c7cdd0101c5v5.html>)

###9 Reasons to use Sonatype Nexus
    1. Nexus is Easy to Install
    2. Hosting Public Repositories
    3. Ability to Host Internal Artifacts
    4. Ability to Deploy 3rd-party Artifacts
    5. More Control Over Dependencies
    6. Greater Self-reliance/Stability
    7. Reduce the Burden on Central
    8. Save Yourself some Bandwidth
    9. Speed up Your Builds

## Maven Environment Configuration

    $ tar -xzvf apache-maven-3.0.4-bin.tar.gz       # unzip the package
    $ sudo gedit /etc/profile                       # setup environment variable
    export MAVEN_HOME=/data/ubuntu/maven/apache-maven-3.0.4
    export MAVEN_OPTS="-Xms256m -Xmx512m"
    export PATH=$JAVA_HOME/bin:$MAVEN_HOME/bin:$PATH
    $ source /etc/profile                           # 
    $ mvn -version                                  # verify that the configuration was successful.

(Read more: <http://blog.csdn.net/s_niper/article/details/6621019>)

###Configure settings.xml
$M2_HOME/conf/settings.xml

    <servers>
    <server>
        <id>nexus-snapshots</id>
        <username>deployment</username>
        <password>deployment</password>
    </server>
    <server>
        <id>nexus-releases</id>
        <username>deployment</username>
        <password>deployment</password>
    </server>
    </servers>

    <mirrors>
    <mirror>
        <id>nexus</id>
        <name>Internal Nexus Repository</name>
        <url>http://192.168.2.10:7076/nexus/content/groups/public/</url>
        <mirrorOf>central</mirrorOf>
    </mirror>
    </mirrors>

(Read more: <http://www.iteye.com/topic/1126678>)

###Q&A
1. Failure to find net.sf:pinyin4j:jar:2.5.0 in http://repo.maven.apache.org/maven2.

    Download pinyin4j-2.5.0.jar
    $ mvn install:install-file -DgroupId=net.sf -DartifactId=pinyin4j -Dversion=2.5.0 -Dpackaging=jar -DgeneratePom=true -DcreateChecksum=true -Dfile=./pinyin4j-2.5.0.jar

(Read more: <http://blog.csdn.net/jiushuai/article/details/7919793>)

2. Failure to find com.oracle:ojdbc14:jar:10.2.0.4.0 in http://repo.maven.apache.org/maven2.

    Download ojdbc14-10.2.0.4.0.jar
    $ mvn install:install-file -DgroupId=com.oracle -DartifactId=ojdbc14 -Dversion=10.2.0.4.0 -Dpackaging=jar -DgeneratePom=true -DcreateChecksum=true -Dfile=./ojdbc14-10.2.0.4.0.jar

(Read more: <http://lowkeyfeng.iteye.com/blog/907148>)

## Mysql Configuration

###Install MySQL
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

###Start MySQL service
    $ sudo bin/mysqld_safe --user=mysql &       # start mysql service
    $ sudo service mysqld start                 # start mysql
    $ ps -A | grep mysql                        # list mysql processes
    $ netstat -atln                             # list ip ports
    $ sudo netstat -tap | grep mysql            # list mysql ip port

###Create super user
    $ sudo bin/mysqladmin -u root password 'new-password'
    $ sudo bin/mysql -u root -p
    mysql>CREATE USER 'cbay'@'localhost' IDENTIFIED BY 'cbay';
    mysql>GRANT ALL PRIVILEGES ON *.* TO 'cbay'@'localhost' WITH GRANT OPTION;
    mysql>CREATE USER 'cbay'@'%' IDENTIFIED BY 'cbay';
    mysql>GRANT ALL PRIVILEGES ON *.* TO 'cbay'@'%' WITH GRANT OPTION;
    mysql>exit

    The 'cbay'@'localhost' account can be used only when connecting from the local host. The 'cbay'@'%' account uses the '%' wildcard fro the host part, so it can be used to connect from any host.

Readmore:

- <http://dev.mysql.com/doc/refman/5.5/en/binary-installation.html>
- <http://lingshaohuprose.blog.163.com/blog/static/16957978220122844024875>
- <http://www.linuxidc.com/Linux/2012-08/68615.htm>
- <http://www.linux265.com/blog/index.php/archives/453>

###Common Commands
    $ mysql -u username -p password             # login
    $ mysql -u username -p
    $ mysql -h localhost -u username -p
    $ mysql -h 192.168.0.100 -u username -p
    
    mysql> show database;
    mysql> create database db_name;
    mysql> drop database db_name;
    mysql> use db_name;
    mysql> show tables;
    mysql> describe tb_name;                 # display table structure
    mysql> create table tb_name;
    mysql> drop table tb_name;
    mysql> insert into tb_name values("Johnny","Zhang");
    mysql> update tb_name set sex="male" where name='Zhang';
    mysql> select * from tb_name;
    mysql> delete from tb_name where ...
    mysql> exit
    
    $ mysqladmin -u username -p old_password -password new_password
    $ mysql -u username -p db_name < db_name.sql        # import from db_name.sql
    
    mysql> use db_name;
    mysql> source < db_name.sql                         # import from db_name.sql
    
    $ mysql -u username -p db_name > db_name.sql        # backup database db_name
    
    # Dumping data with mysqldump
    $ mysqldump [arguments] > filename
    $ mysqldump --all-databases > dump.sql
    $ mysqldump --databases db1 db2 db3 > dump.sql
    $ mysqldump --databases test > dump.sql             # the dump output contains CREATE DATABASE and USE statements.
    $ mysqldump test > dump.sql                         # without --databases, no CREATE DATABASE or USE statements.

###Forgot password
    $ sudo /etc/init.d/mysqld stop              # Stop mysql
    $ sudo bin/mysqld_safe --skip-grant-tables  # Start mysql in safe mode
    $ mysql -uroot
    
    mysql> use mysql;
    mysql> update user set Password = PASSWORD('root') where User ='root';
    mysql> exit
    
    $ sudo /etc/init.d/mysqld restart

(Read more: <http://www.cnblogs.com/yuxc/archive/2012/07/25/2607587.html>)

###Create database by using command
    1.use channel
    echo "create database if not exists abcd character set utf8;" | mysql -u username -p password

    2. use here document
    mysql -u username -p password <<!
    create database if not exists abc character set utf8;
    !
    
    3. mysqladmin -h localhost(ip address) -u username -p password create db_name

(Read more: <http://bbs.csdn.net/topics/380238926>)

###emma--mysql GUI
    $ sudo apt-get install emma                         # Install emma
    $ sudo gedit /usr/share/emma/emmalib/__init__.py    # emma configure file
    
    "db_encoding": "latin1" --> "db_encoding": "utf8"   # change to utf8
    
    $ sudo gedit /usr/share/emma/emmalib/mysql_host.py    # set names utf8
    def _use_db(self, name, do_query=True):             # line 155
        if self.current_db and name == self.current_db.name: return    
        if do_query:     
            self.query("use `%s`" % name, False)    
            self.query("set names utf8",  False)        # add this line
        try:    
            self.current_db = self.databases[name]   

(Read more: <http://blog.csdn.net/lcz_ptr/article/details/7798510>)

  
###Q&A
1. bin/mysqld: error while loading shared libraries: libaio.so.1: cannot open shared object file: No such file or directory

####Solution
    $ sudo apt-get install libaio-dev
    
2. emma: Can't connect to local MySQL server through socket '/var/run/mysqld/mysqld.sock'

####Analysis of the causes
    You have started the mysqld server with the --socket=/path/to/socket option, but forgotten to tell client programs the new name of the socket file.

####Solution
    $ sudo gedit /usr/share/emma/emmalib/mysql_host.py  #def connect(self):
    
    def connect(self):
		c = {
			"host": self.host, 
			"user": self.user, 
			"passwd": self.password, 
			"unix_socket": '/tmp/mysql.sock',                 # add this line
			"connect_timeout": int(self.connect_timeout)
			}


Read more:

- <http://dev.mysql.com/doc/refman/5.6/en/can-not-connect-to-server.html>
- <http://www.cnblogs.com/trams/archive/2012/01/04/2311783.html>

3. can't import long script

####Analysis of the causes
    mysql>source data.sql      #size 99M
    Error
    
####Solution
    modify my.cnf
    max_allowed_packet=100M

(Read more: <http://www.hackbase.com/tech/2011-03-23/63052.html>)

###Appendix
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

## MongoDB configuration
Download [mongodb](http://www.mongodb.org/downloads)

    $ curl http://fastdl.mongodb.org/linux/mongodb-linux-i686-2.4.5.tgz

    $ tar -zxvf mongodb-linux-i686-2.4.5.tgz
    $ mkdir data
    $ mkdir log

###Setup environment variable
    $ sudo gedit /etc/profile
    export MONGO_HOME=/data/ubuntu/mongodb/mongodb-linux-i686-2.4.5
    export PATH=$MONGO_HOME/bin:$PATH
    $ source /etc/profile

###mongodb.conf
    dbpath=/data/ubuntu/mongodb/data/
    logpath=/data/ubuntu/mongodb/log/mongodb.log
    logappend=true
    port=27017
    fork=true
    noauth=true

###Run mongodb
    $ mongod -f /etc/mongodb.conf

###Use mongodb
    $ mongo
    > db.test.save({name:'admin'}) { "_id" : ObjectId("50d1440ef328346cb06c319f"), "name" : "admin" }
    > db.test.find()
    > db.test.remove()
    > db.test.find()

###Mongod--start shell
    #!/bin/sh

    . /lib/lsb/init-functions
    CONFIG="/etc/mongodb.conf"
    PROGRAM="/data/ubuntu/mongodb/mongodb-linux-i686-2.4.5/bin/mongod"
    MONGOPID=`ps -ef | grep 'mongod' | grep -v grep | awk '{print $2}'`

    test -x $PROGRAM || exit 0

    case "$1" in
    start)
    ulimit -n 3000
    log_begin_msg "Starting MongoDB Server"
    $PROGRAM -f $CONFIG &
    log_end_msg 0
    ;;
    stop)
    log_begin_msg "Stopping MongoDB Server"
    if [ ! -z "$MONGOPID" ]; then
    kill -15 $MONGOPID
    fi
    log_end_msg 0
    ;;
    *)
    log_success_msg "Usage:/etc/init.d/mongod {start|stop}"
    exit 1
    esac

    exit 0

####Setup boot start
    $ update-rc.d mongod defaults
    
    $ sudo service mongodb start
    $ sudo service mongodb stop
    $ /etc/init.d/mongodb start
    $ /etc/init.d/mongodb stop

(Read more: <http://blog.163.com/minhao_123/blog/static/12195262012111903242928/>)

## Github

###Install Git
    $ sudo apt-get install git git-core git-gui git-doc

###Configure Git
    $ ssh-keygen -t rsa -C "your_email@example.com"
    # Create a new ssh key (press Enter while need to type a passphrase)

    $ sudo apt-get install xclip
    # Install xclip

    $ xclip -sel clip < ~/.ssh/id_rsa.pub
    # Copy the contents to clipboard, add to github account setting.

    $ ssh -T git@github.com
    # Showing 'Hi username!' means you've successfully authenticated.

(Read more: <https://help.github.com/articles/generating-ssh-keys>)

    $ git config --global user.name "Your Name Here"
    # Set the default name for git to use when you commit

    $ git config --global user.email "your_email@example.com"
    # Set the email associated with your GitHub account

    $ git config --global credential.helper 'cache --timeout=3600'
    # Set the cache to timeout after 1 hour (setting is in seconds)
    
(Read more: <https://help.github.com/articles/set-up-git>)

###Commands
    $ git clone git@github.com:USERNAME/USERNAME.github.com.git # grap a complete copy
    $ cd USERNAME.github.com        # locate to blog
    $ git pull origin master        # fetch remote origin and merge it into local master
    $ git status                    # see the state of the project
    $ git add .                     # add unexisting files into remote
    $ git commit * -m "add comment" # add a comment
    $ git push origin master        # update to remote

    git clone URL                           # grab a complete copy of user's repository
    git://github.com/user/repo.git          # a read-only URL
    https://github.com/user/repo.git        # an HTTPS write-able URL
    git@github.com:user/repo.git            # a private SSH URL
    https://user@github.com/user/repo.git   # a private HTTPS URL

    git pull <REMOTENAME> <BRANCHNAME>      # fetch a specific branch and merge it into current local branch.

(Read more: <https://help.github.com/articles/fetching-a-remote>)

## RVM Ruby Jekyll

Use RVM to manage different version of ruby.

###Install RVM
    $ sudo apt-get install build-essential curl
    $ curl -L get.rvm.io | bash -s stable
    $ source ~/.bashrc
    $ source ~/.bash_profile

###Commands
    $ rvm list known            # list known ruby
    $ rvm install 1.9.3
    $ rvm use 1.9.3
    $ rvm use 1.9.3 --default   # set 1.9.3 as default
    $ rvm list                  # list installed ruby
    $ rvm remove 1.8.7
    
Read more:
- <http://ruby-china.org/wiki/rvm-guide>
- <http://www.cnblogs.com/keen-allan/archive/2012/04/22/2464541.html>

###Q&A
Q1.RVM is not a function, selecting rubies with 'rvm use ...' will not work.
    
A: This error happens because under RVM's installation directory (normally $HOME/.rvm/bin), there is an executable named 'rvm'; whereas under $HOME/.rvm/scripts directory, there is a script called 'rvm'. By default, the 'rvm' executable is used, which cannot handle many rvm commands such as 'rvm use'. 

One should load RVM into a shell session as a function (run the 'rvm' script). To do that, add the following line to '~/.bashrc':

    [[ -s "$HOME/.rvm/scripts/rvm" ]] && source "$HOME/.rvm/scripts/rvm" #Load RVM into a shell session as a function
    PATH=$PATH:$HOME/.rvm/bin #Add RVM to PATH for scripting
    
Open a new terminal or run the following command to reload /.bashrc in the current terminal. The problem should be solved.

    $ source ~/.bashrc

(Read more:<http://blog.sina.com.cn/s/blog_9d6e035501010lol.html>)

## Google Chrome
Download google chrome deb package:

- 32 bit: <https://dl.google.com/linux/direct/google-chrome-stable_current_i386.deb>
- 64 bit: <https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb>

    $ sudo dpkg -i google-chrome-stable_current_i386.deb

###Q&A
1. Dependency problems, uninstall libnss3-1d

A: Solve dependency problems.

    $ sudo apt-get -f install

(Read more: <http://hi.baidu.com/kevin276/item/29bc1c96a208fabc82d29542>)

## Appendix

###1. /etc/profile
    # configure environment variables
    # export JAVA_HOME=/data/ubuntu/jdk/jdk1.7.0_21
    export JAVA_HOME=/data/ubuntu/jdk/jdk1.6.0_32
    # export JAVA_OPTS="-Xms512m -Xmx768m -XX:PermSize=128m -XX:MaxPermSize=256m -XX:NewSize=128m -XX:MaxNewSize=256m"
    # export JRE_HOME=/data/ubuntu/jdk/jdk1.6.0_32/jre
    export MAVEN_HOME=/data/ubuntu/maven/apache-maven-3.0.5
    export MAVEN_OPTS="-Xms256m -Xmx512m -XX:PermSize=128m -XX:MaxPermSize=256m"
    export ANT_HOME=/data/ubuntu/ant/apache-ant-1.8.3
    export GRADLE_HOME=/data/ubuntu/gradle/gradle-1.6
    export NEXUS_HOME=/data/ubuntu/nexus/nexus-2.1.1
    export MYSQL_HOME=/home/cbay/mysql
    export SVN_HOME=/data/ubuntu/jdk/jdk1.6.0_32
    export CLASSPATH=.:$JAVA_HOME/lib:$CLASSPATH
    export PATH=$JAVA_HOME/bin:$MAVEN_HOME/bin:$ANT_HOME/bin:$GRADLE_HOME/bin:$NEXUS_HOME/bin:$MYSQL_HOME/bin:$PATH



