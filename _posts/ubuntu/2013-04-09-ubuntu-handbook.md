---
layout: post
title: "Ubuntu Handbook"
description: "Outline how to use Ubuntu."
category: ubuntu
tags: [ubuntu, Handbook, fdisk, mount, fstab]
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

## start a program automatically on boot
    $ sudo gedit /etc/init.d/aa
    #!/bin/bash
    mplayer /home/aa.avi -fs -vo fbdev -vf scale=800:600
    
    $ sudo chmod 755 /etc/init.d/aa
    $ sudo ln -s /etc/init.d/aa /etc/rc2.d/S100aa

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

###Solution 1
    $ sudo apt-get install python-mutagen       # install mid3iconv
    $ cd ~/Music                                # go to music directory
    $ mid3iconv -e GBK *.mp3                    # converts ID3 tags from GBK to UTF-8

###Solution 2
    function Rhythmbox_garbled() {
    #--begin
    local FILE_NAME
    FILE_NAME=~/.profile
    if ( test -f "$FILE_NAME") then
      COUNT=$(grep -ic 'GST_ID3_TAG_ENCODING' "$FILE_NAME")
      if( test $COUNT = 0 ) then
        sed -i '$a \
    export GST_ID3_TAG_ENCODING=GBK:UTF-8:GB18030\
    export GST_ID3V2_TAG_ENCODING=GBK:UTF-8:GB18030' "${FILE_NAME}"
        #echo "export GST_ID3_TAG_ENCODING=GBK:UTF-8:GB18030" >> "${FILE_NAME}"
        #echo "export GST_ID3V2_TAG_ENCODING=GBK:UTF-8:GB18030" >> "${FILE_NAME}"
        source ${FILE_NAME}
      fi
    else
      echo "[ERROR] $FILE_NAME not exist"
      return 1
    fi
    #--end
    }

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

### Mapping different usernames
    $ sudo gedit /etc/samba/smb.conf
    
    [global]
    ;username map = /etc/samba/smbusers         # remove ;
    
    Then save and close gedit.
    
    $ sudo gedit /etc/samba/smbusers
    
    sam = admin
    # sam(ubuntu username) is mapped to admin(win7 username)
    
    If you set the same password, then you can use admin to log into samba.
    $ sudo smbpasswd -a sam
    ****
    ****

### Samba ports
    1）Port 137 (UDP) - NetBIOS 名字服务 ； nmbd
    2）Port 138 (UDP) - NetBIOS 数据报服务
    3）Port 139 (TCP) - 文件和打印共享 ； smbd （基于SMB(Server Message Block)协议，主要在局域网中使用，文件共享协议）
    4）Port 389 (TCP) - 用于 LDAP (Active Directory Mode)
    5）Port 445 (TCP) - NetBIOS服务在windos 2000及以后版本使用此端口, (Common Internet File System，CIFS，它是SMB协议扩展到Internet后，实现Internet文件共享)
    6）Port 901 (TCP) - 用于 SWAT，用于网页管理Samba

###Q & A

####1. no samba command
    $ sudo /etc/init.d/samba restart            # command not found
    $ sudo apt-get install samba-common-bin     # install common bin
    $ sudo cp /etc/cron.daily/samba /etc/init.d/

####2. Can't connect to smb server
    $ sudo ufw enable
    $ sudo ufw allow 445
    $ smbclient -L //localhost/data
    
    # ufw commands
    $ sudo ufw disable                          # disable the firewall
    $ sudo ufw enable                           # enable  the firewall
    $ sudo ufw status                           # show firewall status
    $ sudo ufw default ARG                      # set default policy
    $ sudo allow ARGS                           # add allow rule
    $ sudo allow 445                            # allow port 445 (samba port)
    $ sudo deny ARGS                            # add deny rule
    $ sudo deny 8080                            # deny port 8080
    $ sudo ufw delete RULE|NUM                  # delete RULE
    $ sudo ufw delete allow 139
    
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

## Click the right mouse button to open a terminal in the current directory
    $ gedit ~/.gnome2/nautilus-scripts/open\ in\ terminal
    
    #!bin/bash
    gnome-terminal --working-directory=$PWD
    
    After saving it, click the right mouse button on the directory you want to run the terminal. Scripts-->open in terminal

## Install skype

    $ sudo add-apt-repository "deb http://archive.canonical.com/ $(lsb_release -sc) partner"
    $ sudo apt-get update && sudo apt-get install skype
    
