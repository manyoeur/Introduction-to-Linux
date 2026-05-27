# Lab 01
## 1 Introduction
This is Lab 5: Command Line Skills. By performing this lab, students will learn how to use basic features of the shell.
In this lab, you will perform the following tasks:
*•	Explore Bash features
*•	Use shell variables
*•	Be able to make use of quoting

## 2 Files and Directories
In this task, we will access the Command Line Interface (CLI) for Linux to explore how to execute basic commands and what affects how they can be executed.
Most users are probably more familiar with how commands are executed using a Graphical User Interface (GUI). Therefore, this task will likely present some new concepts to you if you have not previously worked with a CLI. To use a CLI, you will need to type the command that you want to run.
The window where you will type your command is known as a terminal emulator application. Inside of the Terminal window the system is displaying a prompt, which currently contains a prompt followed by a blinking cursor:
```
sysadmin@localhost:~$
```

Remember

You may need to press Enter in the window to display the prompt.
The prompt tells you that you are user sysadmin; the host or computer you are using: localhost; and the directory where you are at: ~, which represents your home directory.
When you type a command, it will appear at the text cursor. You can use keys such as the home, end, backspace, and arrow keys for editing the command you are typing.
Equally important is the command line syntax, which is the order in which the command, the option(s), and argument(s) must be entered into the prompt so the shell recognizes how to properly execute the command. Proper command line syntax looks like the following:
command [options] [arguments]
Type the ls command at the prompt, which will list the files and directories contained in your current working directory. In this example, no options or arguments will be used.
Once you have typed the command correctly, press Enter to execute it.

```
sysadmin@localhost:~$ ls
```

Desktop  Documents  Downloads  Music  Pictures  Public  Templates  Videos

### 2.1 Step 1
The ls command is used to list information about directories and files and by default it displays information for the current directory. Use the -l option to display this information in the long format, which gives additional information about files located in the current working directory:
```
ls -l
```

Your output should be similar to the following:
```
sysadmin@localhost:~$ ls -l                                                     
total 32                                                                        
drwxr-xr-x 2 sysadmin sysadmin 4096 Oct 31 19:52 Desktop                        
drwxr-xr-x 4 sysadmin sysadmin 4096 Oct 31 19:52 Documents                      
drwxr-xr-x 2 sysadmin sysadmin 4096 Oct 31 19:52 Downloads                      
drwxr-xr-x 2 sysadmin sysadmin 4096 Oct 31 19:52 Music                          
drwxr-xr-x 2 sysadmin sysadmin 4096 Oct 31 19:52 Pictures                       
drwxr-xr-x 2 sysadmin sysadmin 4096 Oct 31 19:52 Public                         
drwxr-xr-x 2 sysadmin sysadmin 4096 Oct 31 19:52 Templates                      
drwxr-xr-x 2 sysadmin sysadmin 4096 Oct 31 19:52 Videos
```

Note that directories are considered a type of file in the Linux file system.

### 2.2 Step 2

Arguments can be added to commands as well. Adding the location of a specific directory to the ls command will list information for that directory. Use the argument /home to display detailed information about files in the /home directory.
```
ls -l /home
```

Your output should be similar to the following:
```
sysadmin@localhost:~$ ls -l /home                                                
total 4                                                                         
drwxr-xr-x 1 sysadmin sysadmin 4096 Aug  8 17:46 sysadmin
```

By using the -l option and the /home argument, we can now see that the /home directory has a directory called sysadmin located inside it.

### 2.3 Step 3
The following command will display the same information that you see in the first part of the prompt. Make sure that you have selected (clicked on) the Terminal window first and then type the following command followed by the Enter key:

```
whoami
```

Your output should be similar to the following:

```
sysadmin@localhost:~$ whoami                            
sysadmin                                                
sysadmin@localhost:~$
```

The output of the whoami command, sysadmin, displays the user name of the current user. Although in this case your username is displayed in the prompt, this command could be used to obtain this information in a situation when the prompt did not contain this information.

