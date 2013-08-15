---
layout: post
title: "Tomcat Handbook"
description: "Tomcat Handbook"
category: java
tags: [tomcat, handbook]
---
{% include JB/setup %}

## Introduction
Apache Tomcat is an open source software implementation of the Java Servlet and JavaServer Pages technologies. The Java Servlet and JavaServer Pages specifications are developed under the Java Community Process.

## Tomcat variables
    $CATALINA_HOME: the directory into which you have installed Tomcat.
    $CATALINA_BASE: refer the base directory against which most relative paths are resolved.

## Tomcat7x Plugin
The Tomcat Maven Plugin provides goals to manipulate WAR projects within the Apache Tomcat servlet container.

###Supported Goals
    Goal	                Description
    tomcat7:deploy	        Deploy a WAR to Tomcat.
    tomcat7:deploy-only	    Deploy a WAR to Tomcat without forking the package lifecycle
    tomcat7:exec-war	    This mojo will create a self executable jar file containing all tomcat classes.
                            So you will be able to use only: java -jar createjar.jar to run your webapp without need to install an Apache Tomcat instance.
                            More details here: http://tomcat.apache.org/maven-plugin-2.0-beta-1/executable-war-jar.html
    tomcat7:exec-war-only	No description.
    tomcat7:help	        Display help information on tomcat7-maven-plugin.
                            Call mvn tomcat7:help -Ddetail=true -Dgoal=<goal-name> to display parameter details.
    tomcat7:run	            Runs the current project as a dynamic web application using an embedded Tomcat server.
    tomcat7:run-war	        Runs the current project as a packaged web application using an embedded Tomcat server.
    tomcat7:run-war-only	Runs the current project as a packaged web application using an embedded Tomcat server without forking the package cycle.
    tomcat7:shutdown	    Shuts down all possibly started embedded tomcat servers. This will be automatically down through a shutdown hook or you may call this Mojo to shut them down explictly.
                            By default the shutdown goal is not bound to any phase. For integration tests you might want to bind it to post-integration-test.

###System Requirements
The following specifies the minimum requirements to run this Maven plugin:

    Maven	    2.0
    JDK	        1.5
    Memory	    No minimum requirement.
    Disk Space	No minimum requirement.

###Usage
You should specify the version in your project's plugin configuration:

    <project>
    ...
    <build>
        <!-- To define the plugin version in your parent POM -->
        <pluginManagement>
            <plugins>
                <plugin>
                    <groupId>org.apache.tomcat.maven</groupId>
                    <artifactId>tomcat7-maven-plugin</artifactId>
                    <version>2.0</version>
                </plugin>
                ...
            </plugins>
        </pluginManagement>
        <!-- To use the plugin goals in your POM or parent POM -->
        <plugins>
            <plugin>
                <groupId>org.apache.tomcat.maven</groupId>
                <artifactId>tomcat7-maven-plugin</artifactId>
                <version>2.0</version>
            </plugin>
            ...
        </plugins>
    </build>
    ...
    </project>

## tomcat-users.xml
$CATALINA_BASE/conf/tomcat-users.xml is assigned to the roles.

###Available roles

- manager-gui — Access to the HTML interface.
- manager-status — Access to the "Server Status" page only.
- manager-script — Access to the tools-friendly plain text interface that is described in this document, and to the "Server Status" page.
- manager-jmx — Access to JMX proxy interface and to the "Server Status" page.

The HTML interface is protected against CSRF (Cross-Site Request Forgery) attacks, but the text and JMX interfaces cannot be protected. To maintain the CSRF protection:

- Users with the manager-gui role should not be granted the manager-script or manager-jmx roles.
- If you use web browser to access the Manager application using a user that has either manager-script or manager-jmx roles (for example for testing the plain text or JMX interfaces), then all windows of the browser MUST be closed afterwards to terminate the session.

###Tomcat7 configuration
    <role rolename="manager-gui"/>
    <role rolename="manager-status"/>
    <role rolename="manager-script"/>
    <role rolename="manager-jmx"/>
    <user username="admin" password="admin" roles="manager-gui"/>

###Tomcat6 configuration
    <role rolename="manager-gui"/>
    <role rolename="manager-status"/>
    <role rolename="manager-script"/>
    <role rolename="manager-jmx"/>
    <user username="admin" password="admin" roles="manager-gui"/>

## Q&A

## REFERENCES
- <http://tomcat.apache.org/>
- <http://tomcat.apache.org/maven-plugin-2.0/tomcat7-maven-plugin/plugin-info.html>
- <http://tomcat.apache.org/tomcat-6.0-doc/manager-howto.html>
- <http://tomcat.apache.org/tomcat-7.0-doc/manager-howto.html>
- <http://www.verydemo.com/demo_c199_i2343.html>
