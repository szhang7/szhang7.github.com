---
layout: post
title: "Maven Handbook"
description: "Maven Handbook"
category: java
tags: [maven, mvn, handbook, java]
---
{% include JB/setup %}

## Introduction
Maven, a Yiddish word meaning accumulator of knowledge, was originally started as an attempt to simplify the build processes in the Jakarta Turbine project. There were several projects each with their own Ant build files that were all slightly different and JARs were checked into CVS. We wanted a standard way to build the projects, a clear definition of what the project consisted of, an easy way to publish project information and a way to share JARs across several projects.

The result is a tool that can now be used for building and managing any Java-based project. We hope that we have created something that will make the day-to-day work of Java developers easier and generally help with the comprehension of any Java-based project.

## Installation Instructions
Maven is a Java tool, so you must have Java installed in order to proceed. More precisely, you need a Java Development Kit (JDK), the Java Runtime Environment (JRE) is not sufficient. Additional optional installation steps are listed after the platform specific instructions. For more details, please refer to the [Download and Installation](http://maven.apache.org/download.cgi) instructions.

###Windows 2000/XP/Win7

1. Unzip the distribution archive, i.e. apache-maven-3.1.0-bin.zip to the directory you wish to install Maven 3.1.0. These instructions assume you chose C:\Program Files\Apache Software Foundation. The subdirectory apache-maven-3.1.0 will be created from the archive.

2. Add the M2_HOME environment variable by opening up the system properties (WinKey + Pause), selecting the "Advanced" tab, and the "Environment Variables" button, then adding the M2_HOME variable in the user variables with the value C:\Program Files\Apache Software Foundation\apache-maven-3.1.0. Be sure to omit any quotation marks around the path even if it contains spaces. Note: For Maven   2.0.9, also be sure that the M2_HOME doesn't have a '\' as last character.

3. In the same dialog, add the M2 environment variable in the user variables with the value %M2_HOME%\bin.

4. Optional: In the same dialog, add the MAVEN_OPTS environment variable in the user variables to specify JVM properties, e.g. the value -Xms256m -Xmx512m. This environment variable can be used to supply extra options to Maven.

5. In the same dialog, update/create the Path environment variable in the user variables and prepend the value %M2% to add Maven available in the command line.

6. In the same dialog, make sure that JAVA_HOME exists in your user variables or in the system variables and it is set to the location of your JDK, e.g. C:\Program Files\Java\jdk1.5.0_02 and that %JAVA_HOME%\bin is in your Path environment variable.

7. Open a new command prompt (Winkey + R then type cmd) and run mvn --version to verify that it is correctly installed.

###Unix-based Operating Systems(Linux, Solaris and Mac OS X)

1. Extract the distribution archive, i.e. apache-maven-3.1.0-bin.tar.gz to the directory you wish to install Maven 3.1.0. These instructions assume you chose /usr/local/apache-maven. The subdirectory apache-maven-3.1.0 will be created from the archive.

2. In a command terminal, add the M2_HOME environment variable, e.g. export M2_HOME=/usr/local/apache-maven/apache-maven-3.1.0.

3. Add the M2 environment variable, e.g. export M2=$M2_HOME/bin.

4. Optional: Add the MAVEN_OPTS environment variable to specify JVM properties, e.g. export MAVEN_OPTS="-Xms256m -Xmx512m". This environment variable can be used to supply extra options to Maven.

5. Add M2 environment variable to your path, e.g. export PATH=$M2:$PATH.

6. Make sure that JAVA_HOME is set to the location of your JDK, e.g. export JAVA_HOME=/usr/java/jdk1.5.0_02 and that $JAVA_HOME/bin is in your PATH environment variable.

7. Run mvn --version to verify that it is correctly installed.

## Configuring Maven
Maven configuration occurs at 3 levels:

- Project - most static configuration occurs in pom.xml
- Installation - this is configuration added once for a Maven installation
- User - this is configuration specific to a particular user

The separation is quite clear - the project defines information that applies to the project, no matter who is building it, while the others both define settings for the current environment.

**Note:** the installation and user configuration can not be used to add shared project information - for example, setting `<organization>` or `<distributionManagement>` company-wide.

For this, you should have your projects inherit from a company-wide parent pom.xml.

You can specify your configuration in `${user.home}/.m2/settings.xml` or `${M2_HOME}/conf/settings.xml`.

###Quick Overview
    <settings xmlns="http://maven.apache.org/SETTINGS/1.0.0"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
      xsi:schemaLocation="http://maven.apache.org/SETTINGS/1.0.0
                          http://maven.apache.org/xsd/settings-1.0.0.xsd">
      <localRepository/>
      <interactiveMode/>
      <usePluginRegistry/>
      <offline/>
      <pluginGroups/>
      <servers/>
      <mirrors/>
      <proxies/>
      <profiles/>
      <activeProfiles/>
    </settings>

###Configuring your Local Repository
    <settings>
      ...
      <localRepository>/path/to/local/repo/</localRepository>
      <interactiveMode>true</interactiveMode>
      <usePluginRegistry>false</usePluginRegistry>
      <offline>false</offline>
      ...
    </settings>

Note: The local repository must be an absolute path.

###Plugin Groups
    <settings>
      ...
      <pluginGroups>
        <pluginGroup>org.mortbay.jetty</pluginGroup>
        <pluginGroup>org.apache.tomcat.maven</pluginGroup>
      </pluginGroups>
      ...
    </settings>

For example, given the above settings the Maven command line may execute org.mortbay.jetty:jetty-maven-plugin:run with the truncated command:

    mvn jetty:run
    mvn tomcat:run

###Security and Deployment Settings
Repositories to deploy to are defined in a project in the `<distributionManagement>` section. However, you cannot put your username, password, or other security settings in that project. For that reason, you should add a server definition to your own settings with an id that matches that of the deployment repository in the project.

    <settings>
      ...
      <servers>
        <server>
          <id>repo1</id>
          <username>repouser</username>
          <!-- other optional elements:
            <password>my_login_password</password>
            <privateKey>/path/to/identity</privateKey> (default is ~/.ssh/id_dsa)
            <passphrase>my_key_passphrase</passphrase>
          -->
        </server>
      ...
      </servers>
      ...
    </settings>

To encrypt passwords in these sections, refer to [Encryption Settings](http://maven.apache.org/guides/mini/guide-encryption.html).

###Using Mirrors for Repositories
Some reasons to use a mirror are:

- There is a synchronized mirror on the internet that is geographically closer and faster
- You want to replace a particular repository with your own internal repository which you have greater control over
- You want to run a repository manager to provide a local cache to a mirror and need to use its URL instead

    <settings>
      ...
      <mirrors>
        <mirror>
          <id>UK</id>
          <name>UK Central</name>
          <url>http://uk.maven.org/maven2</url>
          <mirrorOf>central</mirrorOf>
        </mirror>
      </mirrors>
      ...
    </settings>

You can force Maven to use a single repository by having it mirror all repository requests. To achieve this, set mirrorOf to `*`.

Refer to [Guide to Mirror Settings](http://maven.apache.org/guides/mini/guide-configuring-maven.html) for more details.

###Configuring a proxy
    <settings>
      <proxies>
       <proxy>
          <active>true</active>
          <protocol>http</protocol>
          <host>proxy.somewhere.com</host>
          <port>8080</port>
          <username>proxyuser</username>
          <password>somepassword</password>
          <nonProxyHosts>www.google.com|*.somewhere.com</nonProxyHosts>
        </proxy>
      </proxies>
    </settings>

For more information, see the [Guide to using a Proxy](http://maven.apache.org/guides/mini/guide-proxies.html).

###Configuring Parallel Artifact Resolution
By default, Maven 2.1.0+ will download up to 5 artifacts (from different groups) at once. To change the size of the thread pool, start Maven using -Dmaven.artifact.threads.

    mvn -Dmaven.artifact.threads=1 clean install
    export MAVEN_OPTS=-Dmaven.artifact.threads=3

## Maven Build Lifecycle
Maven 2.0 is based around the central concept of a build lifecycle. What this means is that the process for building and distributing a particular artifact (project) is clearly defined.

There are three built-in build lifecycles: default, clean and site. The default lifecycle handles your project deployment, the clean lifecycle handles project cleaning, while the site lifecycle handles the creation of your project's site documentation.

- A Build Lifecycle is Made Up of Phases.
- A Build Phase is Made up of Plugin Goals.

###Setting Up Your Project to Use the Build Lifecycle

####Packaging
The first, and most common way, is to set the packaging for your project via the equally named POM element `<packaging>`. Some of the valid packaging values are `jar, war, ear and pom`. If no packaging value has been specified, it will default to jar.

####Plugins
The second way to add goals to phases is to configure plugins in your project. Plugins are artifacts that provide goals to Maven.

For example, the Modello plugin binds by default its goal modello:java to the generate-sources phase (Note: The modello:java goal generates Java source codes). 

    ...
     <plugin>
       <groupId>org.codehaus.modello</groupId>
       <artifactId>modello-maven-plugin</artifactId>
       <version>1.4</version>
       <executions>
         <execution>
           <configuration>
             <models>
               <model>src/main/mdo/maven.mdo</model>
             </models>
             <version>4.0.0</version>
           </configuration>
           <goals>
             <goal>java</goal>
           </goals>
         </execution>
       </executions>
     </plugin>
    ...

###Clean Lifecycle
    pre-clean               executes processes needed prior to the actual project cleaning
    clean                   remove all files generated by the previous build
    post-clean              executes processes needed to finalize the project cleaning

###Default Lifecycle
    validate 	            validate the project is correct and all necessary information is available.
    initialize 	            initialize build state, e.g. set properties or create directories.
    generate-sources 	    generate any source code for inclusion in compilation.
    process-sources 	    process the source code, for example to filter any values.
    generate-resources 	    generate resources for inclusion in the package.
    process-resources 	    copy and process the resources into the destination directory, ready for packaging.
    compile 	            compile the source code of the project.
    process-classes 	    post-process the generated files from compilation, for example to do bytecode enhancement on Java classes.
    generate-test-sources   generate any test source code for inclusion in compilation.
    process-test-sources 	process the test source code, for example to filter any values.
    generate-test-resources create resources for testing.
    process-test-resources 	copy and process the resources into the test destination directory.
    test-compile 	        compile the test source code into the test destination directory
    process-test-classes 	post-process the generated files from test compilation, for example to do bytecode enhancement on Java classes. For Maven 2.0.5 and above.
    test 	                run tests using a suitable unit testing framework. These tests should not require the code be packaged or deployed.
    prepare-package 	    perform any operations necessary to prepare a package before the actual packaging. This often results in an unpacked, processed version of the package. (Maven 2.1 and above)
    package 	            take the compiled code and package it in its distributable format, such as a JAR.
    pre-integration-test 	perform actions required before integration tests are executed. This may involve things such as setting up the required environment.
    integration-test 	    process and deploy the package if necessary into an environment where integration tests can be run.
    post-integration-test 	perform actions required after integration tests have been executed. This may including cleaning up the environment.
    verify 	                run any checks to verify the package is valid and meets quality criteria.
    install 	            install the package into the local repository, for use as a dependency in other projects locally.
    deploy 	                done in an integration or release environment, copies the final package to the remote repository for sharing with other developers and projects.

###Site Lifecycle
    pre-site 	            executes processes needed prior to the actual project site generation
    site 	                generates the project's site documentation
    post-site 	            executes processes needed to finalize the site generation, and to prepare for site deployment
    site-deploy 	        deploys the generated site documentation to the specified web server

## Introduction to the POM
A Project Object Model or POM is the fundamental unit of work in Maven. It is an XML file that contains information about the project and configuration details used by Maven to build the project.

###Super POM
The Super POM is Maven's default POM. All POMs extend the Super POM unless explicitly set, meaning the configuration specified in the Super POM is inherited by the POMs you created for your projects.

    ${M2_HOME}/lib/maven-model-builder-3.0.5.jar-->/org/apache/maven/model/pom-4.0.0.xml

###Minimal POM
The minimum requirement for a POM are the following:

- project root
- modelVersion - should be set to 4.0.0
- groupId - the id of the project's group.
- artifactId - the id of the artifact (project)
- verstion - the version of the artifact under the specified group

    <project>
      <modelVersion>4.0.0</modelVersion>
      <groupId>com.mycompany.app</groupId>
      <artifactId>my-app</artifactId>
      <version>1.0.0</version>
    </project>

###Distribution Management
    <distributionManagement>
        <repository>
            <id>deployment</id>
            <name>Internal Releases</name>
            <url>http://192.168.2.10:7076/nexus/content/repositories/releases/</url>
        </repository>
        <snapshotRepository>
            <id>deployment</id>
            <name>Internal Releases</name>
            <url>http://192.168.2.10:7076/nexus/content/repositories/snapshots/</url>
        </snapshotRepository>
    </distributionManagement>

###Project Inheritance (继承)
Elements in the POM that are merged are the following:

- dependencies
- developers and contributors
- plugin lists (including reports)
- plugin executions with matching ids
- plugin configuration
- resources

####Parent POM
    <project>
      <modelVersion>4.0.0</modelVersion>
      <groupId>com.mycompany.app</groupId>
      <artifactId>my-app</artifactId>
      <version>1</version>
    </project>

####Module POM 1
    <project>
      <parent>
        <groupId>com.mycompany.app</groupId>
        <artifactId>my-app</artifactId>
        <version>1</version>
      </parent>
      <modelVersion>4.0.0</modelVersion>
      <groupId>com.mycompany.app</groupId>
      <artifactId>my-module</artifactId>
      <version>1</version>
    </project>

####Module POM 2
    <project>
      <parent>
        <groupId>com.mycompany.app</groupId>
        <artifactId>my-app</artifactId>
        <version>1</version>
        <relativePath>../parent/pom.xml</relativePath>
      </parent>
      <modelVersion>4.0.0</modelVersion>
      <artifactId>my-module</artifactId>
    </project>

###Project Aggregation (聚集)
Project Aggregation is similar to Project Inheritance. But instead of specifying the parent POM from the module, it specifies the modules from the parent POM. To do Project Aggregation, you must do the following:

- Change the parent POMs packaging to the value "pom" .
- Specify in the parent POM the directories of its modules (children POMs)

####my-app
    <project>
      <modelVersion>4.0.0</modelVersion>
      <groupId>com.mycompany.app</groupId>
      <artifactId>my-app</artifactId>
      <version>1</version>
      <packaging>pom</packaging>

      <modules>
        <module>my-module</module>
      </modules>
    </project>

####my-module
    <project>
      <modelVersion>4.0.0</modelVersion>
      <groupId>com.mycompany.app</groupId>
      <artifactId>my-module</artifactId>
      <version>1</version>
    </project>

###Project Interpolation and Variables
One of the practices that Maven encourages is do not repeat yourself.

####Project Model Variables
Any field of the model that is a single value element can be referenced as a variable. For example, ${project.groupId}, ${project.version}, ${project.build.sourceDirectory} and so on.

####Special Variables
    project.basedir         The directory that the current project resides in.
    project.baseUri         The directory that the current project resides in, represented as an URI. Since Maven 2.1.0
    maven.build.timestamp   The timestamp that denotes the start of the build. Since Maven 2.1.0-M1

    <project>
      ...
      <properties>
        <maven.build.timestamp.format>yyyyMMdd-HHmmss</maven.build.timestamp.format>
      </properties>
      ...
    </project>

####Properties
    <project>
      ...
      <properties>
        <mavenVersion>2.1</mavenVersion>
      </properties>
      <dependencies>
        <dependency>
          <groupId>org.apache.maven</groupId>
          <artifactId>maven-artifact</artifactId>
          <version>${mavenVersion}</version>
        </dependency>
        <dependency>
          <groupId>org.apache.maven</groupId>
          <artifactId>maven-project</artifactId>
          <version>${mavenVersion}</version>
        </dependency>
      </dependencies>
      ...
    </project>

## Others

### Common Commands
    $ mvn -v        #Display verstion information
    $ mvn -h        #Display help information
    $ mvn -e        #Produce execution error message
    $ mvn -X        #Produce execution debug output
    $ mvn -ff       #Stop at first failure in reactorized builds
    $ mvn -fae      #Only fail the build afterwards; allow all non-impacted builds to continue
    $ mvn -fn       #Never fail the build, regardless of project results
    $ mvn -l        #Log file to where all build output will go.
    $ mvn --log-file <arg>
    $ mvn -o        #Work offline
    $ mvn -q        #Quiet output - only show errors
    $ mvn -pl       #Comma-delimited list of specified reactor projects to build instead of all projects.
    
    $ mvn help:describe -Dplugin=help
    $ mvn help:describe -Dplugin=help -Dfull
    $ mvn help:describe -Dplugin=compiler -Dmojo=compile -Dfull
    $ mvn help:describe -Dplugin=exec -Dfull
    $ mvn help:effective-pom
    
    $ mvn archetype:generate -DarchetypeArtifactId=maven-archetype-quickstart -Dpackage=com.cbay.simple -DgroupId=com.cbay -DartifactId=simple -Dversion=1.0-SNAPSHOT -DinteractiveMode=false
    
    # run jar
    $ java -cp target/simple-1.0-SNAPSHOT.jar com.cbay.simple.App
    Hello World!
    $ mvn exec:java -Dexec.mainClass=com.cbay.simple.App
    Hello World!
    $ mvn exec:java -Dexec.mainClass=com.cbay.simple.App -Dexec.args="Welcome"
    Welcome
    Hello World!
    
    $ mvn archetype:generate -DarchetypeArtifactId=maven-archetype-webapp -Dpackage=com.cbay.webapp -DgroupId=com.cbay -DartifactId=webapp -Dversion=1.0-SNAPSHOT -DinteractiveMode=false
    $ mvn clean
    $ mvn compile
    $ mvn package
    $ mvn install
    $ mvn clean install
    $ mvn install -Dmaven.test.skip=true
    $ mvn deploy
    $ mvn jetty:run
    $ mvn tomcat:run
    $ mvn site
    $ mvn validate
    $ mvn verify
    $ mvn generate-sources
    $ mvn eclipse:eclipse -Dwtpversion=1.0
    $ mvn eclipse:clean -Dwtpversion=1.0
    $ mvn eclipse:eclipse
    $ mvn eclipse:clean
    
    $ mvn dependency:resolve        #print resolved dependency list
    $ mvn dependency:tree           #print the whole dependency tree
    $ mvn hibernate3:hbm2ddl        #use Hibernate3 plugin to create database.

###Install 3rd Party Package

    $ mvn install:install-file -DgroupId=com.oracle -DartifactId=ojdbc14 -Dversion=10.2.0.3.0 -Dpackaging=jar -Dfile=/driver/ojdbc14.jar

Dependence quote

    <dependency>
        <groupId>com.oracle</groupId>
        <artifactId>ojdbc14</artifactId>
        <version>10.2.0.3.0</version>
    </dependency>

###Deploy into tomcat

####${CATALINA_HOME}/conf/tomcat-users.xml

    <role rolename="manager-gui"/>
    <user username="admin" password="admin" roles="manager-gui"/>

####pom
    <plugin>
        <groupId>org.codehaus.mojo</groupId>
        <artifactId>tomcat-maven-plugin</artifactId>
        <configuration>
            <server>tomcat</server>
            <!-- http port -->
            <port>8080</port>
            <!-- application path always starts with /-->
            <path>/webapp_name</path>
            <url>http://localhost:8080/manager</url>
            <uriEncoding>utf-8</uriEncoding> 
        </configuration>
    </plugin>

####${M2_HOME}/conf/settings.xml
    <servers>
        <server>
            <id>tomcat</id>
            <username>admin</username>
            <password>admin</password>
        </server>
    </servers>

####groupId and Mojo name change
Since version 2.0-beta-1 tomcat mojos has been renamed to tomcat6 and tomcat7 with the same goals.

You must configure your pom to use this new groupId:

    <pluginManagement>
      <plugins>
        <plugin>
          <groupId>org.apache.tomcat.maven</groupId>
          <artifactId>tomcat6-maven-plugin</artifactId>
          <version>2.0</version>
        </plugin>
        <plugin>
          <groupId>org.apache.tomcat.maven</groupId>
          <artifactId>tomcat7-maven-plugin</artifactId>
          <version>2.0</version>
        </plugin>
      </plugins>
    </pluginManagement>

Or add the groupId in your ${M2_HOME}/conf/settings.xml

    <pluginGroups>
        ....
        <pluginGroup>org.apache.tomcat.maven</pluginGroup>
        ....
    </pluginGroups>

####Tomcat Commands
    $ mvn tomcat:deploy
    $ mvn tomcat:undeploy
    $ mvn tomcat:start
    $ mvn tomcat:stop
    $ mvn tomcat:redeploy
    $ mvn tomcat:exploded

###Maven jar plugin

####Generate runnable jar 1
    <build>
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-jar-plugin</artifactId>
                <configuration>
                <archive>
                    <manifest>
                        <addClasspath>true</addClasspath>
                        <classpathPrefix>lib/</classpathPrefix>
                        <mainClass>com.cbay.hardware.GetInfo</mainClass>
                    </manifest>
                </archive>
                </configuration>
            </plugin>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-dependency-plugin</artifactId>
                <executions>
                    <execution>
                        <id>copy</id>
                        <phase>package</phase>
                        <goals>
                            <goal>copy-dependencies</goal>
                        </goals>
                        <configuration>
                            <outputDirectory>${project.build.directory}/lib</outputDirectory>
                        </configuration>
                    </execution>
                </executions>
            </plugin>
        </plugins>
    </build>

####Generate runnable jar 2
    <build>
        <!-- <finalName>...</finalName>  -->
        <sourceDirectory>src/main/java</sourceDirectory>  
        <resources>  
            <!-- 控制资源文件的拷贝 -->  
            <resource>  
                <directory>src/main/resources</directory>  
                <targetPath>${project.build.directory}</targetPath>  
            </resource>  
        </resources>  
        <plugins>  
            <!-- 设置源文件编码方式 -->  
            <plugin>  
                <groupId>org.apache.maven.plugins</groupId>  
                <artifactId>maven-compiler-plugin</artifactId>  
                <configuration>  
                    <defaultLibBundleDir>lib</defaultLibBundleDir>  
                    <source>1.6</source>  
                    <target>1.6</target>  
                    <encoding>UTF-8</encoding>  
                </configuration>  
            </plugin>  
            <!-- 打包jar文件时，配置manifest文件，加入lib包的jar依赖 -->  
            <plugin>  
                <groupId>org.apache.maven.plugins</groupId>  
                <artifactId>maven-jar-plugin</artifactId>  
                <configuration>  
                    <archive>  
                        <manifest>  
                            <addClasspath>true</addClasspath>  
                            <classpathPrefix>lib/</classpathPrefix>  
                            <mainClass>com.cbay.hardware.GetInfo</mainClass>  
                        </manifest>  
                    </archive>  
                </configuration>  
            </plugin>  
            <!-- 拷贝依赖的jar包到lib目录 -->  
            <plugin>  
                <groupId>org.apache.maven.plugins</groupId>  
                <artifactId>maven-dependency-plugin</artifactId>  
                <executions>  
                    <execution>  
                        <id>copy</id>  
                        <phase>package</phase>  
                        <goals>  
                            <goal>copy-dependencies</goal>  
                        </goals>
                        <configuration>  
                            <outputDirectory>  
                                ${project.build.directory}/lib  
                            </outputDirectory>  
                        </configuration>  
                    </execution>  
                </executions>  
            </plugin>  
            <!-- 解决资源文件的编码问题 -->  
            <plugin>  
                <groupId>org.apache.maven.plugins</groupId>  
                <artifactId>maven-resources-plugin</artifactId>  
                <version>2.3</version>  
                <configuration>  
                    <encoding>UTF-8</encoding>  
                </configuration>  
            </plugin>  
            <!-- 打包source文件为jar文件 -->  
            <plugin>  
                <artifactId>maven-source-plugin</artifactId>  
                <version>2.1</version>  
                <configuration>  
                    <attach>true</attach>  
                    <encoding>UTF-8</encoding>  
                </configuration>  
                <executions>  
                    <execution>  
                        <phase>compile</phase>  
                        <goals>  
                            <goal>jar</goal>  
                        </goals>  
                    </execution>  
                </executions>  
            </plugin>  
        </plugins>
    </build>

###Maven Plugins

####log4j
    <properties>
		<log4j.version>1.2.17</log4j.version>
    </properties>

    <dependencies>
		<dependency>
			<groupId>log4j</groupId>
			<artifactId>log4j</artifactId>
			<version>${log4j.version}</version>
		</dependency>
    </dependencies>


## Maven by Example

###Archetypes

####org.apache.maven.archetypes
    maven-archetype-archetype (An archetype which contains a sample archetype.)
    maven-archetype-j2ee-simple (An archetype which contains a simplifed sample J2EE application.)
    maven-archetype-marmalade-mojo (-)
    maven-archetype-mojo (An archetype which contains a sample a sample Maven plugin.)
    maven-archetype-plugin (An archetype which contains a sample Maven plugin.)
    maven-archetype-plugin-site (An archetype which contains a sample Maven plugin site.)
    maven-archetype-portlet (An archetype which contains a sample JSR-268 Portlet.)
    maven-archetype-profiles (-)
    maven-archetype-quickstart (An archetype which contains a sample Maven project.)
    maven-archetype-site (An archetype which contains a sample Maven site.)
    maven-archetype-site-simple (An archetype which contains a sample Maven site.)
    maven-archetype-webapp (An archetype which contains a sample Maven Webapp project.)

####org.devnull
    devnull-web-archetype (DevNull starter webaapp with Spring MVC, JPA, Groovy and Twitter Bootstrap)

####org.jboss.spring.archetypes
    jboss-spring-mvc-archetype (An archetype that generates a starter Spring MVC application with Java EE persistence settings (server bootstrapped JPA, JTA transaction management) for JBoss AS7)
    spring-mvc-webapp (An archetype that generates a starter Spring MVC application with Java EE persistence settings (server bootstrapped JPA, JTA transaction management) for JBoss AS7)

####me.noroutine
    tobacco-bootstrap (Web Application with all modern client libraries)

###A Simple Maven Project
    $ mvn archetype:generate -DarchetypeGroupId=org.apache.maven.archetypes -DarchetypeArtifactId=maven-archetype-quickstart -Dpackage=com.cbay.simple -DgroupId=com.cbay -DartifactId=simple -Dversion=1.0-SNAPSHOT -DinteractiveMode=false
    $ cd simple
    $ mvn install
    
    $ java -cp target/simple-1.0-SNAPSHOT.jar com.cbay.simple.App
    Hello World!
    
    $ mvn exec:java -Dexec.mainClass=com.cbay.simple.App
    Hello World!
    
    $ mvn exec:java -Dexec.mainClass=com.cbay.simple.App -Dexec.args="Welcome"
    $ mvn help:describe -Dplugin=exec -Dfull

###A Simple Web Application

####Generating project

    $ mvn archetype:generate -DarchetypeGroupId=org.apache.maven.archetypes -DarchetypeArtifactId=maven-archetype-webapp -Dpackage=com.cbay.webapp -DgroupId=com.cbay -DartifactId=webapp -Dversion=1.0-SNAPSHOT -DinteractiveMode=false

####Configuring Compiler
    <plugins>
        ...
        <plugin>
            <artifactId>maven-compiler-plugin</artifactId>
            <configuration>
                <source>1.6</source>
                <target>1.6</target>
            </configuration>
        </plugin>
        ...
    </plugins>

####Configuring Jetty Plugin
	<!-- Project Properties -->
	<properties>
	    <jetty.version>8.1.12.v20130726</jetty.version>
	</properties>
	
    <plugins>
        <!-- Jetty Plugin -->
        <plugin>
            <groupId>org.eclipse.jetty</groupId>
            <artifactId>jetty-maven-plugin</artifactId>
            <version>${jetty.version}</version>
            <configuration>
                <stopPort>9966</stopPort>
                <stopKey>foo</stopKey>
                <webAppConfig>
                    <contextPath>/${project.artifactId}</contextPath>
                </webAppConfig>
            </configuration>
        </plugin>
    </plugins>

####Running
    $ mvn jetty:run
    http://localhost:8080/webapp

###A Multi-module Project

###Building Java Projects with Maven

####Create the directory structure
    $ mkdir hello-maven
    $ cd hello-maven
    $ mkdir -p src/main/java/hello

####Create Java classes
    src/main/java/hell/HelloWorld.java
    
    package hello;
    import org.joda.time.LocalTime;
    public class HelloWorld {
      public static void main(String[] args) {
        LocalTime currentTime = new LocalTime();
        System.out.println("The current local time is: " + currentTime);
        
        Greeter greeter = new Greeter();
        System.out.println(greeter.sayHello());
      }
    }
    
    src/main/java/hello/Greeter.java
    
    package hello;
    public class Greeter {
      public String sayHello() {
        return "Hello World!";
      }
    }

####Define a simple Maven build
    pom.xml
    
    <?xml version="1.0" encoding="UTF-8"?>
    <project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
      xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
      <modelVersion>4.0.0</modelVersion>
      <groupId>com.cbay</groupId>
      <artifactId>hello-maven</artifactId>
      <version>0.0.1-SNAPSHOT</version>
      <packaging>jar</packaging>

      <dependencies>
          <dependency>
              <groupId>joda-time</groupId>
              <artifactId>joda-time</artifactId>
              <version>2.2</version>
          </dependency>
      </dependencies>

      <build>
        <plugins>
          <plugin>
              <artifactId>maven-compiler-plugin</artifactId>
              <version>2.3.2</version>
          </plugin>
          <plugin>
            <groupId>org.codehaus.mojo</groupId>
            <artifactId>exec-maven-plugin</artifactId>
            <version>1.2.1</version>
            <executions>
              <execution>
              <phase>test</phase>
              <goals>
                <goal>java</goal>
              </goals>
              <configuration>
                <mainClass>hello.HelloWorld</mainClass>
                <arguments>
                  <argument>arg0</argument>
                  <argument>arg1</argument>
                </arguments>
              </configuration>
              </execution>
            </executions>
           </plugin>
        </plugins>
      </build>
    </project>

####Build Java code
    $ mvn compile
    $ mvn test

## REFERENCES
- [What is Maven?](http://maven.apache.org/what-is-maven.html)
- [Download Apache Maven](http://maven.apache.org/download.cgi)
- [Configuring Maven](http://maven.apache.org/guides/mini/guide-configuring-maven.html)
- [Settings Reference](http://maven.apache.org/settings.html)
- [Introduction to the Build Lifecycle](http://maven.apache.org/guides/introduction/introduction-to-the-lifecycle.html)
- [Introduction to the POM](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html)
- [Maven in 5 Minutes](http://maven.apache.org/guides/getting-started/maven-in-five-minutes.html)
- [Maven Getting Started Guide](http://maven.apache.org/guides/getting-started/index.html)
- [Sonatype Books](http://www.sonatype.com/resources/books)
- [Maven by Example](http://books.sonatype.com/mvnex-book/reference/index.html)
- [Maven常用命令](http://www.cnblogs.com/PatrickLee/archive/2012/10/31/2747398.html)
- [maven打包可运行的JAR](http://blog.163.com/coffee_hc/blog/static/4485331920121274422988/)
- [maven工程打包成runnable的jar包，拷贝资源和依赖jar包](http://ajita.iteye.com/blog/1635470)
- [Building Java Projects with Maven](http://spring.io/guides/gs/maven/)

