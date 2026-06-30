# Getting Help
## 4.1 Introduction
This is Lab 6: Getting Help. By performing this lab, students will learn how to get help on commands and find files.
In this lab, you will perform the following tasks:
*	Use several help systems to get help for commands.
*	Learn how to locate commands.
## 4.2 Getting Help
In this task, you will explore the how to get help. This will be a very useful thing to know how to do when you find yourself stuck or when you can't remember how a command works.
In addition to Internet searches, the Linux Operating System provides a variety of techniques to learn more about a given command or feature. Knowing these different techniques will allow you to more easily and quickly find the answer you need.
### 4.2.1 Step 1
Execute commands in the bash shell by typing the command and then pressing the Enter key. For example, type the following command to display today's date:
```
date
``
The output should be similar to the following:
```
sysadmin@localhost:~$ date                                                
Mon Feb 12 20:57:34 UTC 2024
```
### 4.2.2 Step 2
To learn more about commands, access the manual page for the command with the ```man``` command. For example, execute the following command to learn more about the ```date``` command:
```
man date
```
```
sysadmin@localhost:~$ man date
```
Your output should be similar to the following:
```
DATE(1)                          User Commands                              DATE(1)  
 
NAME                           
       date - print or set the system date and time                             
                                                                              
SYNOPSIS                                                                      
       date [OPTION]... [+FORMAT]                                             
       date [-u|--utc|--universal] [MMDDhhmm[[CC]YY][.ss]]                      
                                                                              
DESCRIPTION                                                                
      Display the current time in the given FORMAT, or set the system date.    
                                                                                
       Mandatory  arguments  to  long  options are mandatory for short options  
       too.  
 
       -d, --date=STRING                                                        
              display time described by STRING, not 'now'                       
                                                                                
       --debug                                                                  
              annotate the parsed date, and warn about questionable  usage  to  
              stderr                                                            
                                                                                
       -f, --file=DATEFILE 
Manual page date(1) line 1 (press h for help or q to quit)
```
Note
Documents that are displayed with the man command are called "Man Pages".
If the man command can find the manual page for the argument provided, then that manual page will be displayed using a command called less. The following table describes useful keys that can be used with the less command to control the output of the display:
```
Key	Purpose
H or h	Display the help
Q or q	Quit the help or manual page
Spacebar or f or PageDown	Move a screen forward
b or PageUp	Move a screen backward
Enter or down arrow	Move down one line
Up arrow	Move up one line
/ followed by text to search	Start searching forward
? followed by text to search	Start searching backward
n	Move to next text that matches search
N	Move to previous matching text
```
### 4.2.3 Step 3
Type the letter h to see a list of movement commands. After reading the movement commands, type the letter q to get back to the document.
```
                  SUMMARY OF LESS COMMANDS                                     
                                               
    Commands marked with * may be preceded by a number, N.     
    Notes in parentheses indicate the behavior if N is given.        
    A key preceded by a caret indicates the Ctrl key; thus ^K is ctrl-K.      
                                                                  
  h  H                 Display this help.                             
  q  :q  Q  :Q  ZZ     Exit.                                          
 -----------------------------------------------------------------------
                                                                    
                         MOVING                                         
 
e  ^E  j  ^N  CR  *  Forward  one line   (or N lines).             
y  ^Y  k  ^K  ^P  *  Backward one line   (or N lines).              
f  ^F  ^V  SPACE  *  Forward  one window (or N lines).             
b  ^B  ESC-v      *  Backward one window (or N lines).
z                 *  Forward  one window (and set window to N).  
w                 *  Backward one window (and set window to N).      
ESC-SPACE         *  Forward  one window, but don't stop at end-of-file.
d  ^D             *  Forward  one half-window (and set half-window to N)
u  ^U             *  Backward one half-window (and set half-window to N)
ESC-)  RightArrow *  Left  one half screen width (or N positions).     
HELP -- Press RETURN for more, or q when done
```
Note that the man pages might be a bit of a mystery to you now, but as you learn more about Linux, you will find they are a very valuable resource.
### 4.2.4 Step 4
Searches are not case sensitive and do not "wrap" around from the bottom to top, or vice versa. Start a forward search for the word "file" by typing:
```
/file
Note that what you are typing will appear at the bottom left portion of the screen.
       -r, --reference=FILE                                                   
              display the last modification time of FILE                       
 
       -R, --rfc-2822                                                         
              output  date  and time in RFC 2822 format.  Example: Mon, 07 Aug
