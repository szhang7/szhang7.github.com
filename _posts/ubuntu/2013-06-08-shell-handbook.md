---
layout: post
title: "Shell Handbook"
description: "Shell Handbook"
category: ubuntu
tags: [shell, handbook, menu, while, case]
---
{% include JB/setup %}

## Introduction

###What is the shell?
The Linux/Unix shell refers to a special program that allows you to interact with it by entering certain commands from the keyboard; the shell will execute the commands and display its output result on the monitor. Nowadays, we have graphical user interfaces (GUIs) in addition to command line interfaces (CLIs) such as the shell.

On most Linux systems a program called bash (which stands for Bourne Again SHell, an enhanced version of the original Bourne shell program, sh, written by Steve Bourne) acts as the shell program. There are several additional shell programs available on a typical Linux system. These include: ksh, tcsh and zsh.

###What's an xterm, gnome-terminal, konsole, etc.?
These are called "terminal emulators." They are programs that put a window up and let you interact with the shell. There are a bunch of different terminal emulators you can use. Most Linux distributions supply several, such as: xterm, rxvt, konsole, kvt, gnome-terminal, nxterm, and eterm.

###References
- <http://linux.about.com/od/linux101/a/desktop11.htm>
- <http://www.linuxcommand.org/lts0010.php>

## Common Shell Scripts
Collect some common shell scripts.

###Variables
    echo "number of parameters  :" $#
    echo "all parameters        :" $*
    echo "current PID           :" $$
    echo "result status         :" $?
    echo "parameter 1           :" $1
    echo "parameter 2           :" $2

###Datetime
    TODAY=`date -d today '+%Y-%m-%d %H:%M:%S'`
    echo "$TODAY"
    
    # calculate the time difference
    start=`date +%s -d "2011-11-28 15:55:37"`
    end=`date +%s -d "2011-11-28 15:55:52"`
    echo $(($end-$start))