### 2.4 Step 4
The next command displays information about the current system. To be able to see the name of the kernel you are using, type the following command into the terminal:
uname
Your output should be similar to the following:
```
sysadmin@localhost:~$ uname
```
                             
Linux

Many commands that are executed produce text output like this. You can change what output is produced by a command by using options after the name of the command.
Options for a command can be specified in several ways. Traditionally in UNIX, options were expressed by a hyphen followed by another character; for example: -n.
In Linux, options can sometimes also be given by two hyphen characters followed by a word, or hyphenated word; for example: --nodename.
Execute the uname command again twice in the terminal, once with the option -n and again with the option --nodename. This will display the network node hostname, also found in the prompt.

```
uname -n
uname --nodename
```

Your output should be similar to the following:

```
sysadmin@localhost:~$ uname -n                          
localhost                                               
sysadmin@localhost:~$ uname --nodename                  
localhost
```

### 2.5 Step 5

The pwd command is used to display your current "location" or current "working" directory. Type the following command to display the working directory:
```
pwd
```
Your output should be similar to the following:
```
sysadmin@localhost:~$ pwd                                            
/home/sysadmin                                                       
sysadmin@localhost:~$
```

The current directory in the example above is /home/sysadmin. This is also referred to as your home directory, a special place where you have control of files and other users normally have no access. By default, this directory is named the same as your username and is located underneath the /home directory.
As you can see from the output of the command, /home/sysadmin, Linux uses the forward slash / to separate directories to make what is called a path. The initial forward slash represents the top-level directory, known as the root directory. More information regarding files, directories and paths will be presented in later labs.
The tilde ~ character that you see in your prompt is also indicating what the current directory is. This character is a "shortcut" way to represent your home.
Consider This
pwd stands for "print working directory". While it doesn't actually "print" in modern versions, older UNIX machines didn't have monitors so the output of commands went to a printer, hence the somewhat misleading name of pwd.

## 5.3 Command History

The Bash shell maintains a history of the commands that you type. Previous commands can be easily accessed in this history in several ways.
The first and easiest way to recall a previous command is to use the up arrow key. Each press of the up arrow key goes backwards one command through your command history. If you accidentally go back too far, then the down arrow key will go forwards through the history of commands.
When you find the command that you want to execute, you can use the left arrow keys and right arrow keys to position the cursor for editing. Other useful keys for editing include the Home, End, Backspace and Delete keys.
Another way to use your command history is to execute the history command to be able to view a numbered history list. The number listed to the left of the command can be used to execute the command again. The history command also has a number of options and arguments which can manipulate which commands will be stored or displayed.
### 3.1 Step 1
Execute a new command and then execute the history command:
```
echo Hi
history
```

Remember

The date command will print the time and date on the system. The clear command clears the screen.
Your output should be similar to the following:
```
sysadmin@localhost:~$ history                                                   
    1  ls                                                                       
    2  ls -l                                                                    
    3  ls -l /tmp                                                               
    4  whoami                                                                   
    5  uname                                                                    
    6  uname -n                                                                 
    7  uname --nodename                                                         
    8  pwd                                                                      
    9  echo Hi                                                                  
   10  history                                                                  
sysadmin@localhost:~$
```

Your command numbers may differ from those provided above. This is because you may have executed a different number of commands since opening the virtual terminal.

### 5.3.2 Step 2

To view a limited number of commands, the history command can take a number as a parameter to display exactly that many recent entries. Type the following command to display the last five commands from your history:
history 5
Your output should be similar to the following:
```
sysadmin@localhost:~$ history 5                                                 
    7  uname --nodename                                                         
    8  pwd                                                                      
    9  echo Hi                                                                  
   10  history                                                                  
   11  history 5
```
### 3.3 Step 3

To execute a command again, type the exclamation point and the history list number. For example, to execute the 9th command in your history list, you would execute the following:
```
!9
sysadmin@localhost:~$ !9                                                        
echo Hi                                                                         
Hi
```

