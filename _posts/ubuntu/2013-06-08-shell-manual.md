---
layout: post
title: "Shell Manual"
description: "Shell manual document"
category: ubuntu
tags: [Shell, Manual, Menu, while, case]
---
{% include JB/setup %}

## Introduction
The Linux/Unix shell refers to a special program that allows you to interact with it by entering certain commands from the keyboard; the shell will execute the commands and display its output on the monitor.

(Read more: <http://linux.about.com/od/linux101/a/desktop11.htm>)

## Shell Function

###Define function
    [ function ] function_name [()] {
        CONSEQUENT-COMMANDS;
        [return int;]
    }

###Variable introduction
    #!/bin/bash
      
    function f1(){
        echo "number of parameters  :" $#
        echo "all parameters        :" $*
        echo "current PID           :" $$
        echo "result status         :" $?
        echo "parameter 1           :" $1
        echo "parameter 2           :" $2
    }

(Read more: <http://guoyunsky.iteye.com/blog/1671338>)

###Load function
shell test

    #!/bin/bash
    . hello     #load file hello
    
    hello       #call function hello()

shell hello

    #!/bin/bash
    function hello(){
        echo "Hello, world."
    }

###Format string
    function format_string(){
        local i len str
        str=$1
        len=${#str}
        #echo $len
        for((i=len;i<=50;i++))
        do
            str="$str-"
        done
        #echo $str
        project_name="$str"
    }

### return string value
    is_true(){
    if [ 5 -gt 3 ] ; then
        echo "yes"
    else
        echo "no"
    fi
    }
    ret=$(is_true)
    echo "ret is : $ret"

(Read more: <http://blog.chinaunix.net/uid-20686716-id-201383.html>)

### function pause
    function pause(){
        #if test -z "$1"     # zero length string
        #if test -n "$1"     # Non-zero length string
        if test $# -eq 0
        then
            echo -n "Press any key to return."       
        else
            echo "$1"
        fi
        read -n1 var
    }

###Are parameters integer? 
    #!/bin/bash
      
    function IntTest()
    {
        for arg  
        do  
            #算术运算符，当参数为整型数字时，执行失败  
            (( $arg )) 2>/dev/null      #屏蔽出错信息  
            if [ $? = 0 ]                 
            then  
                echo "$arg" is an integer   
            else  
                echo "$arg" is not an integer  
            fi  
        done  
    }
    IntTest -100 1234 22222222222222222 0765 0x10a +100 0xaadg assd 1.00 200.0 2a70 0.00

(Read more: <http://blog.csdn.net/yao_zhuang/article/details/5881935>)

## Shell Menu
Create menu using shell script.
    #! /bin/bash
    # Created by Johnny.Zhang
    # 2013/06/08

    while true
    do
    clear
    echo
    echo "-------------------------------------------------------------------------"
    tput cup 2 4
    time=`date +"%d%m%Y"`
    echo -ne "USER:$USER\tHOST:$HOSTNAME\tDATE:$time"
    echo
    tput cup 3
    echo  "-------------------------------------------------------------------------"
    tput cup 4 4
    echo -e "1. File"
    tput cup 5 4
    echo -e "2. Edit"
    tput cup 6 4
    echo -e "3. Exit"
    tput cup 7
    echo  "--------------------------------------------------------------------------"
    echo
    tput cup 9 4
    echo -n "Your choice [1,2,3]:"
    read CC
    case $CC in
    1)
    tput cup 11
    echo "1. File"
    echo -n "Press Enter to return to the main menu."
    ;;
    2)
    tput cup 11
    echo "2. Edit"
    echo -n "Press Enter to return to the main menu."
    ;;
    3)exit
    ;;
    *)
    tput cup 11 4
    echo -n "[WARNING] Invalid choice!"
    ;;
    esac
    read AA
    done

(Read more: <http://liuyu.blog.51cto.com/183345/307539>)

## Create an empty file
    #! /bin/bash
    # touch $file_name                      # when file not exist, create an empty file.
    echo -n>$file_name                      #create an empty file
    echo -e "Hello, world." >>$file_name    #write string into file

###References
- <http://www.cppblog.com/prayer/archive/2010/01/21/106113.html>
- <http://blog.csdn.net/embeddedman/article/details/7253866>

## Is file existed?
    #if ( test -f test11 ) then
    #if ( test -e test11 ) then
    if [ -f test1 ]; then
        echo "File exists"
    else
        echo "File not exists"
    fi

## Modify file content
    #! /bin/bash
    #sed -i '{'s/9080/8080/g'}' pom.xml     #'s/regexp/replacement/flags'
    #sed -e ":begin; /<port>/,/<\/port>/ { /<\/port>/! { $! { N; b begin }; }; s/<port>.*<\/port>/<port>8080<\/port>/; };" pom.xml
    #sed '{'s/3306/7077/g'; 's/root/cbay/g'; }' pom.xml
    #sed -e ":begin; /<connection.password/,/\/>/ { /\/>/! { $! { N; b begin }; }; s/<connection.password.*\/>/<connection.password>cbay<\/connection.password>/; };" pom.xml

    #sed '{'s/9080/8080/g'; 's/3306/7077/g'; 's/root/cbay/g'; }' pom.xml
    
    sed -ie "{s/9080/8080/g; s/3306/7077/g; s/root/cbay/g; }; :begin; /<connection.password/,/\/>/ { /\/>/! { $! { N; b begin }; }; s/<connection.password.*\/>/<connection.password>cbay<\/connection.password>/; };" pom.xml

    if test $? -eq 0
    then
        echo -e "Initialize the project----------OK"
    else
        echo -e "Initialize the project---------ERR"
    fi

###References
- <http://www.gnu.org/software/sed/manual/sed.html>
- <http://fyan.iteye.com/blog/1087242>
- <http://www.blogjava.net/alwayscy/archive/2009/09/01/293409.html>
- <http://blog.sina.com.cn/s/blog_6a1837e901011024.html>

## Read file line by line
    i=0
    cat $file_name | while read line
    do
        i=$(($i+1))     #line i
        echo $line
    done

###References
- <http://xuchengji.blog.51cto.com/160472/310885>

## Is variable null
    t=
    #if ( test -z "$t" ) then
    #if [ ! -n "$t" ]; then
    #if [ ! $t ]; then
    if [ "$t"="" ]; then
        echo "Is null";
    else
        echo "Not null";
    fi

###References
- <http://blog.csdn.net/runming918/article/details/7226507>
- <http://andrew913.iteye.com/blog/277801>

## Scan directory
    #filelist=`ls ${PWD}`
    #for fn in $(ls ${pwd})    #不能处理带空格的目录
    for fn in *               #current directory
    #for fn in ${PWD}/*
    #for fn in $filelist
    do
        if test -d "$fn"
        then
            echo "Directory: $fn"
        elif test -f "$fn"
        then
            echo "File: $fn"
        else
            echo "Error:$fn"
        fi
    done

###References
- <http://www.cnblogs.com/kaituorensheng/archive/2012/12/19/2825376.html>
- <http://www.wenzizone.cn/?p=313>
- <http://blog.163.com/clevertanglei900@126/blog/static/111352259201162553652150/>