/file
Press Enter to search the document for the search string (file).
```
### 4.2.5 Step 5
Notice that the text matching the search is highlighted. You can move forward to the next match by pressing n. Also try moving backwards through the matches by pressing N:
```
-f, --file=DATEFILE                                                      
              like --date once for each line of DATEFILE                        
                                                                                
       -r, --reference=FILE                                                     
              display the last modification time of FILE                        
                                                                                
      -R, --rfc-2822                                                           
              output  date  and time in RFC 2822 format.  Example: Mon, 07 Aug  
              2006 12:34:56 -0600                                               
                                                                                
       --rfc-3339=TIMESPEC                                                      
              output date and time in RFC 3339 format.  TIMESPEC=`date', `sec-  
              onds',  or  `ns'  for  date and time to the indicated precision.  
              Date and time  components  are  separated  by  a  single  space:  
              2006-08-07 12:34:56-06:00                                         
                                                                                
       -s, --set=STRING                                                         
              set time described by STRING                                      
                                                                                
       -u, --utc, --universal                                                  
              print or set Coordinated Universal Time                           
                                                                                
       --help display this help and exit                                        
Manual page date(1) line 18/204 24% (press h for help or q to quit)
```
### 4.2.6 Step 6
Use the movement commands previously described (such as using the spacebar to move down one screen) to read the man page for the date command. When you are finished reading, type q to exit the man page.
### 4.2.7 Step 7
In some cases you may not remember the exact name of the command. In these cases you can use the -k option to the man command and provide a keyword argument. For example, execute the following command to display a summary of all man pages that have the keyword "password" in the description:
```
man -k password
sysadmin@localhost:~$ man -k password                                         
chage (1)            - change user password expiry information                
chgpasswd (8)        - update group passwords in batch mode                   
chpasswd (8)         - update passwords in batch mode                         
cpgr (8)             - copy with locking the given file to the password or gr...
cppw (8)             - copy with locking the given file to the password or gr...
expiry (1)           - check and enforce password expiration policy           
login.defs (5)       - shadow password suite configuration                    
pam_pwhistory (8)    - PAM module to remember last passwords                  
pam_unix (8)         - Module for traditional password authentication         
passwd (1)           - change user password                                   
passwd (1ssl)        - compute password hashes                                
passwd (5)           - the password file                                      
pwck (8)             - verify integrity of password files                     
pwconv (8)           - convert to and from shadow passwords and groups        
shadow (5)           - shadowed password file                                 
shadowconfig (8)     - toggle shadow passwords on and off                     
unix_chkpwd (8)      - Helper binary that verifies the password of the curren...
unix_update (8)      - Helper binary that updates the password of a given user
vipw (8)             - edit the password, group, shadow-password or shadow-gr...
sysadmin@localhost:~$
```
The -k option to the man command will often produce a huge amount of output. We will cover a technique in a later lab to either limit this output or allow you to easily scroll through the data. For now, you can scroll using your mouse in the terminal window to move the display up and down as needed
### 4.2.8 Step 8
Note that the apropos command is another way of viewing man page summaries with a keyword. Type the following command:
```
apropos password
sysadmin@localhost:~$ apropos password                                        
chage (1)            - change user password expiry information                
chgpasswd (8)        - update group passwords in batch mode                   
chpasswd (8)         - update passwords in batch mode                         
cpgr (8)             - copy with locking the given file to the password or gr...
cppw (8)             - copy with locking the given file to the password or gr...
expiry (1)           - check and enforce password expiration policy           
login.defs (5)       - shadow password suite configuration                    
pam_pwhistory (8)    - PAM module to remember last passwords                  
pam_unix (8)         - Module for traditional password authentication         
passwd (1)           - change user password                                   
passwd (1ssl)        - compute password hashes                                
passwd (5)           - the password file                                      
pwck (8)             - verify integrity of password files                     
pwconv (8)           - convert to and from shadow passwords and groups        
shadow (5)           - shadowed password file                                 
shadowconfig (8)     - toggle shadow passwords on and off                     
unix_chkpwd (8)      - Helper binary that verifies the password of the curren...
unix_update (8)      - Helper binary that updates the password of a given user
vipw (8)             - edit the password, group, shadow-password or shadow-gr...
sysadmin@localhost:~$
```
Note
There is no difference between man -k and the apropos command.
### 4.2.9 Step 9
There are often multiple man pages with the same name. For example, the following command shows three pages for passwd. Execute the following command to view the man pages for the word passwd:
```
man -f passwd
sysadmin@localhost:~$ man -f passwd                                           
passwd (5)           - the password file                                      
passwd (1)           - change user password                                   
passwd (1ssl)        - compute password hashes                                
sysadmin@localhost:~$
```
The fact that there are different man pages for the same "name" is confusing for many beginning Linux users. Man pages are not just for Linux commands, but also for system files and other "features" of the Operating System. Additionally, there will sometimes be two commands with the same name, as in the example provided above.
The different man pages are distinguished by "sections". By default there are nine sections of man pages:
*	Executable programs or shell commands
*	System calls (functions provided by the kernel)
*	Library calls (functions within program libraries)
*	Special files (usually found in /dev)
*	File formats and conventions, e.g. /etc/passwd
*	Games
*	Miscellaneous (including macro packages and conventions), e.g. man(7)>, groff(7)
*	System administration commands (usually only for root)
*	Kernel routines
When you type a command such as man passwd, the first section is searched and, if a match is found, the man page is displayed. The man -f passwd command that you previously executed shows that there is a section 1 man page for passwd: passwd (1). As a result, that is the one that is displayed by default.
### 4.2.10 Step 10
To display a man page for a different section, provide the section number as the first argument to the man command. For example, execute the following command:
```
man 5 passwd
PASSWD(5)                File Formats and Conversions                PASSWD(5)  
                                                                              
