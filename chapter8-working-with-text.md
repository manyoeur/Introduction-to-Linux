# Working With Text
## 8.1 Introduction
This is Lab 8: Working with Text. By performing this lab, students will learn how to redirect text streams, use regular expressions and use commands for filtering text files.
In this lab, you will perform the following tasks:
*	Learn how to redirect and pipe standard input, output and error channels.
*	Use regular expressions to filter the output of commands or file content.
*	View large files or command output with programs for paging, and viewing selected portions.
## 8.2 Command Line Pipes and Redirection
Normally, when you execute a command, the output is displayed in the terminal window. This output (also called a channel) is called standard output, symbolized by the term ```stdout```. The file descriptor number for this channel is 1.
Standard ```error (stderr)``` occurs when an error appears during the execution of a command; it has a file descriptor of 2. Error messages are also sent to the terminal window by default.
In this lab, you will use characters that redirect the output from standard output (stdout) and standard error (stderr) to a file or to another command instead of the terminal screen.
Standard input, stdin, usually is provided by you to a command by typing on the keyboard; it has a file descriptor of 0. However, by redirecting standard input, files can also be used as stdin.
### 8.2.1 Step 1
Use the redirection symbol ```>``` along with the ```echo``` command to redirect the output from the normal output of stdout (to the terminal) to a file. The cat command can be used to display file contents and will be used in this example to verify redirected output to the file. Type the following:
```
echo "Hello World"
echo "Hello World" > mymessage
cat mymessage
```
Your output should be similar to the following:
```
sysadmin@localhost:~$ echo "Hello World"                                      
Hello World                                                                   
sysadmin@localhost:~$ echo "Hello World" > mymessage                          
sysadmin@localhost:~$ cat mymessage                                           
Hello World                                                                   
sysadmin@localhost:~$
```
The first command echoes the message (stdout) to the terminal.
The second command redirects the output; instead of sending the output to the terminal, it is sent to a file called mymessage.
The last command displays the contents of the mymessage file.
### 8.2.2 Step 2
When you use the ```>``` symbol to redirect ```stdout```, the contents of the file are first destroyed. Type the following commands to see a demonstration:
```
echo "Greetings" > mymessage
cat mymessage
```
Your output should be similar to the following:
```
sysadmin@localhost:~$ echo "Greetings" > mymessage                              
sysadmin@localhost:~$ cat mymessage                                         
Greetings                                                                     
sysadmin@localhost:~$
```
Notice that using one redirection symbol overwrites an existing file. This is called "clobbering" a file.
### 8.2.3 Step 3
You can avoid clobbering a file by using ```>>``` instead of ```>```. By using ```>>``` you append to a file. Execute the following commands to see a demonstration of this:
```
cat mymessage
echo "How are you?" >> mymessage
cat mymessage
```
Your output should be similar to the following:
```
sysadmin@localhost:~$ cat mymessage                                           
Greetings                                                                     
sysadmin@localhost:~$ echo "How are you?" >> mymessage                        
sysadmin@localhost:~$ cat mymessage                                           
Greetings                                                                     
How are you? 
sysadmin@localhost:~$
```
Notice that by using ```>>``` all existing data is preserved and the new data is appended at the end of the file.
### 8.2.4 Step 4
The ```find``` command is a good command to demonstrate how ```stderr``` works. This very flexible command allows searching with a host of options such as filename, size, date, type and permission.
The ```find``` command will begin the search in the directory specified and recursively search all of the subdirectories. For example, to search for files beginning in your home directory containing the name bash:
```
find ~ -name "*bash*"
```
Your output should be similar to the following:
```
sysadmin@localhost:~$ find ~ -name "*bash*"                                   
/home/sysadmin/.bash_logout                                                   
/home/sysadmin/.bashrc                                                        
sysadmin@localhost:~$
```
Remember that ```~``` is used to represent your home directory.
Now, run the following command and observe the output:
```
find /etc -name hosts
```
Your output should be similar to the following:
```
sysadmin@localhost:~$ find /etc -name hosts                                     
/etc/hosts                                                                      
find: '/etc/ssl/private': Permission denied                                             
sysadmin@localhost:~$
```
Notice the error message indicating you do not have permission to access certain files/directories. This is because as a regular user, you don't have the right to "look inside" some directories. These types of error messages are sent to ```stderr```, not ```stdout```.
The find command is beyond the scope of this course. The purpose of using the command is to demonstrate the difference between stdout and ```stderr```.
### 8.2.5 Step 5
To redirect ```stderr``` (error messages) to a file, issue the following command:
```
find /etc -name hosts 2> err.txt
cat err.txt
```
Your output should be similar to the following:
```
sysadmin@localhost:~$ find /etc -name hosts 2> err.txt                        
/etc/hosts                                                                    
sysadmin@localhost:~$ cat err.txt                                             
find: `/etc/ssl/private': Permission denied                                   
sysadmin@localhost:~$
```
Recall that the file descriptor for stderr is the number 2, so it is used along with the ```>``` symbol to redirect the stderr output to a file ```called err.txt```. Note that ```1>``` is the same as ```>```.
The previous example demonstrates why knowing redirection is important. If you want to "ignore" the errors that the ```find``` command displays, you can redirect those messages into a file and look at them later, making it easier to focus on the rest of the output of the command.
### 8.2.6 Step 6
You can also redirect stdout and stderr into two separate files.
```
find /etc -name hosts > std.out 2> std.err
cat std.err
cat std.out
```
Your output should be similar to the following:
```
sysadmin@localhost:~$ find /etc -name hosts > std.out 2> std.err              
sysadmin@localhost:~$ cat std.err                                             
find: `/etc/ssl/private': Permission denied                                   
sysadmin@localhost:~$ cat std.out                                             
/etc/hosts
```                                                              
Note that a space is permitted but not required after the ```> redirection symbol```.
### 8.2.7 Step 7
To redirect both standard output (stdout) and standard error (stderr) to one file, first redirect stdout to a file and then redirect stderr to that same file by using the notation ```2>&1```.
```
find /etc -name hosts > find.out 2>&1
cat find.out
```
Your output should be similar to the following:
```
sysadmin@localhost:~$ find /etc -name hosts > find.out 2>&1                   
sysadmin@localhost:~$ cat find.out                                              
/etc/hosts                                                                      
find: '/etc/ssl/private': Permission denied    
sysadmin@localhost:~$
```
The ```2>&1``` part of the command means "send the ```stderr (channel 2)``` to the same place where ```stdout (channel 1)``` is going".
### 8.2.8 Step 8
Standard input ```(stdin)``` can also be redirected. Normally ```stdin``` comes from the keyboard, but sometimes you want it to come from a file instead. For example, the ```tr``` command translates characters, but it only accepts data from stdin, never from a file name given as an argument. This is great when you want to do something like capitalize data that is inputted from the keyboard (Note: Press Control+d, to signal the ```tr``` command to stop processing standard input):
```
tr a-z A-Z
this is interesting
how do I stop this?
^D
```
Your output should be similar to the following:
```
sysadmin@localhost:~$ tr a-z A-Z                                              
this is interesting                                                           
THIS IS INTERESTING                                                           
how do I stop this?                                                           
HOW DO I STOP THIS?                                                           
sysadmin@localhost:~$
```
Note: ```^D symbolizes Control+d```

