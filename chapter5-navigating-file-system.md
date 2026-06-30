# Lab 5: Navigating the Filesystem
## 5.1 Introduction
This is Lab 5: Navigating the Filesystem. By performing this lab, students will learn how to navigate and manage files and directories.
In this lab, you will perform the following tasks:
*	Navigate home and system directories
*	List files and directories
## 5.2 Files and Directories
In this task you will explore the concepts of files and directories.
On a Linux OS, data is stored in files and files are stored in directories. You may be used to the term folders to describe directories.
Directories are actually files, too; the data that they hold are the names of the files that have been entered into them, along with the inode number (a unique identifier number assigned to each file) for where the data for that file exists on the disk.
As a Linux user, you will want to know how to manipulate these files and directories, including how to list files in a directory, copy, delete and move files.
Warning
File and directory names in Linux are case-sensitive. This means that a file named ```ABC``` is not the same as a file named ```abc```.
### 5.2.1 Step 1
Type the following command to print the working directory:
```
pwd
```
```
sysadmin@localhost:~$ pwd                                                       
/home/sysadmin                                                                  
sysadmin@localhost:~$
```
The working directory is the directory that your terminal window is currently "in". This is also called the current directory. This will be important for when you are running subsequent commands, as they will behave differently based on the directory you are currently in.

The output of the ```pwd``` command (```/home/sysadmin``` in the example above) is called the path. The first slash represents the root directory, the top level of the directory structure.
In the output above, ```home``` is a directory under the root directory and ```sysadmin``` is a directory under the home directory.
When you first open a terminal window, you will be placed in your home directory. This is a directory where you have full access and other users normally have no access by default. To see the path to your home directory, you can execute the following command to view the value of the ```HOME``` variable:
```
echo $HOME
```
```
sysadmin@localhost:~$ echo $HOME                                                
/home/sysadmin                                                                  
sysadmin@localhost:~$
```
### 5.2.2 Step 2
You can use the ```cd``` command with a path to a directory to change your current directory. Type the following command to make the root directory your current working directory and verify with the ```pwd``` command:
```
cd /
pwd
```
```
sysadmin@localhost:~$ cd /                                                    
sysadmin@localhost:/$ pwd                                                     
/                                                                             
sysadmin@localhost:/$
```
### 5.2.3 Step 3
To change back to your home directory, the ```cd``` command can be executed without a path. Change back to your home directory and verify by typing the following commands:
```
cd
pwd
```
```
sysadmin@localhost:/$ cd                                                        
sysadmin@localhost:~$ pwd                                                       
/home/sysadmin                                                                  
sysadmin@localhost:~$
```
Notice the change in the ```prompt```. The tilde ~ character represents your home directory. This part of the prompt will tell you what directory you are currently in.
### 5.2.4 Step 4
The ```cd``` command may be entered with a path to a directory specified as an argument. Execute the ```cd``` command with the /home directory as an argument by typing the following:
```
cd /home
pwd
```
```
sysadmin@localhost:~$ cd /home                                                
sysadmin@localhost:/home$ pwd                                                 
/home                                                                         
sysadmin@localhost:/home$
```
### 5.2.5 Step 5
Change back to your home directory, using the cd command with the tilde ~ as an argument:
```
cd ~
pwd
```
```
sysadmin@localhost:/home$ cd ~                                                
sysadmin@localhost:~$ pwd                                                     
/home/sysadmin                                                                
sysadmin@localhost:~$
```
When the path that is provided as an argument to the ```cd``` command starts with a tilde ```~ character```, the terminal will expand the character to the home directory of a user with an account on the system.

If either no other characters or a forward slash follows the tilde, then it will expand to the home directory of the user currently active in the shell.

If a user name immediately follows the tilde character, then the shell will expand the tilde and user name to the home directory of that user name. For example, ~bob would be expanded to ```/home/bob```.

