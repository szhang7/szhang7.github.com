---
layout: post
title: "Eclipse Handbook"
description: "Eclipse handbook"
category: java
tags: [eclipse, handbook, java]
---
{% include JB/setup %}

## Shortcuts
    Shift+Alt+S : Generate Getters and Setters
    Shift+Ctrl+F: Format Source code
    Shift+Ctrl+O: Organize imports
    Shift+Ctrl+X: Uppercase the currently selected text
    Shift+Ctrl+Y: Lowercase the currently selected text

## Generating webapp with Eclipse and Maven

###1.New Dynamic Web Project

###2.Deleting src directory

###3.Adding source folders
    src/main/java
    src/main/resources
    src/test/java
    src/test/resources

###4.Setting default output folder
    target/classes

###5.Modifying content directory
    src/main/webapp

###6.Converting to Maven project
    Select the project-->click right button-->Configure-->Convert to Maven Project
    
    packaging: war

###7.Changing test output folder
    target/test-classes

## Questions and answers

###Q1.Project Facets

####Description of the problem
When import web project into eclipse, there is a problem of project type, import a java project.

####Solutions
    1、进入项目目录，可看到.project文件，打开。
    2、找到<natures>...</natures>代码段。
    3、在第2步的代码段中加入如下标签内容并保存：
    <nature>org.eclipse.wst.common.project.facet.core.nature</nature>
    <nature>org.eclipse.wst.common.modulecore.ModuleCoreNature</nature>
    <nature>org.eclipse.jem.workbench.JavaEMFNature</nature>
    4、在eclipse的项目上点右键，刷新项目。
    5、在项目上点右键，进入属性（properties）
    6、在左侧列表项目中点击选择“Project Facets”，在右侧选择“Dynamic Web Module”和"Java"，点击OK保存即可。

(Read more: <http://www.cnblogs.com/jerome-rong/archive/2012/12/18/2822783.html>)

###Q2.Maven Dependencies

####Description of the problem
    You already generated a web project, but you want to reference Maven libraries.

####Solutions
    Properties-->Deployment Assembly-->Add-->Java Build Path Entries-->Next-->Maven Dependencies-->Finish

## REFERENCES
- [Eclipse+Maven快速生成Web项目](http://snowolf.iteye.com/blog/1627343)