### 3.4 Step 4
Next, experiment with accessing your history using the up arrow keys and down arrow keys. Keep pressing the up arrow key until you find a command you want to execute. If necessary, use other keys to edit the command and then press Enter to execute the command.
## 5.4 Shell Variables
Shell variables are used to store data in Linux. This data is used by the shell itself as well as by programs and users.
The focus of this section is to learn how to display the values of shell variables.
### 4.1 Step 1
The echo command can be used to print text and the value of a variable, and to show how the shell environment expands metacharacters (more on metacharacters later in this lab). Type the following command to have it output literal text:
```
echo Hello Student
Your output should be similar to the following:
sysadmin@localhost:~$ echo Hello Student                             
Hello Student                                                        
sysadmin@localhost:~$
```
### 4.2 Step 2
Environment variables are available system-wide. The system automatically recreates environment variables when a new shell is opened. Examples include the PATH, HOME, and HISTSIZE variables. The HISTSIZE variable defines how many previous commands to store in the history list. In the example below, the command will display the value of the HISTSIZE variable:
```
sysadmin@localhost:~$ echo $HISTSIZE‌
1000                                                           
sysadmin@localhost:~$
```
### 4.3 Step 3
Type the following command to display the value of the PATH variable:
```
echo $PATH
```
Your output should be similar to the following:
```
sysadmin@localhost:~$ echo $PATH                                    
/home/sysadmin/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:
/usr/games:/usr/local/games:/snap/bin                                                 
sysadmin@localhost:~$
```
The PATH variable is displayed by placing a $ character in front of the name of the variable.
This variable is used to find the location of commands. Each of the directories listed above are searched when you run a command. For example, if you try to run the date command, the shell will first look for the command in the /home/sysadmin/bin directory and then in the /usr/local/sbin directory and so on. Once the date command is found, the shell "runs it”.
### 4.4 Step 4
Use the which command to determine if there is an executable file, in this case named date, that is located within a directory listed in the PATH value:
```
which date
```
Your output should be similar to the following:
```
sysadmin@localhost:~$ which date                                    
/bin/date                                                           
sysadmin@localhost:~$
```
The output of the which command tells you that when you execute the date command, the system will run the command /bin/date. The which command makes use of the PATH variable to determine the location of the date command.
## 5.5 Command Types
In this section we will learn about the four types of commands used in Linux. Understanding where these commands come from and how they differ allows an administrator to manage the system more effectively.
### 5.1 Step 1
One way to learn more about a command is to look at where it comes from. The type command can be used to determine information about command type.
```
type command
```
There are several different sources of commands within the shell of your CLI:
Internal commands are built into the shell itself. A good example is the cd (change directory) command as it is part of the Bash shell. When a user types the cd command, the Bash shell is already executing and knows how to interpret it, requiring no additional programs to be started.
The type command identifies the cd command as an internal command:
```
sysadmin@localhost:~$ type cd                                     
cd is a shell builtin
```
### 5.2 Step 2
External commands are binary executables stored in directories that are searched by the shell. If a user types the ls command, the shell searches through the directories that are listed in the PATH variable to try to find a file named ls that it can execute. Use the which command to display the full path to the ls command.
```
which ls
sysadmin@localhost:~$ which ls
/bin/ls
```
For external commands, the type command displays the location of the command:
```
sysadmin@localhost:~$ type cp                                      
cp is /bin/cp
```
In some cases the output of the type command may differ significantly from the output of the which command:
```
sysadmin@localhost:~$ which cp                                        
/bin/cp
```
Using the -a option of the type command displays all locations that contain the command:
```
sysadmin@localhost:~$ type -a ls 
ls is aliased to `ls --color=auto'
ls is /bin/ls
```
### 5.3 Step 3
Aliases can be used to map longer commands to shorter key sequences. When the shell sees an alias being executed, it substitutes the longer sequence before proceeding to interpret commands.
To determine what aliases are set on the current shell, use the alias command:
```
sysadmin@localhost:~$ alias                                                     
alias alert='notify-send --urgency=low -i "$([ $? = 0 ] && echo terminal || echo
 error)" "$(history|tail -n1|sed -e '\''s/^\s*[0-9]\+\s*//;s/[;&|]\s*alert$//'\'')"'                                                                            
alias egrep='egrep --color=auto'                                                
alias fgrep='fgrep --color=auto'                                                
alias grep='grep --color=auto'                                                  
alias l='ls -CF'                                                                
alias la='ls -A'                                                                
alias ll='ls -alF'                                                              
alias ls='ls --color=auto'
```
### 5.4 Step 4
The final command type is the executable program. These commands invoke programs installed on the system which perform specific tasks. When a user types the vi command, the shell uses the PATH file to locate and execute the program. Programs like vi are available on just about every Linux distribution; other programs, like vlc (an open source media player often used on Linux desktops), are installed by users or administrators for a specific purpose and will not be listed in the PATH unless they have been installed separately.
```
type vi
cd /bin
type vlc
cd
sysadmin@localhost:~$ type vi 
vi is /usr/bin/vi
sysadmin@localhost:~$ cd /bin
sysadmin@localhost:/bin$ type vlc                                               
-bash: type: vlc: not found
sysadmin@localhost:/bin$ cd
sysadmin@localhost:~$
```
## 5.6 Quoting
There are three types of quotes used by the Bash shell: single quotes ('), double quotes (") and back quotes (`). These quotes have special features in the Bash shell as described below.
To understand single and double quotes, consider that there are times that you don't want the shell to treat some characters as special. For example, the * character is used as a wildcard. What if you wanted the * character to just mean a literal asterisk?
•	Single ' quotes prevent the shell from "interpreting" or expanding all special characters. Often single quotes are used to protect a string (a sequence of characters) from being changed by the shell, so that the string can be interpreted by a command as a parameter to affect the way the command is executed.
•	Double " quotes stop the expansion of glob characters like the asterisk (*), question mark (?), and square brackets ( [] ). Double quotes do allow for both variable expansion and command substitution (see back quotes) to take place.
•	Back ` quotes cause command substitution which allows for a command to be executed within the line of another command.
When using quotes, they must be entered in pairs or else the shell will not consider the command complete.
While single quotes are useful for blocking the shell from interpreting one or more characters, the shell also provides a way to block the interpretation of just a single character called "escaping" the character. To escape the special meaning of a shell metacharacter, the backslash \ character is used as a prefix to that one character.
### 6.1 Step 1
Execute the following command which uses back quotes ` (found under the ~ character on some keyboards) to execute the date command within the line of the echo command:
```
echo Today is `date`
```
Your output should be similar to the following:
```
sysadmin@localhost:~$ echo Today is `date`                               
Today is Mon Feb 12 20:47:22 UTC 2024
```
### 6.2 Step 2
You can also place $( before the command and ) after the command to accomplish command substitution:
```
echo Today is $(date)
Your output should be similar to the following:
sysadmin@localhost:~$ echo Today is $(date)                                     
Today is Mon Feb 12 20:48:10 UTC 2024
```
Why two different methods that accomplish the same thing? Backquotes look very similar to single quotes, making it harder to "see" what a command is supposed to do. Originally, shells used backquotes; the $(command) format was added in a later version of the Bash shell to make the statement more visually clear.
### 6.3 Step 3
If you don't want the backquotes to be used to execute a command, place single quotes around them. Execute the following:
```
echo This is the command '`date`'
```
Your output should be similar to the following:
```
sysadmin@localhost:~$ echo This is the command '`date`'             
This is the command `date`                                           
sysadmin@localhost:~$
```
### 6.4 Step 4
Note that you could also place a backslash \ character in front of each backquote character. Execute the following:
```
echo This is the command \`date\`
Your output should be similar to the following:
sysadmin@localhost:~$ echo This is the command \`date\`     
This is the command `date`                                  
sysadmin@localhost:~$
```
### 6.5 Step 5
Double quote " characters don't have any effect on backquote characters. The shell will still use them as command substitution. Execute the following to see a demonstration:
```
echo This is the command "`date`"
Your output should be similar to the following:
sysadmin@localhost:~$ echo This is the command "`date`"               
This is the command Mon Feb 12 20:51:10 UTC 2024
```
### 6.6 Step 6
Double quote characters will have an effect on wildcard characters, disabling their special meaning. Execute the following:
```
echo D*
echo "D*"
```
Your output should be similar to the following:
```
sysadmin@localhost:~$ echo D*                                        
Desktop Documents Downloads                                          
sysadmin@localhost:~$ echo "D*"                                      
D*                                                                   
sysadmin@localhost:~$
```
Important