Paths that start with a tilde are considered absolute paths because after the shell expands the tilde path, an absolute path is formed.
### 5.2.6 Step 6
Use the echo command below to display some other examples of using the tilde as part of the path:
```
echo  ~ ~sysadmin ~root ~mail ~nobody
```
```
sysadmin@localhost:~$ echo ~ ~sysadmin ~root ~mail ~nobody                     
/home/sysadmin /home/sysadmin /root /var/mail /nonexistent                    
sysadmin@localhost:~$
```
### 5.2.7 Step 7
Attempt to change to the home directory of the root user by typing the following command:
```
cd ~root
```
```
sysadmin@localhost:~$ cd ~root                                                
-bash: cd: /root: Permission denied                                           
sysadmin@localhost:~$
```
Notice the error message; it indicates that the shell attempted to execute ```cd``` with ```/root``` as an argument but it failed due to permission being denied. You will learn more about file and directory permissions in a later lab.
### 5.2.8 Step 8
Using an absolute path, change to the ```/usr/bin``` directory and display the working directory by using the following commands:
```
cd /usr/bin
pwd
```
```
sysadmin@localhost:~$ cd /usr/bin                                             
sysadmin@localhost:/usr/bin$ pwd                                              
/usr/bin                                                                      
sysadmin@localhost:/usr/bin$
```
### 5.2.9 Step 9
Use an absolute path to change to the ```/usr``` directory and display the working directory by issuing the following commands:
```
cd /usr
pwd
```
```
sysadmin@localhost:/usr/bin$ cd /usr                                          
sysadmin@localhost:/usr$ pwd                                                  
/usr                                                                          
sysadmin@localhost:/usr$
```
### 5.2.10 Step 10
Use an absolute path to change to the ```/usr/share/doc``` directory and display the working directory by issuing the following commands:
```
cd /usr/share/doc
pwd
```
```
sysadmin@localhost:/usr$ cd /usr/share/doc                                    
sysadmin@localhost:/usr/share/doc$ pwd                                        
/usr/share/doc                                                                
sysadmin@localhost:/usr/share/doc$
```
### Absolute vs. Relative pathnames
Suppose you are in the ```/usr/share/doc``` directory and you want to go to the ```/usr/share/doc/bash``` directory. Typing the command ```cd /usr/share/doc/bash``` results in a fair amount of typing. In cases like this, you want to use relative pathnames.
With relative pathnames you provide "directions" of where you want to go from the current directory. The following examples will illustrate using relative pathnames.
### 5.2.11 Step 11
Using a relative path, change to the /usr/share/doc/bash directory and display the working directory by issuing the following commands:
```
cd bash
pwd
```
```
sysadmin@localhost:/usr/share/doc$ cd bash                                    
sysadmin@localhost:/usr/share/doc/bash$ pwd                                   
/usr/share/doc/bash                                                           
sysadmin@localhost:/usr/share/doc/bash$
```
Note
If there wasn't a bash directory under the current directory, the previous command would fail.
### 5.2.12 Step 12
Use a relative path to change to the directory above the current directory:
```
cd ..
pwd
```
```
sysadmin@localhost:/usr/share/doc/bash$ cd ..                                 
sysadmin@localhost:/usr/share/doc$ pwd                                        
/usr/share/doc                                                                
sysadmin@localhost:/usr/share/doc$
```
The .. represents one level above your current directory location.
### 5.2.13 Step 13
Use a relative path to change up one level from the current directory and then down into the dict directory:
```
cd ../dict
pwd
```
```
sysadmin@localhost:/usr/share/doc$ cd ../dict                                 
sysadmin@localhost:/usr/share/dict$ pwd                                       
/usr/share/dict                                                               
sysadmin@localhost:/usr/share/dict$
```
## 5.3 Listing Files and Directories
In this task, you will explore how to list files and directories.
### 5.3.1 Step 1
To list the contents of the current directory, use the ls command:
```
cd
ls
```
Your output should be similar to the following:
```
sysadmin@localhost:/usr/share/dict$ cd                                        
sysadmin@localhost:~$ ls                                                      
Desktop  Documents  Downloads  Music  Pictures  Public  Templates  Videos     
sysadmin@localhost:~$
```
In the output of the previous ```ls``` command, the file names were placed in a light blue color. This is a feature that many distributions of Linux automatically provide through a feature called an alias (more on this feature in a later lab).
The color indicates what type the item is. The following table describes some of the more common colors:
Color	Type of File
Black or White	Regular file
Blue	Directory file
Cyan	Symbolic link file (a file that points to another file)
Green	Executable file (a program)
### 5.3.2 Step 2
Not all files are displayed by default. There are files, called hidden files, that are not displayed by default. To display all files, including hidden files, use the -a option to the ls command:
```
ls -a
```
```
sysadmin@localhost:~$ ls -a                                                   
.             .bashrc   .selected_editor  Downloads  Public                   
..            .cache    Desktop           Music      Templates                
.bash_logout  .profile  Documents         Pictures   Videos                   
sysadmin@localhost:~$
```
The names of hidden files begin with a period (a dot character). Typically these files and often directories are hidden because they are not files you normally want to see.
For example, the ```.bashrc``` file shown in the example above contains configuration information for the bash shell. This is a file that you normally don't need to view on a regular basis.
Two important "dot files" exist in every directory: . (which represents the current directory) and .. (which represents the directory above the current directory).
### 5.3.3 Step 3
By itself, the ```ls``` command just provided the names of the files and directories within the specified (or current) directory. Execute the following command to see how the -l option provides more information about a file:
```
ls -l /etc/hosts
```
Your output should be similar to the following:
```
sysadmin@localhost:~$ ls -l /etc/hosts                                    
-rw-r--r-- 1 root root 150 Jan 22 15:18 /etc/hosts                        
sysadmin@localhost:~$
```
So, what does all of this extra output mean? The following table provides a brief breakdown of what each part of the output of ```ls -l``` means:
* -	The first character, a - in the previous example, indicates what type of "file" this is. A -character is for a plain file while a d character would be for a directory.
* rw-r--r--	This represents the permissions of the file. Permissions are discussed in a later lab.
* 1	This represents something called a hard link count (discussed later).
* root	The user owner of the file.
* root	The group owner of the file.
* 150	The size of the file in bytes
* Jan 22 15:18	The date/time when the file was last modified.

