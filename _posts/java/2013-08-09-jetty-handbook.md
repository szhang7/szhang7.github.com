---
layout: post
title: "Jetty Handbook"
description: "Jetty Handbook"
category: java
tags: [jetty, handbook, maven, mvn]
---
{% include JB/setup %}

## Introduction
Jetty provides a Web server and javax.servlet container, plus support for SPDY, WebSocket, OSGi, JMX, JNDI, JAAS and many other integrations. These components are open source and available for commercial use and distribution.

## Jetty Maven Plugin
The Jetty Maven plugin is useful for rapid development and testing. You can add it to any webapp project that is structured according to the usual Maven defaults. The plugin can then periodically scan your project for changes and automatically redeploy the webapp if any are found. This makes the development cycle more productive by eliminating the build and deploy steps: you use your IDE to make changes to the project, and the running web container automatically picks them up, allowing you to test them straight away.

###Quick Start
Add jetty-maven-plugin to your pom.xml definition:

    <plugin>
        <groupId>org.eclipse.jetty</groupId>
        <artifactId>jetty-maven-plugin</artifactId>
        <version>${project.version}</version>
    </plugin>

Then, from the same directory as your root pom.xml, simply type:

    mvn jetty:run

This starts Jetty and serves up your project on http://localhost:8080/

###Stop the Plugin
You can terminate the plugin with `<ctrl-c>` in the terminal window where it is running.

## Supported Goals
The jetty-maven-plugin has a number of distinct Maven goals. Each goal is an action you can run to accomplish a specific task, or to work with a particular web application setup.

###jetty:run
Jetty deploys the webapp from its constituent sources. It looks for the constituent parts of a webapp in the maven default project locations, although you can override these in the plugin configuration. For example, by default it looks for

- resources in ${basedir}/src/main/webapp
- classes in ${project.build.outputDirectory}
- web.xml in ${basedir}/src/main/webapp/WEB-INF/

####Example
Example 1.

    <plugin>
        <groupId>org.mortbay.jetty</groupId>
        <artifactId>jetty-maven-plugin</artifactId>
        <configuration>
            <scanIntervalSeconds>10</scanIntervalSeconds>
            <webApp>
                <contextPath>/test</contextPath>
            </webApp>
        </configuration>
    </plugin>

Example 2.

    <project>
        ...
        <plugins>
            ...
            <plugin>
                <groupId>org.mortbay.jetty</groupId>
                <artifactId>jetty-maven-plugin</artifactId>
                <configuration>
                    <webAppSourceDirectory>${basedir}/src/staticfiles</webAppSourceDirectory>
                    <webAppConfig>
                        <contextPath>/</contextPath>
                        <descriptor>${basedir}/src/over/here/web.xml</descriptor>
                        <jettyEnvXml>${basedir}/src/over/here/jetty-env.xml</jettyEnvXml>
                    </webAppConfig>
                    <classesDirectory>${basedir}/somewhere/else</classesDirectory>
                    <scanTargets>
                        <scanTarget>src/mydir</scanTarget>
                        <scanTarget>src/myfile.txt</scanTarget>
                    </scanTargets>
                    <scanTargetPatterns>
                        <scanTargetPattern>
                            <directory>src/other-resources</directory>
                            <includes>
                                <include>**/*.xml</include>
                                <include>**/*.properties</include>
                            </includes>
                            <excludes>
                                <exclude>**/myspecial.xml</exclude>
                                <exclude>**/myspecial.properties</exclude>
                            </excludes>
                        </scanTargetPattern>
                    </scanTargetPatterns>
                </configuration>
            </plugin>
        </plugins>
    </project>

###jetty:run-war
This goal first packages your webapp as a WAR file and then deploys it to Jetty.

####Configuring the war
    <project>
        ...
        <plugins>
            ...
            <plugin>
                <groupId>org.mortbay.jetty</groupId>
                <artifactId>jetty-maven-plugin</artifactId>
                <configuration>
                    <war>${basedir}/target/mycustom.war</war>
                </configuration>
            </plugin>
        </plugins>
    </project>

###jetty:start
This goal is new in jetty-7.6.0. This goal is designed to be used with an execution binding in your pom.xml. It is just like the jetty:run goal, however the difference is that it does NOT first execute the build up until the "test-compile" phase to ensure that all necessary classes and files of the webapp have been generated. This is most useful when you want to control the start and stop of jetty via execution bindings in your pom.xml.

    <plugin>
        <groupId>org.mortbay.jetty</groupId>
        <artifactId>jetty-maven-plugin</artifactId>
        <configuration>
            <scanIntervalSeconds>10</scanIntervalSeconds>
            <stopKey>foo</stopKey>
            <stopPort>9999</stopPort>
        </configuration>
        <executions>
            <execution>
                <id>start-jetty</id>
                <phase>pre-integration-test</phase>
                <goals>
                    <goal>start</goal>
                </goals>
                <configuration>
                    <scanIntervalSeconds>0</scanIntervalSeconds>
                    <daemon>true</daemon>
                </configuration>
            </execution>
            <execution>
                <id>stop-jetty</id>
                <phase>post-integration-test</phase>
                <goals>
                    <goal>stop</goal>
                </goals>
            </execution>
        </executions>
    </plugin>

###jetty:stop
If you want to use mvn jetty:stop, you need to configure the plugin with a special port number and key that you also supply by executing the stop goal.

    <plugin>
        <groupId>org.mortbay.jetty</groupId>
        <artifactId>jetty-maven-plugin</artifactId>
        <configuration>
            <stopPort>9966</stopPort>
            <stopKey>foo</stopKey>
        </configuration>
    </plugin>

Then, while Jetty is running, type:

    mvn jetty:stop

###jetty:help
mvn jetty:help prints the list of goals for the jetty-maven-plugin, with a description of each goal.

## Q&A

## REFERENCES
- <http://www.eclipse.org/jetty/>
- <http://www.eclipse.org/jetty/documentation/current/jetty-maven-plugin.html>
- <http://wiki.eclipse.org/Jetty/Feature/Jetty_Maven_Plugin>