Quoting may seem trivial and weird at the moment, but as you gain more experience working in the command shell, you will discover that having a good understanding of how different quotes work is critical to using the shell.
## 5.7 Control Statements
Typically, you type a single command and you execute it when you press Enter. The Bash shell offers three different statements that can be used to separate multiple commands typed together.
The simplest separator is the semicolon (;). Using the semicolon between multiple commands allows for them to be executed one right after another, sequentially from left to right.
The && characters create a logical "and" statement. Commands separated by && are conditionally executed. If the command on the left of the && is successful, then the command to the right of the && will also be executed. If the command to the left of the && fails, then the command to the right of the && is not executed.
The || characters create a logical "or" statement, which also causes conditional execution. When commands are separated by ||, then only if the command to the left fails, does the command to the right of the || execute. If the command to the left of the || succeeds, then the command to the right of the || will not execute.
To see how these control statements work, you will be using two special executables: true and false. The true executable always succeeds when it executes, whereas, the false executable always fails. While this may not provide you with realistic examples of how && and || work, it does provide a means to demonstrate how they work without having to introduce new commands.
### 5.7.1 Step 1
Execute the following three commands together separated by semicolons:
echo Hello; echo Linux; echo Student
As you can see the output shows all three commands executed sequentially:
```
sysadmin@localhost:~$ echo Hello; echo Linux; echo Student           
Hello                                                                
Linux                                                              
Student                                                             
sysadmin@localhost:~$
```
### 5.7.2 Step 2
Now, put three commands together separated by semicolons, where the first command executes with a failure result:
false; echo Not; echo Conditional
Your output should be similar to the following:
```
sysadmin@localhost:~$ false; echo Not; echo Conditional          
Not                                                       
Conditional                                              
sysadmin@localhost:~$
```
Note that in the previous example, all three commands still executed even though the first one failed. While you can't see from the output of the false command, it did execute. However, when commands are separated by the ; character, they are completely independent of each other.
### 5.7.3 Step 3
Next, use logical "and" to separate the commands:
```
echo Start && echo Going && echo Gone
Your output should be similar to the following:
sysadmin@localhost:~$ echo Start && echo Going && echo Gone          
Start                                                                
Going                                                                
Gone                                                                 
sysadmin@localhost:~$
```
Because each echo statement executes correctly, a return value of success is provided, allowing the next statement to also be executed.
### 5.7.4 Step 4
Use logical "and" with a command that fails as shown below:
```
echo Success && false && echo Bye
Your output should be similar to the following:
sysadmin@localhost:~$ echo Success && false && echo Bye              
Success                                                              
sysadmin@localhost:~$
```
The first echo command succeeds and we see its output. The false command executes with a failure result, so the last echo statement is not executed.
### 5.7.5 Step 5
The "or" characters separating the following commands demonstrates how the failure before the "or" statement causes the command after it to execute; however, a successful first statement causes the command to not execute:
```
false || echo Fail Or
true || echo Nothing to see here
```
Your output should be similar to the following:
```
sysadmin@localhost:~$ false || echo Fail Or                         
Fail Or                                                              
sysadmin@localhost:~$ true || echo Nothing to see here                    
sysadmin@localhost:~$
```
