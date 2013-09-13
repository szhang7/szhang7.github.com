---
layout: post
title: "Log4j Handbook"
description: "Log4j Handbook"
category: java
tags: [log4j, handbook, java, logging]
---
{% include JB/setup %}

## Introduction
Almost every large application includes its own logging or tracing API. In conformance with this rule, the E.U. SEMPER project decided to write its own tracing API. This was in early 1996. After countless enhancements, several incarnations and much work that API has evolved to become log4j, a popular logging package for Java. The package is distributed under the Apache Software License, a fully-fledged open source license certified by the open source initiative.

    Apache Log4j 2 is an upgrade to Log4j that provides significant improvements over its predecessor, Log4j 1.x, and provides many of the improvements available in Logback while fixing some inherent problems in Logback's architecture.

## Loggers, Appenders and Layouts
Log4j has three main components: loggers, appenders and layouts. These three types of components work together to enable developers to log messages according to message type and level, and to control at runtime how these messages are formatted and where they are reported.

###Loggers
    log4j.rootLogger=[level], appdendName1, appenderName2...

level is priorities: TRACE, DEBUG, INFO, WARN, ERROR, FATAL, OFF `TRACE < DEBUG < INFO < WARN < ERROR < FATAL < OFF`. Log4j recommends to use only four levels: DEBUG, INFO, WARN, ERROR.

####Basic Selection Rule
    A log request of level p in a logger with (either assigned or inherited, whichever is appropriate) level q, is enabled if p >= q.

###Appenders
Appenders are inherited additively from the logger hierarchy. Log4j allows logging requests to print to multiple destinations, which has five destinations:

    org.apache.log4j.ConsoleAppender
    org.apache.log4j.FileAppender
    org.apache.log4j.DailyRollingFileAppender
    org.apache.log4j.RollingFileAppender
    org.apache.log4j.WriterAppender

####ConsoleAppender
    Threshold=WARN:指定日志消息的输出最低层次。
    ImmediateFlush=true:默认值是true,意谓着所有的消息都会被立即输出。
    Target=System.err：默认情况下是：System.out,指定输出控制台

####FileAppender
    Threshold=WARN:指定日志消息的输出最低层次。
    ImmediateFlush=true:默认值是true,意谓着所有的消息都会被立即输出。
    File=mylog.txt:指定消息输出到mylog.txt文件。
    Append=false:默认值是true,即将消息增加到指定文件中，false指将消息覆盖指定的文件内容。

####DailyRollingFileAppender
    Threshold=WARN:指定日志消息的输出最低层次。
    ImmediateFlush=true:默认值是true,意谓着所有的消息都会被立即输出。
    File=mylog.txt:指定消息输出到mylog.txt文件。
    Append=false:默认值是true,即将消息增加到指定文件中，false指将消息覆盖指定的文件内容。
    DatePattern='.'yyyy-ww:每周滚动一次文件，即每周产生一个新的文件。当然也可以指定按月、周、天、时和分。即对应的格式如下：
    1)'.'yyyy-MM: 每月
    2)'.'yyyy-ww: 每周 
    3)'.'yyyy-MM-dd: 每天
    4)'.'yyyy-MM-dd-a: 每天两次
    5)'.'yyyy-MM-dd-HH: 每小时
    6)'.'yyyy-MM-dd-HH-mm: 每分钟

####RollingFileAppender
    Threshold=WARN:指定日志消息的输出最低层次。
    ImmediateFlush=true:默认值是true,意谓着所有的消息都会被立即输出。
    File=mylog.txt:指定消息输出到mylog.txt文件。
    Append=false:默认值是true,即将消息增加到指定文件中，false指将消息覆盖指定的文件内容。
    MaxFileSize=100KB: 后缀可以是KB, MB 或者是 GB. 在日志文件到达该大小时，将会自动滚动，即将原来的内容移到mylog.log.1文件。
    MaxBackupIndex=2:指定可以产生的滚动文件的最大数。

####Practical usage
    log4j.appender.A1=org.apache.log4j.ConsoleAppender //这里指定了日志输出的第一个位置A1是控制台ConsoleAppender