###Passing parameters
    #!/bin/bash
    LANG=en_US.UTF-8
    #get parameters
    sourceFile="/data/ubuntu/test.md"
    if [ $# == 1 ] # $# Number of parameters
    then sourceFile=$1
    else echo "$1 required!"
    fi
    echo $sourceFile
    # if else
    # If there are two commands on the same line, you need to use semicolon ';' to separate.

###Directory and file
    #create an empty file
    touch $FILE_NAME                        #when file not exist, create an empty file.
    echo -n>$FILE_NAME                      #create an empty file
    echo -e "Hello, world.">>$FILE_NAME     #write string into file
    
    # create directories
    mkdir -p guicmd/{bin,lib,src,share/version,doc/{html,pdf,info,man}}
    
    # merge files
    cat $FILE1 $FILE2 |grep -a "关键字" > $MERGE_FILE
    
    # Copy standard input to files.
    echo "hello jack!" |tee -a log1.txt log2.txt
    
    # remove all files
    for i in `ls`; do rm $i; done
    ls|xargs -n20 rm -rf
    find -type f|xargs -n20 rm -rf
    
    # remove all .svn
    find -name '.svn'|xargs rm -rf
    
    # remove all directories in current directory
    ls * -d|xargs -n20 rm -rf
    find -type d|xargs -n20 rm -rf
    
    # get the number of files in the current directory
    find . -type f|wc -l
    
    # get the number of directories in the current directory
    find . -type d|wc -l
    
    # search and replace string in many files.
    sed -i "s/regexp/replacement/g" `grep regexp -rl $FILE_NAME or $DIR_NAME`
    # -i: inplace edit
    # -r: search sub directories
    # -l: output matched file names
    
    #find files by name
    find /data/ubuntu/bin -name "test"
    
    #find files by time
    find /data/ubuntu/bin -mtime -1     # modified files in 1 hour
    find /data/ubuntu/bin -mtime +1     # modified files before 1 hour
    
    #find files by type
    find /data/ubuntu/bin -type d       # directories and sub directories
    find /data/utunbu/bin -type f       # files
    
    #find files by size
    find /data/ubuntu/bin -size +1000k
    
    #split big file
    split -l 10000 log4j.log tt.txt

###grep
    # output the lines including keyword into result.log
    cat "$FILE_NAME"|grep -a "keyword">>result.log
    
    # more keywords
    cat "$FILE_NAME"|grep -a "aop=keyword1\|keyword2"
    
    # is port occupied
    netstat -tln | grep 8080
    RESULT=$?
    
    # does the file contain keyword
    COUNT=$(grep -ic 'jetty-maven-plugin' "$FILE_NAME")
    if( test $COUNT = 0 ) then
        echo "Not find"
    else
        echo "find $COUNT"
    fi
    
    # statistics lines by keyword
    COUNT=$(cat $FILE |grep -a "keyword" |wc -l)
    
    # query control command history
    history |grep "rm"

###Regular expressions
    regex="2010-11-08*"             # in shell
    String regex="2010-11-08.+"     # in java
    regex="2010-11-08.*"            # in java
    # .* or .+ represent any number of strings in java

###awk
    # split file
    awk -F'"' '{print $1}' "$FILE_NAME"
    # print: output on newline
    # printf: no wrap
    
    #Exclude duplicate content
    awk -F',' '!a[$1]++' "$FILE_NAME"
    # ',' delimiter

## if statement

###is the last statement executed successfully?
    echo test>test.md
    if test $? -eq 0
    then
        echo -e "successfully"
    else
        echo -e "failed"
    fi

###Is directory or file exists?
    DIR_NAME="/data/"
    if [ ! -d "$DIR_NAME" ]; then echo "Not exits"
    
    FILE_NAME="/data/test.md"
    #if ( test -f "$FILE_NAME"11 ) then
    #if ( test -e "$FILE_NAME" ) then
    if [ -f "$FILE_NAME" ]; then
        echo "File exists"
    else
        echo "File not exists"
    fi
    
###Is variable null
    t=
    #if ( test -z "$t" ) then
    #if [ ! -n "$t" ]; then
    #if [ ! $t ]; then
    if [ "$t"="" ]; then
        echo "Is null";
    else
        echo "Not null";
    fi

## for statement

###Scan directory
    #filelist=`ls ${PWD}`
    #for fn in $(ls ${pwd})   #不能处理带空格的目录
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

## while statement

###loop read lines
    while read line
    do
        echo $line
    done < $FILE_NAME
    
    cat $FILE_NAME|while read line
    do
        echo $line
    done
    
## Mathematical calculations summary
The default processing in shell is base on string.

###Wrong way to use
    var=1+1
    echo $var   #output result: 1+1
    
    var=1
    var=$var+1
    echo $var   #output result: 1+1

###Right way to use
    var=1
    let "var+=1"
    echo $var   #output result: 2
    # let suports all operators, but supports only integer arithmetic.
    
    var=1
    ((var+=1))
    echo $var   #output result: 2
    # (()) equal let.
    
    var=1
    var=$[$var+1]
    echo $var   #output result: 2
    # $[] supports all operators, but suports only integer arithmetic.
    
    var=1
    var=`expr $var+1`
    echo $var   #output result: 2
    # expr supports: |, &, <, <=, =, !=, >=, >, +, -, *, /, %
    # supports only integer arithmetic.
    
    var=1
    var=`echo "$var+1"|bc`
    echo $var   #output result: 2
    # bc supports float arithmetic.
    
    var=1
    var=`echo "$var 1"|awk '{printf("%g",$1*$2)}'`
    echo $var   #output result: 2
    # awk supports float arithmetic.

## Function

###Define function
    [ function ] function_name [()] {
        CONSEQUENT-COMMANDS;
        [return int;]
    }

###Load function

####shell test
    #!/bin/bash
    . hello     #load file hello
    
    hello       #call function hello()

####shell hello
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

## Font and colors

###coding
    coding  color/action
    0       reset to the default settings
    1       set bold on
    2       set half brightness on
    4       set underscore on
    5       set flashing on
    7       set reverse image on
    22      set general density
    24      set underscore off
    25      set flashing off
    27      set reverse image off
    30      set black foreground
    31      set red foreground
    32      set green foreground
    33      set brown foreground
    34      set blue foreground
    35      set purple foreground
    36      set cyan foreground
    37      set white foreground
    38      set underscore on in default foreground
    39      set underscore off in default foreground
    40      set black background
    41      set red background
    42      set green background
    43      set brown background
    44      set blue background
    45      set purple background
    46      set cyan background
    47      set white background
    49      set the default black background

###Others
    \033[2J     Clear screen
    \033[0q     Close all keyboard lights
    \033[1q     Settings "Scroll Lock" indicator (Scroll Lock)
    \033[2q     Settings "Value Lock" indicator (Num Lock)
    \033[3q     Settings "caps lock" indicator (Caps Lock)
    \033[15:40H move to the closed line 15, 40
    \007        Hair Health beep beep

###examples
    echo -e "\033[32;49;1m [DONE] \033[39;49;0m"
    echo -e "\033[44;37;5m ME \033[0m COOL"

## Q&A

## Examples

###Shell menu
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

## REFERENCES
- <http://blog.sina.com.cn/s/blog_8f31e5b10100zjpr.html>
- <http://wayne173.iteye.com/blog/938202>
- <http://guoyunsky.iteye.com/blog/1671338>
- <http://www.gnu.org/software/sed/manual/sed.html>
- <http://fyan.iteye.com/blog/1087242>
- <http://www.blogjava.net/alwayscy/archive/2009/09/01/293409.html>
- <http://blog.sina.com.cn/s/blog_6a1837e901011024.html>
- <http://blog.csdn.net/runming918/article/details/7226507>
- <http://andrew913.iteye.com/blog/277801>
- <http://www.cnblogs.com/kaituorensheng/archive/2012/12/19/2825376.html>
- <http://www.wenzizone.cn/?p=313>
- <http://blog.163.com/clevertanglei900@126/blog/static/111352259201162553652150/>
- <http://hi.baidu.com/ajarne/item/a871b7f9d30411c60dd1c80f>
- <http://bbs.chinaunix.net/forum.php?mod=viewthread&tid=218853>