### 5.3.4 Step 4
Sometimes you want to see not only the contents of a directory, but also the contents of the subdirectories. You can use the -```R``` option to accomplish this:
```
ls -R /etc/udev
```
```
sysadmin@localhost:~$ ls -R /etc/udev                                         
/etc/udev:                                                                      
hwdb.d  rules.d  udev.conf                                                      
                                                                                
/etc/udev/hwdb.d:                                                               
                                                                                
/etc/udev/rules.d:                                                              
70-persistent-cd.rules  README                                                 
sysadmin@localhost:~$
```
The ```-R``` option stands for "recursive". All of the files in the ```/etc/udev``` directory will be displayed as well as all of the files in each subdirectory, in this case the rules.d subdirectory.
Be careful of the ```-R``` option. Some directories are very, very large!
### 5.3.5 Step 5
You can use file ```globbing``` (wildcards) to limit which files or directories you see. For example, the ```*``` character can match "zero or more of any characters" in a filename. Execute the following command to display only the files that begin with the letter s in the /etc directory:
```
ls -d /etc/s*
```
Your output should be similar to the following:
```
sysadmin@localhost:~$ ls -d /etc/s*                                           
/etc/securetty  /etc/sgml     /etc/shells  /etc/ssl        /etc/sysctl.conf   
/etc/security   /etc/shadow   /etc/skel    /etc/sudoers    /etc/sysctl.d      
/etc/services   /etc/shadow-  /etc/ssh     /etc/sudoers.d  /etc/systemd       
sysadmin@localhost:~$
```
Note that the ```-d``` option prevents files from subdirectories from being displayed. It should always be used with the ls command when you are using file globbing.
### 5.3.6 Step 6
The ? character can be used to match exactly 1 character in a file name. Execute the following command to display all of the files in the /etc directory that are exactly four characters long:
```
ls -d /etc/????
```
Your output should be similar to the following:
```
sysadmin@localhost:~$ ls -d /etc/????                                         
/etc/bind  /etc/init  /etc/motd  /etc/perl  /etc/skel                         
/etc/dpkg  /etc/ldap  /etc/mtab  /etc/sgml  /etc/udev                         
sysadmin@localhost:~$
```
### 5.3.7 Step 7
By using square brackets ```[ ]``` you can specify a single character to match from a set of characters. Execute the following command to display all of the files in the ```/etc``` directory that begin with the letters a, b, c or d:
```
ls –d /etc/[abcd]*
```
Your output should be similar to the following:
```
sysadmin@localhost:~$ ls -d /etc/[abcd]*                                      
/etc/adduser.conf            /etc/blkid.conf            /etc/cron.weekly      
/etc/adjtime                 /etc/blkid.tab             /etc/crontab          
/etc/alternatives            /etc/ca-certificates       /etc/dbus-1           
/etc/apparmor.d              /etc/ca-certificates.conf  /etc/debconf.conf     
/etc/apt                     /etc/calendar              /etc/debian_version   
/etc/bash.bashrc             /etc/cron.d                /etc/default          
/etc/bash_completion.d       /etc/cron.daily            /etc/deluser.conf     
/etc/bind                    /etc/cron.hourly           /etc/depmod.d         
/etc/bindresvport.blacklist  /etc/cron.monthly          /etc/dpkg             
sysadmin@localhost
````
