---
layout: post
title: "Nexus Handbook"
description: "Nexus Handbook"
category: java
tags: [nexus, handbook, java]
---
{% include JB/setup %}

## Introduction
[Sonatype Nexus](http://www.sonatype.org/nexus) manages software "artifacts" required for development, deployment, and provisioning. If you develop software, Nexus can help you share those artifacts with other developers and end-users. Maven’s central repository has always served as a great convenience for users of Maven, but it has always been recommended to maintain your own repositories to ensure stability within your organization. Nexus greatly simplifies the maintenance of your own internal repositories and access to external repositories. With Nexus you can completely control access to, and deployment of, every artifact in your organization from a single location.

## Install Nexus

###Setup Environment Variables
    $ sudo gedit /etc/profile
    export NEXUS_HOME=/data/ubuntu/nexus/nexus-2.1.1
    export PATH=$NEXUS_HOME/bin:$PATH
    $ source /etc/profile

###Running Nexus
    $ nexus start
    
###Create system service
    $ cd etc/init.d
    $ sudo cp $NEXUS_HOME/../nexus
    $ sudo update-rc.d nexus defaults
    $ sudo service nexus start

## Configuring Nexus

###Login nexus
    http://192.168.2.10:7076/nexus
    username: admin
    password: admin123

###HTTP Proxy Settings
Administration-->Server-->Default HTTP Proxy Settings(optional)

    Proxy Host: proxy.xxx.com
    Proxy Port: 8080
    
    username: xxxxxx
    password: xxxxxx

###Configuring Repositories
Views/Repositories-->Repositories

####Some Concepts
- A repository is a collection of binary software artifacts and metadata stored in a defined directory structure which is used by clients such as Apache Ivy to retrieve binaries during a build process, which stores two types of artifacts: releases and snapshots. 
- Release repositories are for stable, static release artifacts.
- Snapshot repositories are frequently updated repositories that store binary software artifacts from projects under constant development.
- A proxy repository is a proxy of a remote repository.
- A hosted repository is a repository which is hosted by Nexus. For example: 3rd Party, Releases, and Snapshots.
- Groups allow you to combine multiple repositories and other repository groups in a single URL.

nexus has three type repositories: proxy, hosted, and group.

####Configuring Central Repository
    Download Remote Indexes: true   #nexus will download index from central repository.

####Configuring Hosted Repository
    Deployement Policy: Allow Redeploy

####Add New Proxy Repository
    Add-->Proxy Repository
    
#####Eclipse Repository
    Repository ID: eclipse
    Repository Name: Eclipse Repo
    Provider: Maven2
    Repository Policy: Release
    
    Remote Storage Location: http://maven.eclipse.org/nexus/content/groups/public/
    Download Remote Indexes: true
    Auto Blocking Enabled  : true
    File Content Validation: true
    
#####JBoss Repository
    Repository ID: jboss
    Repository Name: JBoss Repo
    Provider: Maven2
    Repository Policy: Release
    
    Remote Storage Location: http://repository.jboss.org/nexus/content/groups/public/
    Download Remote Indexes: true
    Auto Blocking Enabled  : true
    File Content Validation: true
    
#####Sonatype Repository
    Repository ID: sonatype
    Repository Name: Sonatype Repo
    Provider: Maven2
    Repository Policy: Release
    
    Remote Storage Location: http://repository.sonatype.org/content/groups/public/
    Download Remote Indexes: true
    Auto Blocking Enabled  : true
    File Content Validation: true
    
#####Springsource Repository
    Repository ID: springsource
    Repository Name: Springsource Repo
    Provider: Maven2
    Repository Policy: Release
    
    Remote Storage Location: http://repo.springsource.org/release/
    Download Remote Indexes: true
    Auto Blocking Enabled  : true
    File Content Validation: true
    
#####Sonatype Repository
    Repository ID: springsource-milestone
    Repository Name: Springsource Milestone
    Provider: Maven2
    Repository Policy: Release
    
    Remote Storage Location: http://repo.springsource.org/libs-milestone/
    Download Remote Indexes: true
    Auto Blocking Enabled  : true
    File Content Validation: true

####Configuring Group Repository
    Note that the order of the repositories listed in Order Group Repositories is important. When Nexus searches for an artifact in a group it will return the first match.
    We also recommend putting Central higher in this list than a smaller.

###Configuring Username Password
Security-->Users

    deployment-->click right button-->Set Password
    
    New Password: deployment123
    Confirm Password: deployment123

## Configuring Maven settings.xml
    <settings>
        <servers>
            <server>
                <id>deployment</id>
                <username>deployment</username>
                <password>deployment123</password>
            </server>
        </servers>
        <mirrors>
            <mirror>
                <!--This sends everything else to /public -->
                <id>nexus</id>
                <mirrorOf>*</mirrorOf>
                <url>http://192.168.2.10:7076/nexus/content/groups/public</url>
            </mirror>
        </mirrors>
        <profiles>
            <profile>
                <id>nexus</id>
                <!--Enable snapshots for the built in central repo to direct -->
                <!--all requests to nexus via the mirror -->
                <repositories>
                    <repository>
                        <id>central</id>
                        <url>http://central</url>
                        <releases><enabled>true</enabled></releases>
                        <snapshots><enabled>true</enabled></snapshots>
                    </repository>
                </repositories>
                <pluginRepositories>
                    <pluginRepository>
                        <id>central</id>
                        <url>http://central</url>
                        <releases><enabled>true</enabled></releases>
                        <snapshots><enabled>true</enabled></snapshots>
                    </pluginRepository>
                </pluginRepositories>
            </profile>
        </profiles>
        <activeProfiles>
            <!--make the profile active all the time -->
            <activeProfile>nexus</activeProfile>
        </activeProfiles>
    </settings>

## Configuring Project pom.xml
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

## REFERENCES
- [Repository Management with Nexus](http://books.sonatype.com/nexus-book/reference/index.html)
- [用nexus搭建maven私服](http://www.iteye.com/topic/1126678)
- [Nexus入门指南（图文）](http://juvenshun.iteye.com/blog/349534)
- [Configure Maven to Download from Nexus](https://support.sonatype.com/entries/20943003-Configure-Maven-to-Download-from-Nexus)
- [Configure Maven to Deploy to Nexus](https://support.sonatype.com/entries/21283268-Configure-Maven-to-Deploy-to-Nexus)

