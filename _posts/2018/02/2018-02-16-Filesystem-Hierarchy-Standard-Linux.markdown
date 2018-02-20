---
layout: post
title: "Filesystem Hierarchy Standard"
date: 2018-02-16 14:00:00 +0800
categories: Linux
---
# Filesystem Hierarchy Standard(FHS)
FHS主页：http://www.pathname.com/fhs/
FHS从两个不同的方面定义文件：shareable vs. unshareable 和 variable vs. static。一般来说在这两个方面不同的文件需要放置在不同的目录中。
shareable（可分享的）:
指那些被保存在一个主机上可以在其他机器上使用的文件。
unshareable（不可分享的）:
指那些只在自己机器上使用的文件。
static（不变的）:
包括二进制文件（binaries）、库文件（libraries）、文档文件（documentation files）和其他只有系统管理员才可修改的文件。
variable（可变动的）:
非static的文件。

## The Root Filesystem
/ （root，根目录）：root filesystem中的内容必须可以胜任boot、restore、recover、and/or repair系统。

### Requirements
/下必须包含以下目录或至目录的符号链接:

|Directory|Description|
|:-:|:-:|
|bin|Essential command binaries|
|boot|Static files of the boot loader|
|dev|Device files|
|etc|Host-specific system configuration|
|lib|Essential shared libraries and kernel modules|
|media|Mount point for removeable media|
|mnt|Mount point for mounting a filesystem temporarily|
|opt|Add-on application software packages|
|sbin|Essential system binaries|
|srv|Data for services provided by this system|
|tmp|Temporary files|
|usr|Secondary hierarchy|
|var|Variable data|

### Specific Options
以下目录或至目录的符号链接必须在/下，如果有安装相应的子系统:

|Directory|Description|
|:-:|:-:|
|home|User home directories(optional)|
|lib\<qual\>|Alternate format essential shared libraries(optional)|
|root|Home directory for the root user(optional)|

## /bin
Essential user command binaries (for use by all users)

### Requirements

|Command|Description|
|:-:|:-:|
|cat|Utility to concatenate files to standard output|
|chgrp|Utility to change file group ownership|
|chmod|Utility to change file access permissions|
|chown|Utility to change file owner and group|
|cp|Utility to copy files and directories|
|date|Utility to print or set the system data and time|
|dd|Utility to convert and copy a file|
|df|Utility to report filesystem disk space usage|
|dmesg|Utility to print or control the kernel message buffer|
|echo|Utility to display a line of text|
|false|Utility to do nothing, unsuccessfully|
|hostname|Utility to show or set the system's host name|
|kill|Utility to send signals to processes|
|ln|Utility to make links between files|
|login|Utility to begin a session on the system|
|ls|Utility to list directory contents|
|mkdir|Utility to make directories|
|mknod|Utility to make block or character special files|
|more|Utility to page through text|
|mount|Utility to mount a filesystem|
|mv|Utility to move/rename files|
|ps|Utility to report process status|
|pwd|Utility to print name of current working directory|
|rm|Utility to remove files or directories|
|rmdir|Utility to remove empty directories|
|sed|The 'sed' stream editor|
|sh|The Bourne command shell|
|stty|Utility to change and print terminal line settings|
|su|Utility to change user ID|
|sync|Utility to flush filesystem buffers|
|true|Utility to do nothing, successfully|
|umount|Utility to unmount file systems|
|uname|Utility to print system information|