###Layouts
The PatternLayout, part of the standard log4j distribution, lets the user specify the output format according to conversion patterns similar to the C language printf function. 

    org.apache.log4j.HTMLLayout（以HTML表格形式布局），
    org.apache.log4j.PatternLayout（可以灵活地指定布局模式），
    org.apache.log4j.SimpleLayout（包含日志信息的级别和信息字符串），
    org.apache.log4j.TTCCLayout（包含日志产生的时间、线程、类别等等信息）
　　
####HTMLLayout 选项
    LocationInfo=true:默认值是false,输出java文件名称和行号
    Title=my app file: 默认值是 Log4J Log Messages.
    
####PatternLayout 选项
    ConversionPattern=%m%n :指定怎样格式化指定的消息。
    
####XMLLayout  选项
    LocationInfo=true:默认值是false,输出java文件和行号　　

    log4j.appender.A1.layout=org.apache.log4j.PatternLayout

####log4j.appender.A1.layout.ConversionPattern=%-4r %-5p %d{yyyy-MM-dd HH:mm:ssS} %c %m%n
    #TTCC layout
    %r [%t] %-5p %c %x - %m%n
    %-6r [%15.15t] %-5p %30.30c %x - %m%n


<div align="center">
<table cellspacing="0" cellpadding="4" width="640" border="1" style="font-size:12px; font-family:Arial;">
    <tbody>
        <tr align="center">
            <th align="center" width="10%">Abbreviation</th>
            <th align="center" width="90%">Full Name</th>
        </tr>
        <tr align="center">
            <td>c</td>
            <td>Used to output the category of the logging event. e.g. for the category name "a.b.c" the pattern %c{2} will output "b.c"</td>
        </tr>
        <tr align="center">
            <td>C</td>
            <td>Used to output the fully qualified class name of the caller issuing the logging request.e.g. for the class name "org.apache.xyz.SomeClass", the pattern %C{1} will output "SomeClass"</td>
        </tr>
        <tr align="center">
            <td>d</td>
            <td>Used to output the date of the logging event. For example, %d{HH:mm:ss,SSS} or %d{dd MMM yyyy HH:mm:ss,SSS}.</td>
        </tr>
        <tr align="center">
            <td>F</td>
            <td>Used to output the file name where the logging request was issued.</td>
        </tr>
        <tr align="center">
            <td>l</td>
            <td>Used to output location information of the caller which generated the logging event.</td>
        </tr>
        <tr align="center">
            <td>L</td>
            <td>Used to output the line number from where the logging request was issued. WARNING Generating caller location information is extremely slow and should be avoided unless execution speed is not an issue. </td>
        </tr>
        <tr align="center">
            <td>m</td>
            <td>Used to output the application supplied message associated with the logging event.</td>
        </tr>
        <tr align="center">
            <td>M</td>
            <td>Used to output the method name where the logging request was issued. WARNING slow</td>
        </tr>
        <tr align="center">
            <td>n</td>
            <td>Outputs the platform dependent line separator character or characters.</td>
        </tr>
        <tr align="center">
            <td>p</td>
            <td>Used to output the priority of the logging event.</td>
        </tr>
        <tr align="center">
            <td>r</td>
            <td>Used to output the number of milliseconds elapsed from the construction of the layout until the creation of the logging event.</td>
        </tr>
        <tr align="center">
            <td>t</td>
            <td>Used to output the name of the thread that generated the logging event.</td>
        </tr>
        <tr align="center">
            <td>x</td>
            <td>Used to output the NDC (nested diagnostic context) associated with the thread that generated the logging event. </td>
        </tr>
        <tr align="center">
            <td>X</td>
            <td>Used to output the MDC (mapped diagnostic context) associated with the thread that generated the logging event.</td>
        </tr>
        <tr align="center">
            <td>%</td>
            <td>The sequence %% outputs a single percent sign. </td>
        </tr>
    </tbody>
</table>
</div>

## Configuring log4j
Inserting log requests into the application code requires a fair amount of planning and effort. Observation shows that approximately 4 percent of code is dedicated to logging. Currently, configuration files can be written in XML or in Java properties `(key=value)` format.

###Create Logger Instance
    import org.apache.log4j.Logger;
    
    static Logger logger = Logger.getLogger(ServerWithLog4j.class.getName());