NAME                                                                          
       passwd - the password file                                             
                                                                              
DESCRIPTION                                                                   
       /etc/passwd contains one line for each user account, with seven fields 
       delimited by colons (":"). These fields are:                           
                                                                              
       o   login name                                                         
                                                                              
       o   optional encrypted password                                        
                                                                              
       o   numerical user ID                                                  
                                                                              
       o   numerical group ID                                               
                                                                              
       o   user name or comment field                                         
                                                                              
       o   user home directory                                                
                                                                              
       o   optional user command interpreter                                  
                                                                                
 Manual page passwd(5) line 1 (press h for help or q to quit)
Type q to return to the system prompt.
```
### 4.2.11 Step 11
Instead of using man -f to display all man page sections for a name, you can also use the whatis command:
```
whatis passwd
sysadmin@localhost:~$ whatis passwd                                           
passwd (5)           - the password file                                      
passwd (1)           - change user password                                   
passwd (1ssl)        - compute password hashes                                
sysadmin@localhost:~$
```
Note
There is no difference between man -f and the whatis command.
### 4.2.12 Step 12
Almost all system features (commands, system files, etc.) have man pages. Some of these features also have a more advanced feature called info pages. For example, execute the following command:
```
info date
File: coreutils.info,  Node: date invocation,  Next: arch invocation,  Up: Syst\
em context                                                                      
                                                                              
21.1 `date': Print or set system date and time                                
==============================================                                
                                                                              
Synopses:                                                                     
                                                                              
     date [OPTION]... [+FORMAT]                                               
     date [-u|--utc|--universal] [ MMDDhhmm[[CC]YY][.ss] ]                    
                                                                              
   Invoking `date' with no FORMAT argument is equivalent to invoking it       
with a default format that depends on the `LC_TIME' locale category.          
In the default C locale, this format is `'+%a %b %e %H:%M:%S %Z %Y'',         
so the output looks like `Thu Mar  3 13:47:51 PST 2005'.                      
                                                                              
   Normally, `date' uses the time zone rules indicated by the 'TZ'            
environment variable, or the system default rules if 'TZ' is not set.         
*Note Specifying the Time Zone with 'TZ': (libc)TZ Variable.                  
                                                                              
   If given an argument that starts with a '+', 'date' prints the             