如果/bin/sh不是真的Bourne shell，也必须是指向真的shell命令的硬链接或符号链接。
[和test命令必须放置在同一目录下，或是/bin或是/usr/bin。

### Specific Options
以下程序或至程序的符号链接必须在/bin下，如果有安装相应的子系统:

|Command|Description|
|:-:|:-:|
|csh|The C shell(optional)|
|ed|The 'ed' editor(optional)|
|tar|The tar archiving utility(optional)|
|cpio|The cpio archiving utility(optional)|
|gzip|The GNU compression utility(optional)|
|gunzip|The GNU uncompression utility(optional)|
|zcat|The GNU uncompression utility(optional)|
|netstat|The network statistics utility(optional)|
|ping|The ICMP network test utility(optional)|

如果gunzip和zcat存在，则他们必须是gzip的硬链接或符号链接。
/bin/csh可以是/bin/tcsh或/usr/bin/tchs的符号链接。

## /boot
Static files of the boot loader

### Specific Options
操作系统的kernel必须置于/或/boot下。

## /dev
Device files

### Specific Options
如果/dev下的设备需要手动创建，/dev下就必须包含一个MAKEDEV命令和MAKEDEV.local
文件。

## /etc
Host-specific system configuration

### Requirements
/etc下不会包含任何binaries。
以下目录或至目录的符号链接需在/etc下:

|Directory|Description|
|:-:|:-:|
|opt|Configuration for /opt|
|X11|Configuration for the X Window system(optional)|
|sgmlConfiguration for SGML(optional)|
|xml|Configuration for XML(optional)|

### Specific Options
The following directories, or symbolic links to directories must be in /etc, if the corresponding subsystem is installed:

|Directory|Description|
|:-:|:-:|
|opt|Configuration for /opt|

The following files, or symbolic links to files, must be in /etc if the corresponding subsystem is installed:

|File|Description|
|:-:|:-:|
|csh.login|Systemwide initialization file for C shell logins(optional)|
|exports|NFS filesystem access control list(optional)|
|fstab|Static information about filesystems(optional)|
|ftpusers|FTP daemon user access control list(optional)|
|gateways|File which lists gateways for routed(optional)|
|gettydefs|Speed and terminal settings used by getty(optional)|
|group|User group file(optional)|
|host.conf|Resolver configuration file(optional)|
|hosts|Static information about host names(optional)|
|hosts.allow|Host access file for TCP wrappers(optional)|
|hosts.deny|Host access file for TCP wrapers(optional)|
|hosts.equiv|List of trusted hosts for rlogin, rsh, rcp(optional)|
|hosts.lpd|List of trusted hosts for lpd(optional)|
|inetd.conf|Configuration file for inetd(optional)|
|inittab|Configuration file for init(optional)|
|issue|Pre-login message and identification file(optional)|
|ld.so.conf|List of extra directories to search for shared libraries(optional)|
|motd|Post-login message of the day file(optional)|
|mtab|Dynamic information about filesystems(optional)|
|mtools.conf|Configuration file for mtools(optional)|
|networks|Static information about network names(optional)|
|passwd|The password file(optional)|
|printcap|The lpd printer capability database(optional)|
|profile|Systemwide initialization file for sh shell logins(optional)|
|protocols|IP protocol listing(optional)|
|resolv.conf|Resolver configuration file(optional)|
|rpc|RPC protocol listing(optional)|
|securetty|TTY access control for root login(optional)|
|services|Port names for network services(optional)|
|shells|Pathnames of valid login shells(optional)|
|syslog.conf|Configuration file for syslogd(optional)|

mtab不是不可变的文件却放置在/etc下，这个是由于历史原因造成的。

### /etc/opt
Configuration files for /opt
Host-specific configuration files for add-on application software packages must be installed within the directory /etc/opt/<subdir>, where <subdir> is the name of the subtree in /opt where the static data from that package is stored.

### /etc/X11
Configuration for the X Window System(optional)
/etc/X11 is the location for all X11 host-specific configuration. This directory is neccessary to allow local control if /usr is mounted read only.

#### Specific Options
The following files, or symbolic links to files, must be in /etc/X11 if the corresponding subsystem is installed:

|File|Description|
|:-:|:-:|
|Xconfig|The configuration file for early versions of XFree86(optional)|
|XF86Config|The configuration file for XFree86 versions 3 and 4(optional)|
|Xmodmap|Global X11 keyboard modification file(optional)|

### /etc/sgml
Configuration files for SGML(optional)

### /etc/xml
Configuration files for XML(optional)

## /home
User home directories(optional)
/home is a fairly standard concept, but it is clearly a site-specific filesystem. The setup will differ from host to host. Therefore, no program should rely on this location.

### Requirements
User specific configuration files for applications are stored in the user's home directory in a file that starts with the '.' character (a "dot file"). If an application needs to create more than one dot file then they should be placed in a subdirectory with a name starting with a '.' character, (a "dot directory"). In this case the configuration files should not start with the '.' character.

## /lib
Essential shared libraries and kernel modules
The /lib directory contains those shared library images needed to boot the system and run the commands in the root filesystem, ie. by binaries in /bin and /sbin.

### Requirements
At least one of each of the following filename patterns are required(they may be files, or symbolic links):

|File|Description|
|:-:|:-:|
|libc.so.\*|The dynamically-linked C library(optional)|
|ld\*|The execution time linker/loader(optional)|

If a C preprocessor is installed, /lib/cpp must be a reference to it, for historical reasons.

### Specific Options
The following directories, or symbolic links to directories, must be in /lib, if the corresponding subsystem is installed:

|Directory|Description|
|:-:|:-:|
|modules|Loadable kernel modules(optional)|

## /lib\<qual\>
Alternate format essential shared libraries(optional)
There may be one or more variants of the /lib directory on systems which support more than one binary format requiring separate libraries.

### Requirements
If one or more of these directories exist, the requirements for their contents are the same as the normal /lib directory, except that /lib\<qual\>/cpp is not required.

## /media
Mount point for removeable media
This directory contains subdirectories which are used as mount points for removeable media such as floppy disks, cdroms and zip disks.

### Specific Options
The following directories, or symbolic links to directories, must be in /media, if the corresponding subsystem is installed:

|Directory|Description|
|:-:|:-:|
|floppy|Floppy drive(optional)|
|cdrom|CD-ROM drive(optional)|
|cdrecorder|CD writer(optional)|
|zip|Zip drive(optional)|

## /mnt
Mount point for a temporarily mounted filesystem
This directory is provided so that the system administrator may temporarily mount a filesystem as needed. The content of this directory is a local issue and should not affect the manner in which any program is run.
This directory must not be used by installation programs: a suitable temporary directory not in use by the system must be used instead.

## /opt
Add-on application software packages
/opt is reserved for the installation of add-on application software packages.
A package to be installed in /opt must locate its static files in a separate /opt/<package> or /opt/<provider> directory tree, where <package> is a name that describes the software package and <provider> is the provider's LANANA(LANANA Linux Device List) registered name.

### Requirements

|Directory|Description|
|:-:|:-:|
|<package>|Static package objects|
|<provider>|LANANA registered provider name|

The directories /opt/bin, /opt/doc, /opt/include, /opt/info, /opt/lib, and /opt/man are reserved for loacl system administrator use.

## /root
Home directory for the root user(optional)

## /sbin
System binaries
Utilities used for system administration (and other root-only commands) are stored in /sbin, /usr/sbin, and /usr/local/sbin. /sbin contains binaries essential for booting, restoring, recovering, and/or repairing the system in addition to the binaries in /bin. Programs executed after /usr is known to be mounted (when there are no problems) are generally placed into /usr/sbin. Locally-installed system administration programs should be placed into /usr/local/sbin.

### Requirements

|Command|Description|
|:-:|:-:|
|shutdown|Command to bring the system down.|

### Specific Options
The following files, or symbolic links to files, must be in /sbin if the corresponding subsystem is installed:

|Command|Description|
|:-:|:-:|
|fastboot|Reboot the system without checking the disks(optional)|
|fasthalt|Stop the system without checking the disks(optional)|
|fdisk|Partition table manipulator(optional)|
|fsck|File system check and repair utility(optional)|
|fsck.\*|File system check and repair utility for a specific filesystem(optional)|
|getty|The getty program(optional)|
|halt|Command to stop the system(optional)|
|ifconfig|Configure a network interface(optional)|
|init|Initial process(optional)|
|mkfs|Command to build a filesystem(optional)|
|mkfs.\*|Command to build a specific filesystem(optional)|
|mkswap|Command to set up a swap area(optional)|
|reboot|Command to reboot the system(optional)|
|route|IP routing table utility(optional)|
|swapon|Enable paging and swapping(optional)|
|swapoff|Disable paging and swapping(optional)|
|update|Daemon to periodically flush filesystem buffers(optional)|

## /srv
Data for services provided by this system
/srv contains site-specific data which is served by this system.

## /tmp
Temporary files
The /tmp directory must be made available for programs that require temporary files.

## The /usr Hierarchy
/usr is the second major section of the filesystem. /usr is shareable, read-only data. That means that /usr should be shareable between various FHS-compliant hosts and must not be written to. Any information that is host-specific or varies with time is stored elsewhere.
Large software packages must not use a direct subdirectory under the /usr hierarchy.

### Requirements
The following directories, or symbolic links to directories, are required in /usr.

|Directory|Description|
|:-:|:-:|
|bin|Most user commands|
|include|Header files included by C programs|
|lib|Libraries|
|local|Local hierarchy(empty after main installation|
|sbin|Non-vital system binaries|
|share|Architecture-independent data|

### Specific Options

|Directory|Description|
|:-:|:-:|
|X11R6|XWindow System, version 11 release 6(optional)|
|games|Games and educational binaries(optional)|
|lib\<qual\>|Alternate Format Libraries(optional)|
|src|Source code(optional)|

### /usrX11R6
X Window System, Version 11 Release 6(optional)
This hierarchy is reserved for the X Window System, version 11 release 6, and related files.

### /usr/bin
Most user commands
This is the primary directory of executable commands on the system.

#### Specific Options
The following directories, or symbolic links to directories, must be in /usr/bin, if the corresponding subsystem is installed:

|Directory|Description|
|:-:|:-:|
|mh|Commands for the MH mail handling system(optional)|

/usr/bin/X11 must be a symlink to /usr/X11R6/bin if the latter exists.

The following files, or symbolic links to files, must be in /usr/bin, if the corresponding subsystem is installed:

|Command|Description|
|:-:|:-:|
|perl|The Practical Extraction and Report Language(optional)|
|python|The Python interpreted language(optional)|
|tclsh|Simple shell containing Tcl interpreter(optional)|
|wish|Simple Tcl/Tk windowing shell(optional)|
|expect|Program for interactive dialog(optional)|

### /usr/include
Directory for standard include files
This is where all of the system's general-use include files for the C programming language should be placed.

#### Specific Options
The following directories, or symbolic links to directories, must be in /usr/include, if the corresponding subsystem is installed:

|Directory|Description|
|:-:|:-:|
|bsd|BSD compatibility include files(optional)|

The symbolic link /usr/include/X11 must link to /usr/X11R6/include/X11 if the later exists.

### /usr/lib
Libraries for programming and packages
/usr/lib includes object files, libraries, and internal binaries that are not intended to be executed directly by users or shell scripts.
Applications may use a single subdirectory under /usr/lib. If an application uses a subdirectory, all architecture-dependent data exclusively used by the application must be placed within that subdirectory.

#### Specific Options
For historical reasons, /usr/lib/sendmail must be a symbolic link to /usr/sbin/sendmail if the latter exists.
If /lib/X11 exists, /usr/lib/X11 must be a symbolic link to /lib/X11, or to whatever /lib/X11 is a symbolic link to.

### /usr/lib\<qual\>
Alternate format libraries(optional)
/usr/lib\<qual\> performs the same role as /usr/lib for an alternate binary format, except that the symbolic links /usr/lib\<qual\>/sendmail and /usr/lib\<qual\>/X11 are not required.

### /usr/local
Local hierarchy
The /usr/local hierarchy is for use by the system administrator when installing software locally. It needs to be safe from being overwritten when the system software is updated. It may be used for programs and data that are shareable amongst a group of hosts, but not found in /usr.
Locally installed software must be placed within /usr/local rather than /usr unless it is being installed to replace or upgrade software in /usr/

#### Requirements
The following directories, or symbolic links to directories, must be in /usr/local

|Directory|Description|
|:-:|:-:|
|bin|Local binaries|
|etc|Host-specific system configuration for local binaries|
|games|Local game binaries|
|include|Local C header files|
|lib|Local libraries|
|man|Local online manuals|
|sbin|Local system binaries|
|share|Local architecture-independent hierarchy|
|src|Local source code|

No other directories, except those listed below, may be in /usr/local after first installing a FHS-compliant system.

#### Specific Options
If directories /lib\<qual\> or /usr/lib\<qual\> exist, the equivalent directories must also exist in /usr/local.
/usr/local/etc may be a symbolic link to /etc/local.

#### /usr/local/share
The requirements for the contents of this directory are the same as /usr/share. The only additional constraint is that /usr/local/share/man and /usr/local/man directories must be synonomous(usually this means that one of them must be a symbolic link).

### /usr/sbin
Non-essential standard system binaries
This directory contains any non-essential binaries used exclusively by the system administrator. System administration programs that are required for system repair, system recovery, mounting /usr, or other essential functions must be placed in /sbin instead.

### /usr/share
Architecture-independent data
The /usr/share hierarchy is for all read-only architecture independent data files.

#### Requirements
The following directories, or symbolic links to directories, must be in /usr/share

|Directory|Description|
|:-:|:-:|
|man|Online manuals|
|misc|Miscellaneous architecture-independent data|

#### Specific Options
The following directories, or symbolic links to directories, must be in /usr/share, if the corresponding subsystem is installed:

|Directory|Description|
|:-:|:-:|
|dict|Word lists(optional)|
|doc|Miscellaneous documentation(optional)|
|games|Static data files for /usr/games(optional)|
|info|GNU Info system s primary directory(optional)|
|locale|Locale information(optional)|
|nls|Message catalogs for Native language support(optional)|
|sgml|SGML data(optional)|
|terminfo|Directories for terminfo database(optional)|
|tmac|troff macros not distributed with groff(optional)|
|xml|XML data(optional)|
|zoneinfo|Timezone information and configuration(optional)|

#### /usr/share/dict
Word lists(optional)

#### /usr/share/man
Manual pages

##### Specific Options
The following directories, or symbolic links to directories, must be in /usr/share/\<mandir\>/\<locale\>,unless they are empty:

|Directory|Description|
|:-:|:-:|
|man1|User programs(optional)|
|man2|System calls(optional)|
|man3|Library calls(optional)|
|man4|Special files(optional)|
|man5|File formats(optional)|
|man6|Games(optional)|
|man7|Miscellaneous(optional)|
|man8|System administration(optional)|

#### /usr/share/misc
Miscellaneous architecture-independent data

##### Specific Options
The following files, or symbolic links to files, must be in /usr/share/misc, if the corresponding subsystem is installed:

|File|Description|
|:-:|:-:|
|ascii|ASCII character set table(optional)|
|magic|Default list of magic numbers for the file command(optional)|
|termcap|Terminal capability database(optional)|
|termcap.db|Terminal capability database(optional)|

#### /usr/share/sgml
SGML data(optional

##### Specific Options
The following directories, or symbolic links to directories, must be in /usr/share/sgml, if the corresponding subsystem is installed:

|Directory|Description|
|:-:|:-:|
|docbook|docbook DTD(optional)|
|tei|tei DTD(optional)|
|html|html DTD(optional)|
|mathml|mathml DTD(optional)|

#### /usr/share/xml
XML data(optional)

The following directories, or symbolic links to directories, must be in /usr/share/xml, if the corresponding subsystem is installed:

|Directory|Description|
|:-:|:-:|
|docbook|docbook XML DTD(optional)|
|xhtml|XHTML DTD(optional)|
|mathml|MathML DTD(optional)|

### /usr/src
Source code(optional)

## The /var hierarchy
/var contains variable data files. This includes spool directories and files, administrative and logging data, and transient and temporary files.

### Requirements
The following directories, or symbolic links to directories, are required in /var.

|Directory|Description|
|:-:|:-:|
|cache|Application cache data|
|lib|Variable state information|
|local|Variable data for /usr/local|
|lock|Lock files|
|log|Log files and directories|
|opt|Variable data for /opt|
|run|Data relevant to running processes|
|spool|Application spool data|
|tmp|Temporary files preserved between system reboots|

Several directories are 'reserved' in the sense that they must not be used arbitrarily by some new application, since they would conflict with historical and/or local practice. They are:
    /var/backups
    /var/cron
    /var/msgs
    /var/preserve

### Specific Options
The following directories, or symbolic links to directories, must be in /var, if the corresponding subsystem is installed:

|Directory|Description|
|:-:|:-:|
|account|Process accounting logs(options)|
|crash|System crash dumps(optional)|
|games|Variable game data(optional)|
|mail|User mailbox files(optional)|
|yp|Network Information Service (NIS) database files(optional)|

### /var/account
Process accounting logs(optional)

### /var/cache
Application cache data

#### Specific Options

|Directory|Description|
|:-:|:-:|
|fonts|Locally-generated fonts(optional)|
|man|Locally-formatted manual pages(optional)|
|www|WWW proxy or cache data(optional)|
|\<package\>|Package specific cache data(optional)|

#### /var/cache/fonts
Locally-generated fonts(optional)

#### /var/cache/man
Locally-formatted manual pages(optional)

### /var/crash
System crash dumps(optional)

### /var/games
Variable game data(optional)

### /var/lib
Variable state information

#### Requirements
The following directories, or symbolic links to directories, are required in /var/lib:

|Directory|Description|
|:-:|:-:|
|misc|Miscellaneous state data|

#### Specific Options
The following directories, or symbolic links to directories, must be in /var/lib, if the corresponding subsystem is installed:

|Directory|Description|
|:-:|:-:|
|\<editor\>|Editor backup files and state(optional)|
|\<pkgtool\>|Packaging support files(optional)|
|\<package\>|State data for packages and subsystems(optional)|
|**hwclock**|State directory for hwclock(optional)|
|**xdm**|X display manager variable data(optional)|

#### /var/lib/\<editor\>
Editor backup files and state(optional)

#### /var/lib/hwclock
State directory for hwclock(optional)

#### /var/lib/misc
Miscellaneous variable data

### /var/lock
Lock files

### var/log
Log files and directories

#### Specific Options
The following files, or symbolic links to files, must be in /var/log, if the corresponding subsystem is installed:

|File|Description|
|:-:|:-:|
|lastlog|record of last login of each user|
|messages|system messages from syslogd|
|wtmp|record of all logins and logouts|

### /var/mail
User mailbox files(optional)

### /var/opt
Variable data for /opt

### /var/run
Run-time variable data

### /var/spool
Application spool data

#### Specific Options
The following directories, or symbolic links to directories, must be in /var/spool, if the corresponding subsystem is installed:

|Deirctory|Description|
|lpd|Printer spool directory(optional)|
|mqueue|Outgoing mail queue(optional)|
|news|News spool directory(optional)|
|rwho|Rwhod files(optional)|
|uucp|Spool directory for UUCP(optional)|

#### /var/spool/lpd
Line-printer daemon print queues(optional)

#### /var/spool/rwho
Rwhod files(optional)

### /var/tmp
Temporary files preserved between system reboots

### /var/yp
Network Information Service (NIS) database files(optional)