###Read configure file
    BasicConfigurator.configure()：自动快速地使用缺省Log4j环境。
    PropertyConfigurator.configure(String configFilename)：读取使用Java的特性文件编写的配置文件。
    DOMConfigurator.configure(String filename)：读取XML形式的配置文件。
    
    实际使用:
    import org.apache.log4j.BasicConfigurator;
    import org.apache.log4j.PropertyConfigurator;
    import org.apache.log4j.xml.DOMConfigurator;

    BasicConfigurator.configure();           //加载默认配置ConversionPattern=%-4r [%t] %-5p %c %x - %m%n
    //DOMConfigurator.configure("log4j.xml");//加载.xml文件
    //PropertyConfigurator.configure("log4j.properties");//加载.properties文件

###Insert logging info
    Log4j Levels: DEBUG, INFO, WARN, ERROR, FATAL
    
    Logger.debug(Object message);//调试信息
    Logger.info(Object message);//一般信息
    Logger.warn(Object message);//警告信息
    Logger.error(Object message);//错误信息
    Logger.fatal(Object message);//致命错误信息
    
    Logger.log(Priority priority, Object message);
    
    import static org.apache.log4j.Priority.*;//warning: [deprecation] WARN in Priority has been deprecated
    import static org.apache.log4j.Level.*;
    
    Logger.log(Priority.DEBUG, "Debug Infor in Alternate Form");//warning: Priority has been deprecated
    Logger.log(Level.DEBUG, "Debug Infor in Alternate Form");   //Deprecated. Use Level.DEBUG instead.

###Default Initialization Procedure
1. Setting the log4j.defaultInitOverride system property to any other value then "false" will cause log4j to skip the default initialization procedure.
2. Set the resource string variable to the value of the log4j.configuration system property.The preferred way to specify the default initialization file is through the log4j.configuration system property. In case the system property log4j.configuration is not defined, then set the string variable resource to its default value "log4j.properties".
3. Attempt to convert the resource variable to a URL.
4. If the resource variable cannot be converted to a URL, for example due to a MalformedURLException, then search for the resource from the classpath by calling org.apache.log4j.helpers.Loader.getResource\(resource, Logger.class\) which returns a URL. Note that the string "log4j.properties" constitutes a malformed URL.
5. If no URL could not be found, abort default initialization. Otherwise, configure log4j from the URL. 

## Example Configurations

###Common Output Format
    -X   :Information output left-align.
    %p   :Used to output the priority of the logging event.
    %d{} :Used to output the date of the logging event.
    %c   :Used to output the category of the logging event (package and class).
    %m   :Used to output the application supplied message associated with the logging event.
    %n   :Outputs the platform dependent line separator character or characters.
    %L   :Used to output the line number from where the logging request was issued.
    %F   :Used to output the file name where the logging request was issued.

The invocation of the BasicConfigurator.configure method creates a rather simple log4j setup. This method is hardwired to add to the root logger a ConsoleAppender. The output will be formatted using a PatternLayout set to the pattern `%-4r [%t] %-5p %c %x - %m%n`.

    %d{yyy-MMM-dd HH:mm:ss,SSS} output: 2002-Sep-18 22:10:28,921
    %d{yyy-MM-dd HH:mm:ss,SSS}  output: 2002-10-18 22:10:28,921
    
    log4j.appender.Console.layout=org.apache.log4j.PatternLayout
    #log4j.appender.Console.layout.ConversionPattern=%d [%t] %-5p [%c] - %m%n
    log4j.appender.Console.layout.ConversionPattern=%d %-5p [%t] (%-13F:%L) - %m%n

###Simple configuration file

####log4j.properties
    # Set root logger level to DEBUG and its only appender to A1.
    log4j.rootLogger=DEBUG, A1

    # A1 is set to be a ConsoleAppender.
    log4j.appender.A1=org.apache.log4j.ConsoleAppender

    # A1 uses PatternLayout.
    log4j.appender.A1.layout=org.apache.log4j.PatternLayout
    #log4j.appender.A1.layout.ConversionPattern=%-4r [%t] %-5p %c %x - %m%n
    # Print the date in ISO 8601 format
    log4j.appender.A1.layout.ConversionPattern=%d [%t] %-5p %c - %m%n

    # Print only messages of level WARN or above in the package com.foo.
    log4j.logger.com.foo=WARN