### 8.2.9 Step 9
The ```tr``` command accepts keyboard input ```(stdin)```, translates the characters and then redirects the output to ```stdout```. To create a file of all lower-case characters, execute the following:
```
tr A-Z a-z > myfile
Wow, I SEE NOW
This WORKS!
```
Your output should be similar to the following:
```
sysadmin@localhost:~$ tr A-Z a-z > myfile                                     
Wow, I SEE NOW                                                                
This WORKS!                                                                   
sysadmin@localhost:~$
```
Press the Enter key to make sure your cursor is on the line below "This works!", then use Control+d to stop input. To verify you created the file, execute the following command:
```
cat myfile
```
Your output should be similar to the following:
```
sysadmin@localhost:~$ cat myfile                                              
wow, i see now                                                                
this works!                                                                   
sysadmin@localhost:~$
```
### 8.2.10 Step 10
Execute the following commands to use the ```tr``` command by redirecting stdin from a file:
```
cat myfile
tr a-z A-Z < myfile
```
Your output should be similar to the following:
```
sysadmin@localhost:~$ cat myfile                                              
wow, i see now                                                                
this works!                                                                   
sysadmin@localhost:~$ tr a-z A-Z < myfile                                     
WOW, I SEE NOW                                                                
THIS WORKS!                                                                   
sysadmin@localhost:~$
```
### 8.2.11 Step 11
Another popular form of redirection is to take the output of one command and send it into another command as input. For example, the output of some commands can be massive, resulting in the output scrolling off the screen too quickly to read. Execute the following command to take the output of the ls command and send it into the more command, which displays one page of data at a time:
```
ls -l /etc | more
```
Your output should be similar to the following:
```
sysadmin@localhost:~$ ls -l /etc | more                                       
total 372                                                                     
-rw-r--r-- 1 root root    2981 Jan 28  2015 adduser.conf                      
-rw-r--r-- 1 root root      10 Jan 28  2015 adjtime                           
drwxr-xr-x 1 root root     900 Jan 29  2015 alternatives                      
drwxr-xr-x 1 root root     114 Jan 29  2015 apparmor.d                        
drwxr-xr-x 1 root root     168 Oct  1  2014 apt                               
-rw-r--r-- 1 root root    2076 Apr  3  2012 bash.bashrc                       
drwxr-xr-x 1 root root      72 Jan 28  2015 bash_completion.d                 
drwxr-sr-x 1 root bind     342 Jan 29  2015 bind                              
-rw-r--r-- 1 root root     356 Apr 19  2012 bindresvport.blacklist            
-rw-r--r-- 1 root root     321 Mar 30  2012 blkid.conf                        
lrwxrwxrwx 1 root root      15 Jun 18  2014 blkid.tab -> /dev/.blkid.tab      
drwxr-xr-x 1 root root      16 Jan 29  2015 ca-certificates                   
-rw-r--r-- 1 root root    7464 Jan 29  2015 ca-certificates.conf              
drwxr-xr-x 1 root root      14 Jan 29  2015 calendar                          
drwxr-xr-x 1 root root      24 Jan 29  2015 cron.d                            
drwxr-xr-x 1 root root     134 Jan 29  2015 cron.daily                        
drwxr-xr-x 1 root root      24 Jan 29  2015 cron.hourly                       
drwxr-xr-x 1 root root      24 Jan 29  2015 cron.monthly
-rw-r--r-- 1 root root    2969 Mar 15  2012 debconf.conf                      
--More--
```
You will need to press the spacebar to continue or you can also press ```CTRL+c``` to escape this listing.
The ```cut``` command is useful for extracting fields from files that are either delimited by a character, like the colon : in ```/etc/passwd```, or that have a fixed width. It will be used in the next few examples as it typically provides a great deal of output that we can use to demonstrate using the ```|``` character.
### 8.2.12 Step 12
In the following example, you will use a command called ```cut``` to extract all of the usernames from a database called ```/etc/passwd``` (a file that contains user account information). First, try running the cut command by itself:
```
cut -d: -f1 /etc/passwd
```
A portion of the command output is shown in the graphic below.
```
sysadmin@localhost:~$ cut -d: -f1 /etc/passwd                                 
root                                                                          
daemon                                                                        
bin                                                                           
sys                                                                           
sync                                                                          
games                                                                         
man                                                                           
lp                                                                            
mail                                                                          
news                                                                          
uucp                                                                          
proxy                                                                         
www-data                                                                      
backup                                                                        
list                                                                          
irc                                                                           
gnats                                                                         
nobody                                                                        
libuuid                                                                       
syslog                                                                       
bind                                                                          
sshd                                                                          
operator
```
### 8.2.13 Step 13
The output in the previous example was unordered and scrolled off the screen. In the next step you are going to take the output of the ```cut``` command and send it into the ```sort``` command to provide some order to the output:
```
cut -d: -f1 /etc/passwd | sort
```
A portion of the command output is shown in the graphic below.
```
sysadmin@localhost:~$ cut -d: -f1 /etc/passwd | sort                          
backup                                                                        
bin                                                                           
bind                                                                          
daemon                                                                        
games                                                                         
gnats                                                                         
irc                                                                           
libuuid                                                                       
list                                                                          
lp                                                                            
mail                                                                          
man                                                                           
news                                                                          
nobody                                                                        
operator                                                                      
proxy                                                                       
root                                                                          
sshd                                                                          
sync                                                                          
sys
```
### 8.2.14 Step 14
Now the output is sorted, but it still scrolls off the screen. Send the output of the ```sort``` command to the ```more``` command to solve this problem:
```
cut -d: -f1 /etc/passwd | sort | more
```
```
sysadmin@localhost:~$ cut -d: -f1 /etc/passwd | sort | more                   
backup                                                                        
bin                                                                           
bind                                                                          
daemon                                                                        
games                                                                         
gnats                                                                         
irc                                                                           
libuuid                                                                       
list                                                                          
lp                                                                            
mail                                                                          
man                                                                           
news                                                                          
nobody                                                                        
operator                                                                      
proxy                                                                         
root                                                                          
sshd                                                                          
sync                                                                          
sys                                                                           
sysadmin                                                                      
syslog                                                                        
uucp                                                                          
--More--
```
## 8.3 Viewing Large Text Files
Although large text files can be viewed with the ```cat``` command, it is inconvenient to scroll backwards towards the top of the file. Additionally, really large files can't be displayed in this manner because the terminal window only stores a specific number of lines of output in memory.
The use of the more or less commands allows for the user to the view data a "page" or a line at a time. These "pager" commands also permit other forms of navigation and searching that will be demonstrated in this section.
### Note
Examples are given using both the ```more``` and ```less``` commands. Most of the time, the commands work the same, however, the ```less``` command is more advanced and has more features. The ```more``` command is still important to know because some Linux distributions don't have the ```less``` command, but all Linux distributions have the ```more``` command.
If you are not interested in viewing the entire file or output of a command, then there are numerous commands that are able to filter the contents of the file or output. In this module, you will learn the use of the ```head``` and ```tail``` commands to be able to extract information from the top or bottom of the output of a command or file contents.
### 8.3.1 Step 1
The ```/etc/passwd``` is likely too large to be displayed on the screen without scrolling the screen. To see a demonstration of this, use the ```cat``` command to display the entire contents of the ```/etc/passwdfile```:
```
cat /etc/passwd
```
Your output should be similar to the following:
```
sysadmin@localhost:~$ cat /etc/passwd
daemon:x:1:1:daemon:/usr/sbin:/bin/sh                                         
bin:x:2:2:bin:/bin:/bin/sh                                                    
sys:x:3:3:sys:/dev:/bin/sh                                                    
sync:x:4:65534:sync:/bin:/bin/sync                                            
games:x:5:60:games:/usr/games:/bin/sh                                         
man:x:6:12:man:/var/cache/man:/bin/sh                                         
lp:x:7:7:lp:/var/spool/lpd:/bin/sh                                            
mail:x:8:8:mail:/var/mail:/bin/sh                                             
news:x:9:9:news:/var/spool/news:/bin/sh                                       
uucp:x:10:10:uucp:/var/spool/uucp:/bin/sh                                     
proxy:x:13:13:proxy:/bin:/bin/sh                                              
www-data:x:33:33:www-data:/var/www:/bin/sh                                    
backup:x:34:34:backup:/var/backups:/bin/sh                                    
list:x:38:38:Mailing List Manager:/var/list:/bin/sh                           
irc:x:39:39:ircd:/var/run/ircd:/bin/sh                                      
gnats:x:41:41:Gnats Bug-Reporting System (admin):/var/lib/gnats:/bin/sh       
nobody:x:65534:65534:nobody:/nonexistent:/bin/sh                              
libuuid:x:100:101::/var/lib/libuuid:/bin/sh                                   
syslog:x:101:103::/home/syslog:/bin/false                                     
bind:x:102:105::/var/cache/bind:/bin/false                                    
sshd:x:103:65534::/var/run/sshd:/usr/sbin/nologin                             
operator:x:1000:37::/root:/bin/sh                                             
sysadmin:x:1001:1001:System Administrator,,,,:/home/sysadmin:/bin/bash        
sysadmin@localhost:~$
```
### 8.3.2 Step 2
Use the more command to display the entire contents of the ```/etc/passwd``` file:
```
more /etc/passwd
```
Your output should be similar to the following:
```
sysadmin@localhost:~$ more /etc/passwd
root:x:0:0:root:/root:/bin/bash                                               
daemon:x:1:1:daemon:/usr/sbin:/bin/sh                                         
bin:x:2:2:bin:/bin:/bin/sh                                                    
sys:x:3:3:sys:/dev:/bin/sh                                                    
sync:x:4:65534:sync:/bin:/bin/sync                                            
games:x:5:60:games:/usr/games:/bin/sh                                         
man:x:6:12:man:/var/cache/man:/bin/sh                                         
lp:x:7:7:lp:/var/spool/lpd:/bin/sh                                            
mail:x:8:8:mail:/var/mail:/bin/sh                                             
news:x:9:9:news:/var/spool/news:/bin/sh                                       
uucp:x:10:10:uucp:/var/spool/uucp:/bin/sh                                     
proxy:x:13:13:proxy:/bin:/bin/sh                                              
www-data:x:33:33:www-data:/var/www:/bin/sh                                    
backup:x:34:34:backup:/var/backups:/bin/sh                                    
list:x:38:38:Mailing List Manager:/var/list:/bin/sh                           
irc:x:39:39:ircd:/var/run/ircd:/bin/sh                                        
gnats:x:41:41:Gnats Bug-Reporting System (admin):/var/lib/gnats:/bin/sh       
nobody:x:65534:65534:nobody:/nonexistent:/bin/sh                              
libuuid:x:100:101::/var/lib/libuuid:/bin/sh                                   
syslog:x:101:103::/home/syslog:/bin/false                                     
bind:x:102:105::/var/cache/bind:/bin/false                                    
sshd:x:103:65534::/var/run/sshd:/usr/sbin/nologin                             
operator:x:1000:37::/root:/bin/sh                                             
--More--(92%)
```
### Note
The ```--More--(92%)``` indicates you are "in" the ```more``` command and 92% through the current data.
### 8.3.3 Step 3
While you are in the ```more`` command, you can view the help screen by pressing the h key:
```
h
```
Your output should be similar to the following:
```
Most commands optionally preceded by integer argument k.  Defaults in brackets
Star (*) indicates argument becomes new default.                              
------------------------------------------------------------------------------
<space>                 Display next k lines of text [current screen size]    
z                       Display next k lines of text [current screen size]*   
<return>                Display next k lines of text [1]*                     
d or ctrl-D             Scroll k lines [current scroll size, initially 11]*   
q or Q or <interrupt>   Exit from more                                        
s                       Skip forward k lines of text [1]                      
f                       Skip forward k screenfuls of text [1]                 
b or ctrl-B             Skip backwards k screenfuls of text [1]               
'                       Go to place where previous search started             
=                       Display current line number                           
/<regular expression>   Search for kth occurrence of regular expression [1]   
n                       Search for kth occurrence of last r.e [1]             
!<cmd> or :!<cmd>       Execute <cmd> in a subshell                           
v                       Start up /usr/bin/vi at current line                  
ctrl-L                  Redraw screen                                         
:n                      Go to kth next file [1]                               
:p                      Go to kth previous file [1]                           
:f                      Display current file name and line number         
.                       Repeat previous command                               
------------------------------------------------------------------------------
--More--(92%)
```
### 8.3.4 Step 4
Press the Spacebar to view the rest of the document:
```
<SPACE>
```
In the next example, you will learn how to search a document using either the more or less commands.
Searching for a pattern within both the ```more``` and ```less``` commands is done by typing the ```slash /```, followed by the pattern to find. If a match is found, the screen should scroll to the first match. To move forward to the next match, press the ```n``` key. With the ```less``` command you can also move backwards to previous matches by pressing the ```N``` (capital n) key.
### 8.3.5 Step 5
Use the ```less``` command to display the entire contents of the ```/etc/passwd``` file. Then search for the word ```bin```, use ```n``` to move forward, and ```N``` to move backwards. Finally, quit the ```less``` pager by typing the letter ```q```:
```
less /etc/passwd
/bin
nnnNNNq
```
### Important
Unlike the ```more``` command which automatically exits when you reach the end of a file, you must press a quit key such as ```q``` to quit the ```less``` program.
### 8.3.6 Step 6
You can use the ```head``` command to display the top part of a file. By default, the ```head``` command will display the first ten lines of the file:
```
head /etc/passwd
```
Your output should be similar to the following:
```
sysadmin@localhost:~$ head /etc/passwd                                        
root:x:0:0:root:/root:/bin/bash                                               
daemon:x:1:1:daemon:/usr/sbin:/bin/sh                                         
bin:x:2:2:bin:/bin:/bin/sh                                                    
sys:x:3:3:sys:/dev:/bin/sh                                                    
sync:x:4:65534:sync:/bin:/bin/sync                                            
games:x:5:60:games:/usr/games:/bin/sh                                         
man:x:6:12:man:/var/cache/man:/bin/sh                                         
lp:x:7:7:lp:/var/spool/lpd:/bin/sh                                            
mail:x:8:8:mail:/var/mail:/bin/sh                                             
news:x:9:9:news:/var/spool/news:/bin/sh                                       
sysadmin@localhost:~$
```
### 8.3.7 Step 7
Use the tail command to display the last ten lines of the /etc/passwd file:
```
tail /etc/passwd
```
Your output should be similar to the following:
```
sysadmin@localhost:~$ tail /etc/passwd                                          
nobody:x:65534:65534:nobody:/nonexistent:/usr/sbin/nologin                      
_apt:x:100:65534::/nonexistent:/usr/sbin/nologin                                
systemd-network:x:101:102:systemd Network Management,,,:/run/systemd/netif:/usr/
sbin/nologin                                                                    
systemd-resolve:x:102:103:systemd Resolver,,,:/run/systemd/resolve:/usr/sbin/nol
ogin                                                                            
syslog:x:103:106::/home/syslog:/usr/sbin/nologin                                
messagebus:x:104:107::/nonexistent:/usr/sbin/nologin                            
bind:x:105:110::/var/cache/bind:/usr/sbin/nologin                               
sshd:x:106:65534::/run/sshd:/usr/sbin/nologin                                   
operator:x:1000:37::/root:/bin/sh                                               
sysadmin:x:1001:1001:System Administrator,,,,:/home/sysadmin:/bin/bash 
sysadmin@localhost:~$
```
### 8.3.8 Step 8
Use the ```head``` command to display the first two lines of the ```/etc/passwd``` file:
```
head -2 /etc/passwd
```
Your output should be similar to the following:
```
sysadmin@localhost:~$ head -2 /etc/passwd                                       
root:x:0:0:root:/root:/bin/bash                                                 
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin                                          
sysadmin@localhost:~$
```
### 8.3.9 Step 9
Execute the following command line to pipe the output of the ```ls``` command to the ```tail``` command, displaying the last five file names in the ```/etc``` directory:
```
ls /etc | tail -5
```
Your output should be similar to the following:
```
sysadmin@localhost:~$ ls /etc | tail -5                                         
updatedb.conf                                                                   
vim                                                                             
vtrgb                                                                           
wgetrc                                                                          
xdg                                 
sysadmin@localhost:~$
```
As you've seen, both ```head``` and ```tail``` commands output ten lines by default. You could also use an option ```-#``` (or you can use the option ```-n #```, where ```#``` is a number of lines to output). Both commands can be used to read standard input from a pipe that receives output from a command.
You have also seen where ```head``` and ```tail``` commands are different: the ```head``` command starts counting its lines to output from the top of the data, whereas the ```tail``` command counts the number of lines to output from the bottom of the data. There are some additional differences between these two commands as demonstrated in the next few tasks.
### 8.3.10 Step 10
Another way to specify how many lines to output with the head command is to use the option ```-n -#```, where ```#``` is the number of lines counted from the bottom of the output to exclude. Notice the minus symbol - in front of the ```#```. For example, if the ```/etc/passwd``` contains 27 lines, the following command will display lines 1-7, excluding the last twenty lines:
```
head -n -20 /etc/passwd
sysadmin@localhost:~$ head -n -20 /etc/passwd                                   
root:x:0:0:root:/root:/bin/bash                                                 
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin                                 
bin:x:2:2:bin:/bin:/usr/sbin/nologin                                            
sys:x:3:3:sys:/dev:/usr/sbin/nologin                                            
sync:x:4:65534:sync:/bin:/bin/sync                                              
games:x:5:60:games:/usr/games:/usr/sbin/nologin                                 
man:x:6:12:man:/var/cache/man:/usr/sbin/nologin           
sysadmin@localhost:~$
```
## 8.4 Searching Text Using Regular Expressions
In this task, you will use the grep family of commands with regular expressions in order to search for a specific string of characters in a stream of data (for example, a text file).
The grep command uses basic regular expressions, special characters like wildcards that match patterns in data. The ```grep``` command returns the entire line containing the pattern that matches.
The ```-E``` option to the grep command can be used to perform searches with extended regular expressions, essentially more powerful regular expressions. Another way to use extended regular expressions is to use the ```egrep``` command.
The ```fgrep``` command is used to match literal characters, ignoring the special meaning of regular expression characters.
### 8.4.1 Step 1
The use of ```grep``` in its simplest form is to search for a given string of characters, such as sshd in the ```/etc/passwd``` file. The ```grep``` command will print the entire line containing the match:
```
cd /etc
grep sshd passwd
```
Your output should be similar to the following:
```
sysadmin@localhost:~$ cd /etc                                                 
sysadmin@localhost:/etc$ grep sshd passwd                                       
sshd:x:106:65534::/run/sshd:/usr/sbin/nologin 
sysadmin@localhost:/etc$
```
### 8.4.2 Step 2
Regular expressions are "greedy" in the sense that they will match every single instance of the specified pattern:
```
grep root passwd
```
Your output should be similar to the following:
```
sysadmin@localhost:/etc$ grep root passwd                                     
root:x:0:0:root:/root:/bin/bash                                               
operator:x:1000:37::/root:/bin/sh                                             
sysadmin@localhost:/etc$
```
Note the red highlights indicate what exactly was matched. You can also see that all occurrences of root were matched on each line.
### 8.4.3 Step 3
To limit the output, you can use regular expressions to specify a more precise pattern. For example, the caret ```^``` character can be used to match a pattern at the beginning of a line; so, when you execute the following command line, only lines that begin with root should be matched and displayed:
```
grep '^root' passwd
```
Your output should be similar to the following:
```
sysadmin@localhost:/etc$ grep '^root' passwd                                   
root:x:0:0:root:/root:/bin/bash                                                
sysadmin@localhost:/etc$
```
Note that there are two additional instances of the word ```root``` but only the one appearing at the beginning of the line is matched (displayed in red).
### Best Practice
Use single quotes (not double quotes) around regular expressions to prevent the shell program from trying to interpret them.
### 8.4.4 Step 4
Match the pattern sync anywhere on a line:
```
grep 'sync' passwd
```
Your output should be similar to the following:
```
sysadmin@localhost:/etc$ grep 'sync' passwd                                   
sync:x:4:65534:sync:/bin:/bin/sync                                             
sysadmin@localhost:/etc$
```
### 8.4.5 Step 5
Use the ```$ symbol``` to match the pattern sync at the end of a line:
```
grep 'sync$' passwd
```
Your output should be similar to the following:
```
sysadmin@localhost:/etc$ grep 'sync$' passwd                                  
sync:x:4:65534:sync:/bin:/bin/sync                                            
sysadmin@localhost:/etc$
```
The command in the previous step matched every instance; the second only matches the instance at the end of the line.
### 8.4.6 Step 6
Use the period character ```.``` to match any single character. For example, execute the following command to match any character followed by a ```'y'```:
```
grep '.y' passwd
```
Your output should be similar to the following:
```
sysadmin@localhost:/etc$ grep '.y' passwd                                       
sys:x:3:3:sys:/dev:/usr/sbin/nologin                                            
sync:x:4:65534:sync:/bin:/bin/sync                                              
proxy:x:13:13:proxy:/bin:/usr/sbin/nologin                                      
gnats:x:41:41:Gnats Bug-Reporting System (admin):/var/lib/gnats:/usr/sbin/nologin                                                                               
nobody:x:65534:65534:nobody:/nonexistent:/usr/sbin/nologin                      
systemd-network:x:101:102:systemd Network Management,,,:/run/systemd/netif:/usr/sbin/nologin                                                                    
systemd-resolve:x:102:103:systemd Resolver,,,:/run/systemd/resolve:/usr/sbin/nologin                                                                            
syslog:x:103:106::/home/syslog:/usr/sbin/nologin                                
sysadmin:x:1001:1001:System Administrator,,,,:/home/sysadmin:/bin/bash     
sysadmin@localhost:/etc$
```
### 8.4.7 Step 7
The pipe character, ```|```, or "alternation operator", acts as an "or" operator. For example, execute the following to attempt to match either sshd, ```root``` or operator:
```
grep 'sshd|root|operator' passwd
Your output should be similar to the following:
sysadmin@localhost:/etc$ grep 'sshd|root|operator' passwd                     
sysadmin@localhost:/etc$
```
Observe that the ```grep``` command does not recognize the pipe as the alternation operator by default. The ```grep``` command is actually including the pipe as a plain character in the pattern to be matched. The use of either ```grep -E``` or ```egrep``` will allow the use of the extended regular expressions, including alternation.
### 8.4.8 Step 8
Use the ```-E``` switch to allow grep to operate in extended mode in order to recognize the alternation operator:
```
grep -E 'sshd|root|operator' passwd
```
Your output should be similar to the following:
```
sysadmin@localhost:/etc$ grep -E 'sshd|root|operator' passwd                  
root:x:0:0:root:/root:/bin/bash                                               
sshd:x:103:65534::/var/run/sshd:/usr/sbin/nologin                             
operator:x:1000:37::/root:/bin/sh                                             
sysadmin@localhost:/etc$
```
### 8.4.9 Step 9
Use another extended regular expression, this time with ```egrep``` with alternation in a group to match a pattern. The strings nob and non will match:
```
egrep 'no(b|n)' passwd
```
Your output should be similar to the following:
```
sysadmin@localhost:/etc$ egrep 'no(b|n)' passwd                                 
nobody:x:65534:65534:nobody:/nonexistent:/usr/sbin/nologin                      
_apt:x:100:65534::/nonexistent:/usr/sbin/nologin                                
messagebus:x:104:107::/nonexistent:/usr/sbin/nologin                                 
sysadmin@localhost:/etc$
```
### Note
The parentheses, ```( )```, were used to limit the "scope" of the ```|``` character. Without them, a pattern such as ```nob|n``` would have meant "match either ```nob``` or ```n```”.
### 8.4.10 Step 10
The ```[ ]``` characters can also be used to match a single character. However, unlike the period character ```.```, the ```[ ]``` characters are used to specify exactly what character you want to match. For example, if you want to match a numeric character, you can specify ```[0-9]```. Execute the following command for a demonstration:
```
head passwd | grep '[0-9]'
```
Your output should be similar to the following:
```
sysadmin@localhost:/etc$ head passwd | grep '[0-9]'                             
root:x:0:0:root:/root:/bin/bash                                                 
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin                                 
bin:x:2:2:bin:/bin:/usr/sbin/nologin                                            
sys:x:3:3:sys:/dev:/usr/sbin/nologin                                            
sync:x:4:65534:sync:/bin:/bin/sync                                              
games:x:5:60:games:/usr/games:/usr/sbin/nologin                                 
man:x:6:12:man:/var/cache/man:/usr/sbin/nologin                                 
lp:x:7:7:lp:/var/spool/lpd:/usr/sbin/nologin                                    
mail:x:8:8:mail:/var/mail:/usr/sbin/nologin                                     
news:x:9:9:news:/var/spool/news:/usr/sbin/nologin     
sysadmin@localhost:/etc$
```
### Note
The ```head``` command was used to limit the output of the ```grep``` command.
### 8.4.11 Step 11
Suppose you want to search for a pattern containing a sequence of three digits. You can use ```{ }``` characters with a number to express that you want to repeat a pattern a specific number of times; for example: ```{3}```. The use of the numeric qualifier requires the extended mode of grep:
```
grep -E '[0-9]{3}' passwd
Your output should be similar to the following:
sysadmin@localhost:/etc$ grep -E '[0-9]{3}' passwd                              
sync:x:4:65534:sync:/bin:/bin/sync                                              
nobody:x:65534:65534:nobody:/nonexistent:/usr/sbin/nologin                      
_apt:x:100:65534::/nonexistent:/usr/sbin/nologin                                
systemd-network:x:101:102:systemd Network Management,,,:/run/systemd/netif:/usr/sbin/nologin                                                                    
systemd-resolve:x:102:103:systemd Resolver,,,:/run/systemd/resolve:/usr/sbin/nologin                                                                            
syslog:x:103:106::/home/syslog:/usr/sbin/nologin                                
messagebus:x:104:107::/nonexistent:/usr/sbin/nologin                            
bind:x:105:110::/var/cache/bind:/usr/sbin/nologin                               
sshd:x:106:65534::/run/sshd:/usr/sbin/nologin                                   
operator:x:1000:37::/root:/bin/sh                                               
sysadmin:x:1001:1001:System Administrator,,,,:/home/sysadmin:/bin/bash       
sysadmin@localhost:/etc$
```