(Read more: <https://help.ubuntu.com/community/Skype>)

## AsciiDoc
AsciiDoc is a text document format for writing notes, documentation, articles, books, ebooks, slideshows, web pages, man pages and blogs. AsciiDoc files can be translated to many formats including HTML, PDF, EPUB, man page.

    $ sudo apt-get install asciidoc

(Read more: <http://www.methods.co.nz/asciidoc/>)

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

## axel
    $ sudo apt-get install axel
    $ axel http://svn.hyperic.org/projects/sigar_bin/dist/SIGAR_1_6_4/lib/libsigar-x86-linux.so
    Usage: axel [options] url1 [url2] [url...]

    --max-speed=x		-s x	Specify maximum speed (bytes per second)
    --num-connections=x	-n x	Specify maximum number of connections
    --output=f		-o f	Specify local output file
    --search[=x]		-S [x]	Search for mirrors and download from x servers
    --header=x		-H x	Add header string
    --user-agent=x		-U x	Set user agent
    --no-proxy		-N	Just don't use any proxy server
    --quiet			-q	Leave stdout alone
    --verbose		-v	More status information
    --alternate		-a	Alternate progress indicator
    --help			-h	This information
    --version		-V	Version information


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

    if condition    #0-->true-->then, condition not support integar variable.
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

###grep
Search for PATTERN in each FILE or standard input.

    grep [OPTION]... PATTERN [FILE]...

####Example:
    grep -i 'hello world' menu.h main.c
    grep -rn "hello,world!" ./              #search "hello,world!" in current directory and sub directories.

####Regexp selection and interpretation:
    -E, --extended-regexp     PATTERN is an extended regular expression (ERE)
    -F, --fixed-strings       PATTERN is a set of newline-separated fixed strings
    -G, --basic-regexp        PATTERN is a basic regular expression (BRE)
    -P, --perl-regexp         PATTERN is a Perl regular expression
    -e, --regexp=PATTERN      use PATTERN for matching
    -f, --file=FILE           obtain PATTERN from FILE
    -i, --ignore-case         ignore case distinctions
    -w, --word-regexp         force PATTERN to match only whole words
    -x, --line-regexp         force PATTERN to match only whole lines
    -z, --null-data           a data line ends in 0 byte, not newline

####Miscellaneous:
    -s, --no-messages         suppress error messages
    -v, --invert-match        select non-matching lines
    -V, --version             print version information and exit
      --help                display this help and exit
      --mmap                ignored for backwards compatibility

####Output control:
    -m, --max-count=NUM       stop after NUM matches
    -b, --byte-offset         print the byte offset with output lines
    -n, --line-number         print line number with output lines
      --line-buffered       flush output on every line
    -H, --with-filename       print the file name for each match
    -h, --no-filename         suppress the file name prefix on output
      --label=LABEL         use LABEL as the standard input file name prefix
    -o, --only-matching       show only the part of a line matching PATTERN
    -q, --quiet, --silent     suppress all normal output
      --binary-files=TYPE   assume that binary files are TYPE;
                            TYPE is `binary', `text', or `without-match'
    -a, --text                equivalent to --binary-files=text
    -I                        equivalent to --binary-files=without-match
    -d, --directories=ACTION  how to handle directories;
                            ACTION is `read', `recurse', or `skip'
    -D, --devices=ACTION      how to handle devices, FIFOs and sockets;
                            ACTION is `read' or `skip'
    -R, -r, --recursive       equivalent to --directories=recurse
      --include=FILE_PATTERN  search only files that match FILE_PATTERN
      --exclude=FILE_PATTERN  skip files and directories matching FILE_PATTERN
      --exclude-from=FILE   skip files matching any file pattern from FILE
      --exclude-dir=PATTERN  directories that match PATTERN will be skipped.
    -L, --files-without-match  print only names of FILEs containing no match
    -l, --files-with-matches  print only names of FILEs containing matches
    -c, --count               print only a count of matching lines per FILE
    -T, --initial-tab         make tabs line up (if needed)
    -Z, --null                print 0 byte after FILE name

####Context control:
    -B, --before-context=NUM  print NUM lines of leading context
    -A, --after-context=NUM   print NUM lines of trailing context
    -C, --context=NUM         print NUM lines of output context
    -NUM                      same as --context=NUM
      --color[=WHEN],
      --colour[=WHEN]       use markers to highlight the matching strings;
                            WHEN is `always', `never', or `auto'
    -U, --binary              do not strip CR characters at EOL (MSDOS)
    -u, --unix-byte-offsets   report offsets as if CRs were not there (MSDOS)

    `egrep' means `grep -E'.  `fgrep' means `grep -F'.

###type
Display information about command type.

    help type           #see type help
    type [-afptP] name [name ...]

####Options:
    -a	display all locations containing an executable named NAME;
        includes aliases, builtins, and functions, if and only if
        the `-p' option is not also used
    -f	suppress shell function lookup
    -P	force a PATH search for each NAME, even if it is an alias,
        builtin, or function, and returns the name of the disk file
        that would be executed
    -p	returns either the name of the disk file that would be executed,
        or nothing if `type -t NAME' would not return `file'.
    -t	output a single word which is one of `alias', `keyword',
        `function', `builtin', `file' or `', if NAME is an alias, shell
        reserved word, shell function, shell builtin, disk file, or not
        found, respectively

####Examples
    type -t NAME
    type -t init_pr

###wc
Print newline, word, and byte counts for each FILE, and a total line if more than one FILE is specified.  With no FILE, or when FILE is -, read standard input.  A word is a non-zero-length sequence of characters delimited by white space.

    wc [OPTION]... [FILE]...
    wc [OPTION]... --files0-from=F

####options
    -c, --bytes            print the byte counts
    -m, --chars            print the character counts
    -l, --lines            print the newline counts
        --files0-from=F    read input from the files specified by
                           NUL-terminated names in file F;
                           If F is - then read names from standard input
    -L, --max-line-length  print the length of the longest line
    -w, --words            print the word counts
        --help     display this help and exit
        --version  output version information and exit

###tee
Copy standard input to each FILE, and also to standard output.

    tee [OPTION]... [FILE]...

####Options
    -a, --append              append to the given FILEs, do not overwrite
    -i, --ignore-interrupts   ignore interrupt signals
        --help     display this help and exit
        --version  output version information and exit

If a FILE is -, copy again to standard output.

###find

    find [-H] [-L] [-P] [-Olevel] [-D help|tree|search|stat|rates|opt|exec] [path...] [expression]

default path is the current directory; default expression is -print expression may consist of: operators, options, tests, and actions:

####operators
    (decreasing precedence; -and is implicit where no others are given):
    ( EXPR )   ! EXPR   -not EXPR   EXPR1 -a EXPR2   EXPR1 -and EXPR2
    EXPR1 -o EXPR2   EXPR1 -or EXPR2   EXPR1 , EXPR2

####positional options (always true):
    -daystart -follow -regextype

####normal options (always true, specified before other expressions):
    -depth --help -maxdepth LEVELS -mindepth LEVELS -mount -noleaf
    --version -xdev -ignore_readdir_race -noignore_readdir_race

####tests (N can be +N or -N or N): -amin N -anewer FILE -atime N -cmin N
    -cnewer FILE -ctime N -empty -false -fstype TYPE -gid N -group NAME
    -ilname PATTERN -iname PATTERN -inum N -iwholename PATTERN -iregex PATTERN
    -links N -lname PATTERN -mmin N -mtime N -name PATTERN -newer FILE
    -nouser -nogroup -path PATTERN -perm [+-]MODE -regex PATTERN
    -readable -writable -executable
    -wholename PATTERN -size N[bcwkMG] -true -type [bcdpflsD] -uid N
    -used N -user NAME -xtype [bcdpfls]

####actions: -delete -print0 -printf FORMAT -fprintf FILE FORMAT -print 
    -fprint0 FILE -fprint FILE -ls -fls FILE -prune -quit
    -exec COMMAND ; -exec COMMAND {} + -ok COMMAND ;
    -execdir COMMAND ; -execdir COMMAND {} + -okdir COMMAND ;

###xargs

    xargs [-0prtx] [--interactive] [--null] [-d|--delimiter=delim]
    [-E eof-str] [-e[eof-str]]  [--eof[=eof-str]]
    [-L max-lines] [-l[max-lines]] [--max-lines[=max-lines]]
    [-I replace-str] [-i[replace-str]] [--replace[=replace-str]]
    [-n max-args] [--max-args=max-args]
    [-s max-chars] [--max-chars=max-chars]
    [-P max-procs]  [--max-procs=max-procs] [--show-limits]
    [--verbose] [--exit] [--no-run-if-empty] [--arg-file=file]
    [--version] [--help] [command [initial-arguments]]

###seq
Print numbers from FIRST to LAST, in steps of INCREMENT.

    seq [OPTION]... LAST
    seq [OPTION]... FIRST LAST
    seq [OPTION]... FIRST INCREMENT LAST

####Options
    -f, --format=FORMAT      use printf style floating-point FORMAT
    -s, --separator=STRING   use STRING to separate numbers (default: \n)
    -w, --equal-width        equalize width by padding with leading zeroes
    --help     display this help and exit
    --version  output version information and exit

    If FIRST or INCREMENT is omitted, it defaults to 1.  That is, an omitted INCREMENT defaults to 1 even when LAST is smaller than FIRST. FIRST, INCREMENT, and LAST are interpreted as floating point values. INCREMENT is usually positive if FIRST is smaller than LAST, and INCREMENT is usually negative if FIRST is greater than LAST. FORMAT must be suitable for printing one argument of type `double'; it defaults to %.PRECf if FIRST, INCREMENT, and LAST are all fixed point decimal numbers with maximum precision PREC, and to %g otherwise.


