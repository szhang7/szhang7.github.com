---
layout: post
title: "Ubuntu Manual"
description: "Outline how to use Ubuntu."
category: ubuntu
tags: [ubuntu, Manual, fdisk, mount, fstab]
---
{% include JB/setup %}

## Keyborad Shortcuts

    Ctrl + Shift + N    # Create New Folder, Very useful shortcut
    Ctrl + Alt + T      # Open new Terminal window
    Ctrl + Alt + L      # Quick shortcut to Lock Screen
    Ctrl + 1/2          # Change folder view to icon/list.
    Ctrl + T            # Open a new tab in Nautilus
    Ctrl + W            # close current Nautilus Window
    Ctrl + H            # Toggle Display of hidden files and folders
    Alt + Enter         # Show properties of a selected file/folder
    Alt + Home          # Move directly to your Home Folder

    F9                  # Toggle display of Nautilus Sidepane

## Ubuntu One

    Share a folder outside the home folder.
    $ mount --bind /path/to/folder /home/username/folder_to_sync
    # This should make the contents of /path/to/folder available in both places
 
    Unbuntu-one doesn't support symlinks, but it might support binding mounts. If it does work, you can add a line to /etc/fstab
    /path/to/folder/ /home/username/forlder_to_sync none bind 0 0
    That way it will alsways mount on boot.
    