###Rolling appender
    log4j.appender.ROLLING_FILE=org.apache.log4j.RollingFileAppender   //指定以文件的方式输出日志
    log4j.appender.ROLLING_FILE.Threshold=ERROR 
    log4j.appender.ROLLING_FILE.File=rolling.log  //文件位置,也可以用变量${java.home}、rolling.log
    log4j.appender.ROLLING_FILE.Append=true 
    log4j.appender.ROLLING_FILE.MaxFileSize=10KB  //文件最大尺寸
    log4j.appender.ROLLING_FILE.MaxBackupIndex=1  //备份数
    log4j.appender.ROLLING_FILE.layout=org.apache.log4j.PatternLayout 
    log4j.appender.ROLLING_FILE.layout.ConversionPattern=[framework] %d - %c -%-4r [%t] %-5p %c %x - %m%n  　

###Multiple Appenders
    log4j.rootLogger=DEBUG,CONSOLE,A1,im
    log4j.addivity.org.apache=true
    # 应用于控制台
    log4j.appender.CONSOLE=org.apache.log4j.ConsoleAppender
    log4j.appender.Threshold=DEBUG
    log4j.appender.CONSOLE.Target=System.out
    log4j.appender.CONSOLE.layout=org.apache.log4j.PatternLayout
    log4j.appender.CONSOLE.layout.ConversionPattern=[framework] %d - %c -%-4r [%t] %-5p %c %x - %m%n
    #log4j.appender.CONSOLE.layout.ConversionPattern=[start]%d{DATE}[DATE]%n%p[PRIORITY]%n%x[NDC]%n%t[THREAD] n%c[CATEGORY]%n%m[MESSAGE]%n%n
    #应用于文件
    log4j.appender.FILE=org.apache.log4j.FileAppender
    log4j.appender.FILE.File=file.log
    log4j.appender.FILE.Append=false
    log4j.appender.FILE.layout=org.apache.log4j.PatternLayout
    log4j.appender.FILE.layout.ConversionPattern=[framework] %d - %c -%-4r [%t] %-5p %c %x - %m%n
    # Use this layout for LogFactor 5 analysis
    # 应用于文件回滚
    log4j.appender.ROLLING_FILE=org.apache.log4j.RollingFileAppender
    log4j.appender.ROLLING_FILE.Threshold=ERROR
    log4j.appender.ROLLING_FILE.File=rolling.log  //文件位置,也可以用变量${java.home}、rolling.log
    log4j.appender.ROLLING_FILE.Append=true       //true:添加  false:覆盖
    log4j.appender.ROLLING_FILE.MaxFileSize=10KB   //文件最大尺寸
    log4j.appender.ROLLING_FILE.MaxBackupIndex=1  //备份数
    log4j.appender.ROLLING_FILE.layout=org.apache.log4j.PatternLayout
    log4j.appender.ROLLING_FILE.layout.ConversionPattern=[framework] %d - %c -%-4r [%t] %-5p %c %x - %m%n

    #应用于socket
    log4j.appender.SOCKET=org.apache.log4j.RollingFileAppender
    log4j.appender.SOCKET.RemoteHost=localhost
    log4j.appender.SOCKET.Port=5001
    log4j.appender.SOCKET.LocationInfo=true
    # Set up for Log Facter 5
    log4j.appender.SOCKET.layout=org.apache.log4j.PatternLayout
    log4j.appender.SOCET.layout.ConversionPattern=[start]%d{DATE}[DATE]%n%p[PRIORITY]%n%x[NDC]%n%t[THREAD]%n%c[CATEGORY]%n%m[MESSAGE]%n%n

    # Log Factor 5 Appender
    log4j.appender.LF5_APPENDER=org.apache.log4j.lf5.LF5Appender
    log4j.appender.LF5_APPENDER.MaxNumberOfRecords=2000
    # 发送日志给邮件
    log4j.appender.MAIL=org.apache.log4j.net.SMTPAppender
    log4j.appender.MAIL.Threshold=FATAL
    log4j.appender.MAIL.BufferSize=10
    www.wuset.com">log4j.appender.MAIL.From=web@www.wuset.com
    log4j.appender.MAIL.SMTPHost=www.wusetu.com
    log4j.appender.MAIL.Subject=Log4J Message
    www.wusetu.com">log4j.appender.MAIL.To=web@www.wusetu.com
    log4j.appender.MAIL.layout=org.apache.log4j.PatternLayout
    log4j.appender.MAIL.layout.ConversionPattern=[framework] %d - %c -%-4r [%t] %-5p %c %x - %m%n
    # 用于数据库
    log4j.appender.DATABASE=org.apache.log4j.jdbc.JDBCAppender
    log4j.appender.DATABASE.URL=jdbc:mysql://localhost:3306/test
    log4j.appender.DATABASE.driver=com.mysql.jdbc.Driver
    log4j.appender.DATABASE.user=root
    log4j.appender.DATABASE.password=
    log4j.appender.DATABASE.sql=INSERT INTO LOG4J (Message) VALUES ('[framework] %d - %c -%-4r [%t] %-5p %c %x - %m%n')
    log4j.appender.DATABASE.layout=org.apache.log4j.PatternLayout
    log4j.appender.DATABASE.layout.ConversionPattern=[framework] %d - %c -%-4r [%t] %-5p %c %x - %m%n

    log4j.appender.A1=org.apache.log4j.DailyRollingFileAppender
    log4j.appender.A1.File=SampleMessages.log4j
    log4j.appender.A1.DatePattern=yyyyMMdd-HH'.log4j'
    log4j.appender.A1.layout=org.apache.log4j.xml.XMLLayout
    #自定义Appender
    log4j.appender.im = net.cybercorlin.util.logger.appender.IMAppender
    log4j.appender.im.host = mail.cybercorlin.net
    log4j.appender.im.username = username
    log4j.appender.im.password = password
    log4j.appender.im.recipient = corlin@cybercorlin.net
    log4j.appender.im.layout=org.apache.log4j.PatternLayout
    log4j.appender.im.layout.ConversionPattern =[framework] %d - %c -%-4r [%t] %-5p %c %x - %m%n

