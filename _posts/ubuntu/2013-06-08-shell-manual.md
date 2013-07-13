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
