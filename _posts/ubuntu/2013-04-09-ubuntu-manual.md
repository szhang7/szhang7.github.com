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
 

## Samba server configuration

    $ sudo apt-get install samba smbfs          # install Samba Server
    $ sudo apt-get install system-config-samba  # Samba Server Configuration
    $ sudo apt-get install winbind              # synchronize user account of linux and windows
    $ sudo system-config-samba                  # start Samba Server Configuration
    system-->Administration-->Samba
 

    /etc/samba/smb.conf                         # Samba configuration file
 

    Optional
    $ sudo apt-get install nautilus-share       # File Manager
 

(Read more: <http://blog.sina.com.cn/s/blog_502691720100w8dl.html>)

## Load windows partition

    cbay@ubuntu:~$ sudo fdisk -l        # list partition table(s)
    [sudo] password for cbay: 

    Disk /dev/sda: 80.0 GB, 80026361856 bytes
    255 heads, 63 sectors/track, 9729 cylinders, total 156301488 sectors
    Units = sectors of 1 * 512 = 512 bytes
    Sector size (logical/physical): 512 bytes / 512 bytes
    I/O size (minimum/optimal): 512 bytes / 512 bytes
    Disk identifier: 0xfcedc925

       Device Boot      Start         End      Blocks   Id  System
    /dev/sda1   *          63    51199154    25599546    7  HPFS/NTFS/exFAT
    /dev/sda2        51199155   156280319    52540582+   f  W95 Ext'd (LBA)
    /dev/sda5        51199218   156280319    52540551    7  HPFS/NTFS/exFAT
    cbay@ubuntu:~$ sudo gedit /etc/fstab

    Open fstab to edit, add the following:
    /dev/sda5 /data ntfs defaults,locale=en_US.UTF-8 0 0   # mount /dev/sda5
    Finally, restart your computer.

## Extract the 7z file

    $ sudo apt-get install p7zip-full   # install p7zip
    $ 7z x file                         # Extract file
 

## Common Commands

**chown**

Change the owner and/or group of each FILE to OWNER and/or GROUP.

    chown [OPTION]... [OWNER][:[GROUP]] FILE...
    Examples:
    chown root /u       # Change the owner of /u to "root"
    chown root:staff /u # Likewise, but also change its group to "staff".
    chown -hR root /u   # Change the owner of /u and subfiles to "root".
 

**chgrp**

Chage the group of each FILE to GROUP

    chgrp [OPTION]... GROUP FILE...
    Examples:
    chgrp staff /u      Change the group of /u to "staff".
    chgrp -hR staff /u  Change the group of /u and subfiles to "staff".
 

**chmod**

Change the mode of each FILE to MODE.

    chmod [OPTION]... MODE[,MODE]... FILE...
    Each MODE is of the form `[ugoa]*([-+=]([rwxXst]*|[ugo]))+'.
 
**source**

Re-run the initialization file just modified to make it take effect immediately, without having to restart the system.

    source filename [arguments]