###Tomcat
    export TOMCAT_OPTS="-Dlog4j.configuration=foobar.txt"
    export TOMCAT_OPTS="-Dlog4j.debug -Dlog4j.configuration=foobar.xml"
    set TOMCAT_OPTS=-Dlog4j.configuration=foobar.lcf -Dlog4j.configuratorClass=com.foo.BarConfigurator
    set TOMCAT_OPTS=-Dlog4j.configuration=file:/c:/foobar.lcf

## Example

###Log4jApp.java
    package com.cbay;

    import org.apache.log4j.Logger;
    import org.apache.log4j.BasicConfigurator;
    import org.apache.log4j.PropertyConfigurator;
    import org.apache.log4j.xml.DOMConfigurator;

    //Deprecated. Use Level.WARN instead Priority.WARN
    import static org.apache.log4j.Level.*;

    public class Log4jApp {

        //private static Logger log=Logger.getLogger("com.cbay.Log4jApp");
        private static Logger log=Logger.getLogger(Log4jApp.class.getName());

        public static void main(String[] args) {
            //BasicConfigurator.configure();           //加载默认配置ConversionPattern=%-4r [%t] %-5p %c %x - %m%n
            //DOMConfigurator.configure("log4j.xml");//加载.xml文件
            PropertyConfigurator.configure("log4j.properties");//加载.properties文件
            
            //Log4j Levels: DEBUG, INFO, WARN, ERROR, FATAL
            log.trace("Trace Info");
            log.debug("Debug Info");
            log.log(DEBUG, "Debug Infor in Alternate Form");
            log.info("Info Info");
            log.log(INFO, "Info Infor in Alternate Form");
            log.warn("Warn Info");
            log.log(WARN, "Warn Infor in Alternate Form");
            log.error("Error Info");
            log.log(ERROR, "Error Infor in Alternate Form");
            log.fatal("Fatal Info");
            log.log(FATAL, "Fatal Infor in Alternate Form");
        }
    }

