---
layout: post
title: "Shell Menu"
description: "Create menu using shell script"
category: ubuntu
tags: [Shell, Menu, while, case]
---
{% include JB/setup %}

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