current date and time (or the date and time specified by the `--date'         
-----Info: (coreutils)date invocation, 40 lines --Top-----------------
Welcome to Info version 6.5.  Type H for help, h for tutorial.
```
Many beginning Linux users find info pages to be easier to read. They are often written more like "lessons" while man pages are written purely as documentation.
### 4.2.13 Step 13
While viewing the info page from the previous step, type Shift and the letter h to see a list of movement commands. Note that they are different from the movement commands used in man pages. After reading the movement commands, type the letter l (lowercase L) to return to viewing the document.
### 4.2.14 Step 14
Use the movement commands to read the info page for the date command. When you are done, put your cursor anywhere on the line that reads *Examples of date:: and then press the Enter key. A new document will be displayed that shows examples of date.
### 4.2.15 Step 15
Type the l key to return to the previous screen. When you are finished reading, type q to exit the info page.
### 4.2.16 Step 16
Another way of getting help is by using the --help option to a command. Most commands allow you to pass an argument of --help to view basic command usage:

```date --help```
```
sysadmin@localhost:~$ date --help                                             
Usage: date [OPTION]... [+FORMAT]                                             
  or:  date [-u|--utc|--universal] [MMDDhhmm[[CC]YY][.ss]]                    
Display the current time in the given FORMAT, or set the system date.         
                                                                              
  -d, --date=STRING         display time described by STRING, not `now'       
  -f, --file=DATEFILE       like --date once for each line of DATEFILE        
  -r, --reference=FILE      display the last modification time of FILE        
  -R, --rfc-2822            output date and time in RFC 2822 format.          
                            Example: Mon, 07 Aug 2006 12:34:56 -0600          
      --rfc-3339=TIMESPEC   output date and time in RFC 3339 format.          
                            TIMESPEC=`date', `seconds', or `ns' for           
                            date and time to the indicated precision.         
                            Date and time components are separated by         
                            a single space: 2006-08-07 12:34:56-06:00         
  -s, --set=STRING          set time described by STRING                      
  -u, --utc, --universal    print or set Coordinated Universal Time           
      --help     display this help and exit                                   
      --version  output version information and exit
```
### 4.2.17 Step 17
Some system features also have more detailed help documents located in the /usr/share/doc directory structure. Execute the following command to view the contents of this document:
```
ls /usr/share/doc
sysadmin@localhost:~$ ls /usr/share/doc                                       
adduser              libdrm2               libx11-data                        
apt                  libedit2              libxau6                            
ascii                libelf1               libxcb1                            
base-files           libffi6               libxdmcp6                          
base-passwd          libgcc1               libxext6                           
bash                 libgcrypt11           libxml2                            
bind9                libgdbm3              libxmuu1                           
bind9-host           libgeoip1             locales                            
bind9utils           libgettextpo0         login                              
bsdmainutils         libglib2.0-0          logrotate                          
bsdutils             libgnutls26           lsb-base                           
busybox-initramfs    libgomp1              makedev                            
bzip2                libgpg-error0         man-db                             
ca-certificates      libgpm2               mawk                               
coreutils            libgssapi-krb5-2      mc                                 
cpio                 libgssapi3-heimdal    mc-data                            
cron                 libhcrypto4-heimdal   mime-support                       
curl                 libheimbase1-heimdal  mlocate                            
dash                 libheimntlm0-heimdal  module-init-tools
```
Note that in almost all cases, the man pages and info pages will provide you with the information that you need. However, if you need more in-depth information (something that system administrators sometimes need), then you may find this information in the files located in the ```/usr/share/doc```
## 4.3 Finding Files
In this task, we will explore how to search for a file on the system. This is useful to know in situations when you can't find a file on the system, either one that you created or one that was created by someone else.
### 4.3.1 Step 1
An easy way to search for a file is to use the locate command. For example, you can find the location of the crontab file by executing the following command:
```locate crontab```
```
sysadmin@localhost:~$ locate crontab                                          
/etc/crontab                                                                    
/usr/bin/crontab                                                                
/usr/share/bash-completion/completions/crontab                                  
/usr/share/doc/cron/examples/crontab2english.pl                                 
/usr/share/man/man1/crontab.1.gz                                                
/usr/share/man/man5/crontab.5.gz                                              
sysadmin@localhost:~$
```
### 4.3.2 Step 2
Note that the output from the previous example includes files that have crontab as part of their name. To find files that are just named crontab, use the following command:
```locate -b "\crontab"```
```
sysadmin@localhost:~$ locate -b /etc/crontab                                                                    
/usr/bin/crontab                                                                
/usr/share/bash-completion/completions/crontab                                                             
sysadmin@localhost:~$
```
Note: The locate command makes use of a database that is traditionally updated once per day (normally in the middle of the night). This database contains a list of all files that were on the system when the database was last updated.
As a result, any files that you created today will not normally be searchable with the locate command. If you have access to the system as the root user (the system administrator account), you can manually update this file by running the updatedb command. Regular users cannot update the database file.
Another possible solution to searching for "newer" files is to make use of the find command. This command searches the live filesystem, rather than a static database. The find command isn't part of the Linux Essentials objectives for this lab, so it is only mentioned here. Execute man find if you want to explore this command on your own.
### 4.3.3 Step 3
You may just want to find where a command (or its man pages) is located. This can be accomplished with the``` whereis``` command:
```
whereis passwd
```
```
sysadmin@localhost:~$ whereis passwd 
passwd: /usr/bin/passwd /etc/passwd /usr/share/man/man1/passwd.1.gz /usr/share/m
an/man1/passwd.1ssl.gz /usr/share/man/man5/passwd.5.gz                       
sysadmin@localhost:~$
```
The ```whereis``` command does not search for just any file, only for commands and man pages.
Recall from earlier that there is more than one ```passwd``` man page on the system. This is why you see multiple file names and man pages (the files that end in ```.gz``` are man pages) when you execute the previous command.
