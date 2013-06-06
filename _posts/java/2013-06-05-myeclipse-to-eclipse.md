---
layout: post
title: "MyEclipse to Eclipse"
description: ""
category: java
tags: [MyEclipse, Eclipse, Project]
---
{% include JB/setup %}

## MyEclipse to Eclipse

解决方法如下：

###1、删除工程中.myeclipse文件件

###2、删除工程中.mymetadata文件

###3、打开.project文件
    (1)、在<buildSpec>中增加：
    <buildCommand>
        <name>org.eclipse.wst.common.project.facet.core.builder</name>
        <arguments>
        </arguments>
    </buildCommand>
    <buildCommand>
        <name>org.eclipse.wst.jsdt.core.javascriptValidator</name>
        <arguments>
        </arguments>
    </buildCommand>
    (2)、在<natures>中增加：
    <nature>org.eclipse.jem.workbench.JavaEMFNature</nature>
    <nature>org.eclipse.wst.jsdt.core.jsNature</nature>
    <nature>org.eclipse.wst.common.project.facet.core.nature</nature>
    <nature>org.eclipse.wst.common.modulecore.ModuleCoreNature</nature>"

###4、.settings文件件加下面建立文件：org.eclipse.wst.common.component
    在org.eclipse.wst.common.component文件中增加下面内容：
    <?xmlversion="1.0" encoding="UTF-8"?>
    <project-modules id="moduleCoreId" project-version="1.5.0">
        <wb-module deploy-name="jeecg-framework">
            <wb-resource deploy-path="/" source-path="/WebRoot"/>
            <wb-resource deploy-path="/WEB-INF/classes" source-path="/src"/>
            <wb-resource deploy-path="/WEB-INF/classes" source-path="/resources"/>
            <property name="context-root" value="jeecg-framework"/>
            <property name="java-output-path" value="/jeecg-framework/WebRoot/WEB-INF/classes"/>
        </wb-module>
    </project-modules>"

###5、设置jdk：
![1.jpg]({{ site.img_url }}/2013-06-05-01.jpg)

###6、设置工程编码：
![2.jpg]({{ site.img_url }}/2013-06-05-02.jpg)

###7、修改工程类型：
![3.jpg]({{ site.img_url }}/2013-06-05-03.jpg)

此时，.settings文件夹下面会增加几个文件，具体内容有兴趣的可以去研究。
至此，在server中可以成功部署！

![4.jpg]({{ site.img_url }}/2013-06-05-04.jpg)