###log4j.xml
    <?xml version="1.0" encoding="UTF-8" ?>
    <!DOCTYPE log4j:configuration SYSTEM "log4j.dtd">
    <log4j:configuration xmlns:log4j='http://jakarta.apache.org/log4j/'>

        <!-- ========================== 自定义输出格式说明================================ -->
          <!-- %p 输出优先级，即DEBUG，INFO，WARN，ERROR，FATAL -->
          <!-- %r 输出自应用启动到输出该log信息耗费的毫秒数  -->
          <!-- %c 输出所属的类目，通常就是所在类的全名 -->
          <!-- %t 输出产生该日志事件的线程名 -->
          <!-- %n 输出一个回车换行符，Windows平台为“/r/n”，Unix平台为“/n” -->
          <!-- %d 输出日志时间点的日期或时间，默认格式为ISO8601，也可以在其后指定格式，比如:
               %d{yyy-MMM-dd HH:mm:ss,SSS} 输出: 2002-Sep-18 22:10:28,921
               %d{yyy-MM-dd HH:mm:ss,SSS}  输出: 2002-10-18 22:10:28,921
          -->
          <!-- %l 输出日志事件的发生位置，包括类目名、发生的线程，以及在代码中的行数。举例:Testlog4.main(TestLog4.java:10)  -->
          <!-- ========================================================================== -->

          <!-- ========================== 输出方式说明================================ -->
          <!-- Log4j提供的appender有以下几种:  -->
          <!-- org.apache.log4j.ConsoleAppender(控制台),  -->
          <!-- org.apache.log4j.FileAppender(文件),  -->
          <!-- org.apache.log4j.DailyRollingFileAppender(每天产生一个日志文件), -->
          <!-- org.apache.log4j.RollingFileAppender(文件大小到达指定尺寸的时候产生一个新的文件),  -->
          <!-- org.apache.log4j.WriterAppender(将日志信息以流格式发送到任意指定的地方)   -->
      <!-- ========================================================================== -->

        <!-- ConsoleAppender  -->
        <appender name="Console" class="org.apache.log4j.ConsoleAppender">
            <!--param name="Threshold" value="INFO"  为打印logger 去掉Threshold参数配置 /-->
            <layout class="org.apache.log4j.PatternLayout">
                <param name="ConversionPattern" value="%d{yyy-MM-dd HH:mm:ss} [%t] %-5p [%c] - %m%n" />
            </layout>
        </appender>

        <!-- DailyRollingFileAppender  -->
        <appender name="DailyRollingFile" class="org.apache.log4j.DailyRollingFileAppender">
            <param name="File" value="logs/Log4jApp.log" />
            <!--日志过滤门槛，记录warn以上级别日志  -->
            <param name="Threshold" value="WARN" />
            <param name="DatePattern" value="'.'yyyy-MM-dd'.log'" />
            <layout class="org.apache.log4j.PatternLayout">
                <param name="ConversionPattern" value="%d [%t] %-5p [%c] - %m%n" />
            </layout>
        </appender>

        <!-- RollingFileAppender  -->
        <appender name="RollingFile" class="org.apache.log4j.RollingFileAppender">
            <param name="File" value="logs/Log4jAppRF.log"/>
            <param name="Append" value="true"/>
            <param name="MaxFileSize" value="5KB"/>
            <param name="MaxBackupIndex" value="2"/>
            <layout class="org.apache.log4j.PatternLayout">
                <param name="ConversionPattern" value="%d [%t] %-5p [%c] - %m%n"/>
            </layout>
            <filter class="org.apache.log4j.varia.LevelRangeFilter">
                <param name="LevelMin" value="INFO"/>
                <param name="LevelMax" value="INFO"/>
            </filter>
        </appender>

       <!-- 打印具体类或包中的指定级别以上的日志
        <category name="com.cbay">
            <priority value="INFO" />
            <appender-ref ref="RollingDaily" />
            <appender-ref ref="RollingFile" />
        </category> -->

        <!-- 打印具体类或包中的指定级别以上的日志 -->
        <logger name="com.cbay">
            <level value="DEBUG" />
            <appender-ref ref="DailyRollingFile" />
            <appender-ref ref="RollingFile" />
        </logger>

        <!-- 设置默认过滤优先级，如果appender没有设置filter或Threshold 默认采用该级别，但定义的logger不会被过滤 -->
        <root>
            <priority value="DEBUG" />
            <appender-ref ref="Console" />
        </root>
    </log4j:configuration>

