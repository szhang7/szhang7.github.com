---
layout: post
title: "Eclipse Handbook"
description: "Eclipse handbook"
category: java
tags: [eclipse, handbook, java]
---
{% include JB/setup %}

## Project Facets
Q: When import web project into eclipse, there is a problem of project type, import a java project.

A:
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

## REFERENCES