(Read more: <http://askubuntu.com/questions/78924/is-it-possible-to-share-a-folder-using-ubuntu-one-outside-the-home-folder>)

## Chinese Input Method

    System->Startup Application->Add    # Config ibus
    Name:   ibus
    Command:/usr/bin/ibus-daemon
    Comment:ibus

    $sudo apt-get install ibus-googlepinyin     #谷歌拼音输入法
    $sudo apt-get install ibus-sunpinyin        #Sun 拼音输入法

## Cairo-dock2

    $ sudo apt-get install cairo-dock
    
    System->Startup Application->Add
    /usr/bin/cairo-dock -o                      #Cairo-Dock with OpenGL
    /usr/bin/cairo-dock -c                      #Cairo-Dock without OpenGL

(Read more: <http://wobu.blog.163.com/blog/static/170709620124110715716/>)

## Optimize memory

    $ cat /proc/sys/vm/swappiness
    $ sudo sysctl vm.swappiness=10              # 10--1G memory
    $ sudo chmod +w /etc/rc.local               # Lont-term effect
    $ sudo vi /etc/rc.local
    $ echo 10 > /proc/sys/vm/swappiness         # append to the end, then save and quit
    $ sudo chmod -w /etc/rc.local

(Read more: <http://blog.163.com/lixiangqiu_9202/blog/static/535750372011849522739/>)

## Solve rhythmbox Chinse garbled--解决中文乱码

    $ sudo apt-get install python-mutagen       # install mid3iconv
    $ cd ~/Music                                # go to music directory
    $ mid3iconv -e GBK *.mp3                    # converts ID3 tags from GBK to UTF-8

## Samba server configuration

    $ sudo apt-get install samba smbfs          # install Samba Server
    $ sudo apt-get install system-config-samba  # Samba Server Configuration
    $ sudo apt-get install winbind              # synchronize user account of linux and windows
    $ sudo gedit /etc/samba/smb.conf            # Samba configuration file
    [global]
    workgroup = WORKGROUP                       # windows workgroup
    netbios name = ubuntu                       # computer name(terminal, after @)
    
    ;name resolve order = lmhosts host wins bcast # remove ;
    Then, saved and close gedit
    
    $ sudo gedit /etc/nsswitch.conf
    hosts: files mdns4_minimal [NOTFOUND=return] dns mdns4  # changed to
    hosts: files mdns4_minimal [NOTFOUND=return] wins dns mdns4
    Then, saved and close gedit
    
    Finally, restart samba and winbind
    $ sudo /etc/init.d/samba restart
    $ sudo /etc/init.d/winbind restart

    $ sudo system-config-samba                  # start Samba Server Configuration
    or system-->Administration-->Samba

    Optional
    $ sudo apt-get install nautilus-share       # File Manager

###Q & A
    $ sudo /etc/init.d/samba restart            # command not found
    $ sudo apt-get install samba-common-bin     # install common bin
    $ sudo cp /etc/cron.daily/samba /etc/init.d/
    
(Read more: <http://blog.sina.com.cn/s/blog_502691720100w8dl.html>)

## Load windows partition

    $ sudo fdisk -l                            # list partition table(s)
    $ ls -al /dev/disk/by-uuid                 # or sudo blkid -- list uuid
    $ sudo gedit /etc/fstab                    # Open fstab to edit, add the followings:
    # mount /dev/sda5
    # /dev/sda5   /data   ntfs-3g    defaults,user,uid=1000,gid=1000,locale=en_US.UTF-8    0    0
    UUID=00029B5700040ACB /data   ntfs-3g    defaults,user,exec,uid=1000,gid=1000,locale=en_US.UTF-8    0    0
    $ sudo mount -a                            # or restart your computer.

(Read more: <http://blog.chinaunix.net/uid-25100840-id-271088.html>)

## Install skype

    $ sudo add-apt-repository "deb http://archive.canonical.com/ $(lsb_release -sc) partner"
    $ sudo apt-get update && sudo apt-get install skype
    
(Read more: <https://help.ubuntu.com/community/Skype>)

## Can't find wireless

    $ sudo gedit /etc/NetworkManager/NetworkManager.conf
    [ifupdown]
    managed=false --> true                                  # modify false to true
    $ sudo gedit /etc/network/interfaces
    auto lo
    iface lo inet loopback                                  # only remain the two lines.
    $ sudo mv /etc/resolvconf/ /etc/resolvconf_backup       # delete dns settings
    $ sudo service network-manager restart                  # restart network-manager then you'll see wifi
    
    Set static ip
    Edit connections->Wireless->IPv4 Settings
    Address: 192.168.2.20
    Netmask: 255.255.255.0
    Gateway: 192.168.2.1
    DNS: 8.8.8.8 or 202.102.128.68                          # Unicom

## Mount Windows Share folder

    $ sudo apt-get install smbfs        # install smbfs if not installed
    $ mkdir ~/windows                   # make directory to be mount point
    $ chmod -R 777 ~/windows            # modify the permission
    $ sudo smbmount //\<ip\>/\<windows sharing folder\> /\<mount point\> -o username=\<windows username\>,rw
    $ sudo umount \<mount point\>       # umount mount point
    For example
    $ sudo smbmount //192.168.2.10/d/Music ~/windows -o username=admin,uid=1000,gid=1000,rw
    $ sudo umount ~/windows
    
## Extract software

    $ sudo apt-get install p7zip-full   # install p7zip
    $ 7z x file                         # Extract file
    $ sudo apt-get install rar          # Install rar
    $ rar e file.rar                    # Extract file.rar

### Q & A

####Q1. Chinese garbled.
 
A1. install unrar

    $ sudo apt-get remove rar
    $ sudo apt-get install unrar
    
A2. install p7zip

    $ sudo apt-get install p7zip-rar

(Read more: <http://www.cnblogs.com/feng_013/archive/2012/04/23/2466224.html>)

## Alias

    alias [name]=[value]
    $ gedit ~/.bashrc                   # alias configure file
    alias ll='ls -alF'                  # for example
    
    $ source .bashrc

**Note** be sure to add '/' at the end of the directory name, otherwise prompt error.

## Linux/Unix Commands

###chown
Change the owner and/or group of each FILE to OWNER and/or GROUP.

    chown [OPTION]... [OWNER][:[GROUP]] FILE...
    Examples:
    chown root /u       # Change the owner of /u to "root"
    chown root:staff /u # Likewise, but also change its group to "staff".
    chown -hR root /u   # Change the owner of /u and subfiles to "root".

###chgrp
Chage the group of each FILE to GROUP

    chgrp [OPTION]... GROUP FILE...
    Examples:
    chgrp staff /u      Change the group of /u to "staff".
    chgrp -hR staff /u  Change the group of /u and subfiles to "staff".

###chmod
Change the mode of each FILE to MODE.

    chmod [OPTION]... MODE[,MODE]... FILE...
    Each MODE is of the form `[ugoa]*([-+=]([rwxXst]*|[ugo]))+'.
 
###source
Re-run the initialization file just modified to make it take effect immediately, without having to restart the system.

    source filename [arguments]

###id
Print user and group information for the specified USERNAME, or (when USERNAME omitted) for the current user.

    id [OPTION]... [USERNAME]

###mkdir
Create the DIRECTORY(ies), if they do not already exist.

     mkdir [OPTION]... DIRECTORY...

###rmdir
Remove the DIRECTORY(ies), if they are empty.

    rmdir [OPTION]... DIRECTORY...

###rm
Remove (unlink) the FILE(s).

    rm [OPTION]... FILE...
    rm -rf DIRECTORY            # Remove an unempty directory

###touch
Create new file, Update the access and modification times of each FILE to the current time.

    touch [OPTION]... FILE...

###mv
Rename SOURCE to DEST, or move SOURCE(s) to DIRECTORY.

    mv [OPTION]... SOURCE... DIRECTORY
    mv file1 file2              # rename file1 to file2

###rename
Rename filenames.

    rename [-v] [-n] [-f] perlexpr [filenames]
    rename foo foo0 foo?        # rename foo1--foo9 to foo01--foo09
    rename foo foo0 foo??       # rename foo01--foo99 to foo001--foo099
    rename foo foo0 foo*        # rename foo001--foo999 to foo0001--foo0999
    rename foo0 foo foo0[2]*    # rename foo0200--foo0299 to foo200--foo299

###tput
Initialize a terminal or query terminfo database.

    tput init                   # Initialize the terminal according to the type of terminal in the environment variable TERM.
    tput -T5620 reset           # Reset an AT&T 5620 terminal.
    tput cup 0 0                # Send the sequence to mvoe the cursor to row 0, column 0.
    tput clear                  # Echo the clear-screen sequence for the current terminal.
    tput cols                   # Print the number of columns for the current terminal.
    
(Read more: <http://linux.about.com/library/cmd/blcmdl1_tput.htm>)

###echo
display a line of text.

    echo [OPTION]...[STRING]...
    -n      # do not output the trailing newline
    -e      # enable interpretation of the backslash-escaped characters listed below.
    -E      # disable interpretation of those sequences in STRINGs
    Without -E, the following sequences are recognized and interpolated:
    \NNN    # the character whose ASCII code is NNN(octal)
    \\      # backslash
    \a      # alert(BELL)
    \b      # backspace
    \c      # suppress trailing newline
    \f      # form feed
    \n      # new line
    \v      # vertical tab

(Read more: <http://linux.about.com/library/cmd/blcmdl1_echo.htm>)

Set the terminal title

    echo -ne "\033]0;$MY_TITLE\007"

###read
Use to get input (data from user) from keyboard and store (data) to variable.

    read variable1, variable2,...,variableN

(Read more: <http://freeos.com/guides/lsst/ch02sec10.html>)

###while
Execute script repeatedly as long as a condition is met.

    while [condition]
    do
        command1
        command2
        ...
    done                    # end do

(Read more: <http://freeos.com/guides/lsst/ch03sec07.html>)

###if...else...fi
If given condition is true then command1 is executed otherwise command2 is executed.

    if condition
    then
        condition is zero(true - 0)
        execute all commands to else statement
    else
        if condition is not true then
        execute all commands up to fi
    fi                      # end if

(Read more: <http://freeos.com/guides/lsst/ch03sec03.html>)

###test command or \[ expr \]
test command or \[ expr \] is used to see if an expression is true, and if it is true it return zero(0), otherwise returns nonzero for false.

    test expression OR [ expression ]

####Mathematical operators
    -eq	is equal to	                5 == 6	    if test 5 -eq 6	    if [ 5 -eq 6 ]
    -ne	is not equal to	            5 != 6	    if test 5 -ne 6	    if [ 5 -ne 6 ]
    -lt	is less than	            5 < 6	    if test 5 -lt 6	    if [ 5 -lt 6 ]
    -le	is less than or equal to	5 <= 6	    if test 5 -le 6	    if [ 5 -le 6 ]
    -gt	is greater than	            5 > 6	    if test 5 -gt 6	    if [ 5 -gt 6 ]
    -ge	is greater than or equal to	5 >= 6	    if test 5 -ge 6	    if [ 5 -ge 6 ]

####String comparisons
    string1 = string2	string1 is equal to string2
    string1 != string2	string1 is NOT equal to string2
    string1	            string1 is NOT NULL or not defined 
    -n string1	        string1 is NOT NULL and does exist
    -z string1	        string1 is NULL and does exist

####Test for file and directory types
    -s file   	Non empty file
    -f file   	Is File exist or normal file and not a directory 
    -d dir    	Is Directory exist and not a file
    -w file  	Is writeable file
    -r file   	Is read-only file
    -x file   	Is file is executable

####Logical Operators
    ! expression	                Logical NOT
    expression1 -a expression2	    Logical AND
    expression1 -o expression2	    Logical OR

Read more:

- <http://freeos.com/guides/lsst/ch03sec02.html>
- <http://www.tldp.org/LDP/Bash-Beginners-Guide/html/sect_07_01.html>
- <http://andrew913.iteye.com/blog/277801>

###for Loop
    for {variable name} in {list}
    do
        execute one for each item in the list until the list is
        not finished (And repeat all statement between do and done)
    done

(Read more: <http://freeos.com/guides/lsst/ch03sec06.html>)

###The case Statement
The case statement is good alternative to Multilevel if-then-else-fi statement. It enable you to match several values against one variable. Its easier to read and write.

    case $variable-name in
    pattern1)
        command
        ...
        command;;
    pattern2)
        command
        ...
        command;;
    ...
    patternN)
        command
        ...
        command;;
    *)
        command
        ...
        command;;
    esac                        # end case

The `$variable-name` is compared against the patterns until a match is found. The shell then executes all the statements up to the two semicolons that are next to each other. The default is `*)` and its executed if no match is found.

###netstat
    netstat [-vWnNcaeol] [<Socket> ...]
    
    $ sudo netstat -tap | grep mysql          # list mysql ip port

###nm-tool
NetworkManager Tool, list devices, IPv4 settings(address, gateway,DNS)
    
    $ nm-tool

###sed
sed is a stream editor. A stream editor is used to perform basic text transformations on an input stream (a file or input from a pipeline).

    sed OPTIONS... [SCRIPT] [INPUTFILE...]

####command-line options
    -n, --quiet, --silent
                 suppress automatic printing of pattern space
    -e script, --expression=script
                 add the script to the commands to be executed
    -f script-file, --file=script-file
                 add the contents of script-file to the commands to be executed
    --follow-symlinks
                 follow symlinks when processing in place
    -i[SUFFIX], --in-place[=SUFFIX]
                 edit files in place (makes backup if extension supplied)
    -l N, --line-length=N
                 specify the desired line-wrap length for the `l' command
    --posix
                 disable all GNU extensions.
    -r, --regexp-extended
                 use extended regular expressions in the script.
    -s, --separate
                 consider files as separate rather than as a single continuous
                 long stream.
    -u, --unbuffered
                 load minimal amounts of data from the input files and flush
                 the output buffers more often
    --help     display this help and exit
    --version  output version information and exit

####The s Command
The syntax of the s (as in substitute) command is ‘s/regexp/replacement/flags’.

The s command can be followed by zero or more of the following flags: 

    g   Apply the replacement to all matches to the regexp, not just the first. 
    i   The I modifier to regular-expression matching is a GNU extension which makes sed match regexp in a case-insensitive manner. 
    p   If the substitution was made, then print the new pattern space. 

(Read more: <http://www.gnu.org/software/sed/manual/sed.html>)

###cp
Copy SOURCE to DEST, or multiple SOURCE(s) to DIRECTORY.

    cp [OPTION]... [-T] SOURCE DEST
    cp [OPTION]... SOURCE... DIRECTORY
    cp [OPTION]... -t DIRECTORY SOURCE...

####Parameters
    -f, --force                  if an existing destination file cannot be
                                 opened, remove it and try again (redundant if
                                 the -n option is used)
    -i, --interactive            prompt before overwrite (overrides a previous -n
                                  option)
    -R, -r, --recursive          copy directories recursively
      --reflink[=WHEN]           control clone/CoW copies. See below
      --remove-destination       remove each existing destination file before
                                 attempting to open it (contrast with --force)
      --sparse=WHEN              control creation of sparse files. See below
      --strip-trailing-slashes   remove any trailing slashes from each SOURCE
                                 argument
    -t, --target-directory=DIRECTORY  copy all SOURCE arguments into DIRECTORY
    -T, --no-target-directory    treat DEST as a normal file

###Linux System Services
Services are put into /etc/init.d

    update-rc.d mysqld defaults     #Create service mysqld
    update-rc.d -f mysqld remove    #Delete service mysqld

(Read more: <http://blog.sina.com.cn/s/blog_79159ef50100z1ax.html>)