###log4j.properties
    # Output pattern : date [thread] priority category - message   FATAL 0  ERROR 3  WARN 4  INFO 6  DEBUG 7 

    #Console
    log4j.appender.Console=org.apache.log4j.ConsoleAppender
    log4j.appender.Console.layout=org.apache.log4j.PatternLayout
    #log4j.appender.Console.layout.ConversionPattern=%d [%t] %-5p [%c] - %m%n
    log4j.appender.Console.layout.ConversionPattern=%d %-5p [%t] (%-13F:%L) - %m%n

    #DailyRollingFileAppender
    log4j.appender.DailyRollingFile=org.apache.log4j.DailyRollingFileAppender
    log4j.appender.DailyRollingFile.File=logs/Log4jApp.log
    log4j.appender.DailyRollingFile.Threshold=WARN
    log4j.appender.DailyRollingFile.DatePattern='.'yyyy-MM-dd'.log'
    log4j.appender.DailyRollingFile.layout=org.apache.log4j.PatternLayout
    #log4j.appender.DailyRollingFile.layout.ConversionPattern=%d [%t] %-5p [%c] - %m%n
    log4j.appender.DailyRollingFile.layout.ConversionPattern=%d %-5p [%t] (%-13F:%L) - %m%n

    #RollingFileAppender
    log4j.appender.RollingFile=org.apache.log4j.RollingFileAppender
    log4j.appender.RollingFile.File=logs/Log4jAppRF.log
    log4j.appender.RollingFile.MaxFileSize=5KB
    log4j.appender.RollingFile.MaxBackupIndex=2
    log4j.appender.RollingFile.layout=org.apache.log4j.PatternLayout
    #log4j.appender.RollingFile.layout.ConversionPattern=%d [%t] %-5p [%c] - %m%n
    log4j.appender.RollingFile.layout.ConversionPattern=%d %-5p [%t] (%-13F:%L) - %m%n
    log4j.appender.RollingFile.filter.F1=org.apache.log4j.varia.LevelRangeFilter
    log4j.appender.RollingFile.filter.F1.LevelMin=INFO
    log4j.appender.RollingFile.filter.F1.LevelMax=INFO
    #log4j.appender.RollingFile.filter.F2=org.apache.log4j.varia.LevelMatchFilter
    #log4j.appender.RollingFile.filter.F2.levelToMatch=INFO
    #log4j.appender.RollingFile.filter.F2.acceptOnMatch=false

    #Project defalult level
    log4j.logger.com.cbay=DEBUG, DailyRollingFile, RollingFile

    #root 
    log4j.rootLogger=WARN, Console
    #By default the message priority should be no lower than info. That is, by default debug message should not be seen in the logs. 

## Conclusions
Log4j is a popular logging package written in Java. One of its distinctive features is the notion of inheritance in loggers. Using a logger hierarchy it is possible to control which log statements are output at arbitrary granularity. This helps reduce the volume of logged output and minimize the cost of logging.

One of the advantages of the log4j API is its manageability. Once the log statements have been inserted into the code, they can be controlled with configuration files. They can be selectively enabled or disabled, and sent to different and multiple output targets in user-chosen formats. The log4j package is designed so that log statements can remain in shipped code without incurring a heavy performance cost.

## REFERENCES
- [Short introduction to log4j](http://logging.apache.org/log4j/1.2/manual.html)
- [log4j 详解](http://www.blogjava.net/hwpok/archive/2008/08/23/223891.html)
- [log4j 配置](http://www.blogjava.net/fancydeepin/archive/2012/10/11/java_log4j.html)
- [常用log4j配置](http://fanqiang.chinaunix.net/app/other/2006-06-22/4640.shtml)
- [java log4j.xml配置与使用](http://blog.csdn.net/coolcoffee168/article/details/6368924)
- [Log4J基础详解及示例大全](http://blog.csdn.net/NearEast/article/details/7584385#comments)
- [Apache通用日志工具commons-logging和Log4j使用总结](http://lavasoft.blog.51cto.com/62575/26134/)
- [log4j xml 配置](http://houwen.iteye.com/blog/446721)
- [Log4j 分级输出](http://wendal.net/219.html)

