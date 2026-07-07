# Archiving and Compression
## 7.1 Introduction
This is Lab 7: Archiving and Compression. By performing this lab, students will learn how to work with archive files.
In this lab, you will perform the following tasks:
*	Create archive files using tar with and without compression
*	Compress and uncompress files into a ```gzip``` archive file
*	Compress and uncompress files into a ```bzip2``` archive file
*	Compress and uncompress files into an ```xz``` archive file
*	Use zip and ```unzip``` to compress and uncompress archive files
## 7.2 Archiving Commands
In this task, we will use ```gzip```, ```bzip2```, ```tar```, ```zip/unzip``` and ```xz/unxz``` to archive and restore files. These commands are designed to either merge multiple files into a single file or compress a large file into a smaller one. In some cases, the commands will perform both functions.
The task of archiving data is important for several reasons, including but not limited to the following:
*	Large files may be difficult to transfer. Making these files smaller helps make transfer quicker.
*	Transferring multiple files from one system to another can become tedious when there are many files. Merging them into a single file for transport makes this process easier.
*	Files can quickly take up a lot of space, especially on smaller removable media like thumb drives. Archiving reduces this problem.
One potential area of confusion that a beginner Linux user may experience stems from the following question: why are there so many different archiving commands? The answer is that these commands have different features (for example, some of them allow you to password protect the archive file) and compression techniques used.
The most important thing to know for now is how these different commands function. Over time you will learn to pick the correct archive tool for any given situation.
### 7.2.1 Step 1
Use the following ```tar``` command to create an archive of the ```/etc/udev``` directory. Save the backup in the ```~/mybackups``` directory:
```
cd
mkdir mybackups
tar –cvf mybackups/udev.tar /etc/udev
ls mybackups
```
Your output should be similar to the following:
```
sysadmin@localhost:~$ cd                                                        
sysadmin@localhost:~$ mkdir mybackups                                           
sysadmin@localhost:~$ tar -cvf mybackups/udev.tar /etc/udev                     
tar: Removing leading `/' from member names                                     
/etc/udev/                                                                      
/etc/udev/rules.d/                                                              
/etc/udev/rules.d/70-persistent-cd.rules                                        
/etc/udev/rules.d/README                                                        
/etc/udev/hwdb.d/                                                               
/etc/udev/udev.conf                                                             
sysadmin@localhost:~$ ls mybackups                                              
udev.tar                                                      
sysadmin@localhost:~$
```
The ```tar``` command is used to merge multiple files into a single file. By default, it does not compress the data.
The ```-c``` option tells the tar command to create a ```tar``` file. The -v option stands for "verbose", which instructs the ```tar``` command to demonstrate what it is doing. The ```-f``` option is used to specify the name of the ```tar``` file.
### Consider This
```tar``` stands for Tape ARchive. This command was originally used to create tape backups, but today it is more commonly used to create archive files.
### Important
You are not required to use the ```.tar``` extension to the archive file name, however, it is helpful for identifying the file type. It is considered "good style" when sending an archive file to another person.
### 7.2.2 Step 2
Display the contents of a ```tar``` file by using the available options (t = list contents, v = verbose, f = filename):
```
tar –tvf mybackups/udev.tar
```
Your output should be similar to the following:
```
sysadmin@localhost:~$ tar -tvf mybackups/udev.tar                               
drwxr-xr-x root/root         0 2021-02-08 15:07 etc/udev/                       
drwxr-xr-x root/root         0 2021-02-08 15:08 etc/udev/rules.d/               
-rw-r--r-- root/root       306 2021-02-08 15:08 etc/udev/rules.d/70-persistent-cd.rules                                                                         
-rw-r--r-- root/root      1157 2021-02-08 15:08 etc/udev/rules.d/README         
drwxr-xr-x root/root         0 2021-01-06 21:04 etc/udev/hwdb.d/                
-rw-r--r-- root/root       218 2021-02-08 15:08 etc/udev/udev.conf     
sysadmin@localhost:~$
```
Notice that files were backed up recursively using relative path names. This is important because when you extract the files, they will be placed in your current directory, not override the current files.
### 7.2.3 Step 3
To create a ```tar``` file that is compressed, use the ```-z``` option. The ```-z``` option makes use of the ```gzip``` utility to perform compression.
```
tar –zcvf mybackups/udev.tar.gz /etc/udev
ls –lh mybackups
```
Your output should be similar to the following:
```
sysadmin@localhost:~$ tar -zcvf mybackups/udev.tar.gz /etc/udev
tar: Removing leading `/' from member names                                     
/etc/udev/                                                                      
/etc/udev/rules.d/                                                              
/etc/udev/rules.d/70-persistent-cd.rules                                        
/etc/udev/rules.d/README                                                        
/etc/udev/hwdb.d/                                                               
/etc/udev/udev.conf                                                              
sysadmin@localhost:~$ ls -lh mybackups/                                         
total 16K                                                                       
-rw-rw-r-- 1 sysadmin sysadmin  10K Feb  9 17:34 udev.tar                       
-rw-rw-r-- 1 sysadmin sysadmin 1.2K Feb  9 17:45 udev.tar.gz            
sysadmin@localhost:~$
```
Notice the difference in size; the first backup (10K bytes) is larger than the second backup (1.2K bytes).
### 7.2.4 Step 4
Extract the contents of an archive. Data is restored to the current directory by default.
```
cd mybackups
ls
tar –xvf udev.tar.gz
ls 
ls etc
ls etc/udev
ls etc/udev/rules.d
```
Your output should be similar to the following:
```
sysadmin@localhost:~$ cd mybackups                                            
sysadmin@localhost:~/mybackups$ ls                                            
udev.tar  udev.tar.gz                                                         
sysadmin@localhost:~/mybackups$ tar -xvf udev.tar.gz                            
etc/udev/                                                                       
etc/udev/rules.d/                                                               
etc/udev/rules.d/70-persistent-cd.rules                                         
etc/udev/rules.d/README                                                         
etc/udev/hwdb.d/                                                                
etc/udev/udev.conf                                              
sysadmin@localhost:~/mybackups$ ls                                            
etc  udev.tar  udev.tar.gz                                                    
sysadmin@localhost:~/mybackups$ ls etc                                          
udev                                                                            
sysadmin@localhost:~/mybackups$ ls etc/udev                                     
hwdb.d  rules.d  udev.conf                                                      
sysadmin@localhost:~/mybackups$ ls etc/udev/rules.d
70-persistent-cd.rules  README     
sysadmin@localhost:~/mybackups$
```
If you wanted the files to "go back" into their original location, you could first ```cd``` to the ```/``` directory and then run the ```tar``` command. However, in this example, this would require you to be logged in as an administrator because creating files in the ```/etc``` directory can only be done by the administrator.
### 7.2.5 Step 5
To add a file to an existing archive, use the ```-r``` option to the tar command. Execute the following commands to perform this action and verify the existence of the new file in the ```tar``` archive:
```
tar -rvf udev.tar /etc/hosts
tar –tvf udev.tar
Your output should be similar to the following:
sysadmin@localhost:~/mybackups$ tar -rvf udev.tar /etc/hosts             
tar: Removing leading `/' from member names                               
/etc/hosts                                                                
sysadmin@localhost:~/mybackups$ tar -tvf udev.tar                               
drwxr-xr-x root/root         0 2021-02-08 15:07 etc/udev/                       
drwxr-xr-x root/root         0 2021-02-08 15:08 etc/udev/rules.d/               
-rw-r--r-- root/root       306 2021-02-08 15:08 etc/udev/rules.d/70-persistent-cd.rules                                                                         
-rw-r--r-- root/root      1157 2021-02-08 15:08 etc/udev/rules.d/README         
drwxr-xr-x root/root         0 2021-01-06 21:04 etc/udev/hwdb.d/                
-rw-r--r-- root/root       218 2021-02-08 15:08 etc/udev/udev.conf              
-rw-r--r-- root/root       172 2024-02-09 17:33 etc/hosts    
sysadmin@localhost:~/mybackups$
```
### 7.2.6 Step 6
In the following examples, you will use gzip and gunzip to compress and uncompress a file. Execute the following commands to compress a copy of the words file:
```
cp /usr/share/dict/words .
ls -l words
gzip words
ls -l words.gz
```
Your output should be similar to the following:
```
sysadmin@localhost:~/mybackups$ cp /usr/share/dict/words .                
sysadmin@localhost:~/mybackups$ ls -l words                               
-rw-r--r-- 1 sysadmin sysadmin 971578 Feb  9 17:59 words                  
sysadmin@localhost:~/mybackups$ gzip words                                
sysadmin@localhost:~/mybackups$ ls -l words.gz                            
-rw-r--r-- 1 sysadmin sysadmin 259983 Feb  9 17:59 words.gz               
sysadmin@localhost:~/mybackups$
```
Notice the size of the zipped words file (259983 bytes in the example above) is much smaller than the original file (971578 bytes in the example above).
### Very important
When you use ```gzip```, the original file is replaced by the zipped file. In the example above, the words file was replaced with ```words.gz```.
When you ```unzip``` the file, the ```zipped``` file will be replaced with the original file.
### 7.2.7 Step 7
Execute the following commands to uncompress the ```words.gz``` file:
```
ls -l words.gz
gunzip words.gz
ls -l words
```
Your output should be similar to the following:
```
sysadmin@localhost:~/mybackups$ ls -l words.gz                                  
-rw-r--r-- 1 sysadmin sysadmin 259983 Feb  9 17:59 words.gz               
sysadmin@localhost:~/mybackups$ gunzip words.gz                                 
sysadmin@localhost:~/mybackups$ ls -l words                                     
-rw-r--r-- 1 sysadmin sysadmin 971578 Feb  9 17:59 words         
sysadmin@localhost:~/mybackups$
```
Linux provides a large number of compression utilities in addition to gzip/gunzip. Each of them has pros and cons (faster compression, better compression rates, more flexible, more portable, faster decompression, etc.).
The ```gzip/gunzip``` commands are very popular in Linux, but you should be aware that ```bzip2/bunzip2``` are also popular on some Linux distributions. It is fortunate that most of the functionality (the way you run the commands) and options are the same as ```gzip/gunzip```.
### 7.2.8 Step 8
Using ```bzip2``` and ```bunzip2``` to compress and uncompress a file is very similar to using ```gzip``` and ```gunzip```. The compressed file is created with a ```.bz2``` extension. The extension is removed when uncompressed. Execute the following commands to compress a copy of the words file:
```
ls -l words
bzip2 words
ls -l words.bz2
```
Your output should be similar to the following:
```
sysadmin@localhost:~/mybackups$ ls -l words                                     
-rw-r--r-- 1 sysadmin sysadmin 971578 Feb  9 17:59 words
sysadmin@localhost:~/mybackups$ bzip2 words
sysadmin@localhost:~/mybackups$ ls -l words.bz2                                 
-rw-r--r-- 1 sysadmin sysadmin 345560 Feb  9 17:59 words.bz2
```
If you compare the resulting ```.bz2``` file size (345560) to the ```.gz``` file size (259983) from Step 7, you will notice that ```gzip``` did a better job compressing this particular file.
### 7.2.9 Step 9
Execute the following commands to uncompress the words.bz2 file:
```
ls -l words.bz2
bunzip2 words.bz2
ls -l words
```
```
sysadmin@localhost:~/mybackups$ ls -l words.bz2                                 
-rw-r--r-- 1 sysadmin sysadmin 345560 Feb  9 17:59 words.bz2 
sysadmin@localhost:~/mybackups$ bunzip2 words.bz2                               
sysadmin@localhost:~/mybackups$ ls -l words                                     
-rw-r--r-- 1 sysadmin sysadmin 971578 Feb  9 17:59 words
```
### 7.2.10 Step 10
Using ```xz``` and ```unxz``` to compress and uncompress a file is also very similar to using ```gzip``` and ```gunzip```. The compressed file is created with a ```.xz``` extension. The extension is removed when uncompressed. Execute the following commands to compress a copy of the words file:
```
ls -l words
xz words
ls -l words.xz
```
Your output should be similar to the following:
```
sysadmin@localhost:~/mybackups$ ls -l words                                     
-rw-r--r-- 1 sysadmin sysadmin 971578 Feb  9 17:59 words                        
sysadmin@localhost:~/mybackups$ xz words                                        
sysadmin@localhost:~/mybackups$ ls -l words.xz                                  
-rw-r--r-- 1 sysadmin sysadmin 198756 Feb  9 17:59 words.xz            
sysadmin@localhost:~/mybackups$
```
If you compare the resulting ```.xz``` file size (198756) to the ```.gz``` file size (259983) from Step 7, you will notice that ```xz``` did a better job compressing this particular file.
### 7.2.11 Step 11
Execute the following commands to uncompress the ```words.xz``` file:
```
ls -l words.xz
unxz words.xz
ls -l words
```
```
sysadmin@localhost:~/mybackups$ ls -l words.xz                                  
-rw-r--r-- 1 sysadmin sysadmin 198756 Feb  9 17:59 words.xz                  
sysadmin@localhost:~/mybackups$ unxz words.xz                                   
sysadmin@localhost:~/mybackups$ ls -l words                                     
-rw-r--r-- 1 sysadmin sysadmin 971578 Feb  9 17:59 words
```
While ```gzip```, ```bzip``` and ```xz``` archive files are commonly used in Linux, the ```zip``` archive type is more commonly used by other operating systems, such as Windows. In fact, the Windows Explorer application has built-in support to extract ```zip``` archive files.
Therefore, if you are planning to share an archive with Windows users, it is usually preferred to use the ```zip``` archive type. Unlike ```gzip``` and ```bzip2```, when a file is compressed with the ```zip``` command, a copy of the original file is compressed and the original remains uncompressed.
### 7.2.12 Step 12
Use the ```zip``` command to compress the words file:
```
zip words.zip words
ls -l words.zip
```
Your output should be similar to the following:
```
sysadmin@localhost:~/mybackups$ zip words.zip words                             
  adding: words (deflated 73%)                                                  
sysadmin@localhost:~/mybackups$ ls -l words.zip                                 
-rw-rw-r-- 1 sysadmin sysadmin 260119 Feb  9 18:23 words.zip        
sysadmin@localhost:~/mybackups$
```
In the example above, the first argument (words.zip) of the ```zip``` command is the file name that you wish to create. The remaining arguments (words) are the files you want placed in the compressed file.
### Important
You are not required to use the ```.zip``` extension to the compressed file name; however, it is helpful for determining the file type. It is also considered "good style" when sending an archive file to another person.
### 7.2.13 Step 13
Compress the /etc/udev directory and its contents with zip compression:
```
zip -r udev.zip /etc/udev
ls -l udev.zip
```
Your output should be similar to the following:
```
sysadmin@localhost:~/mybackups$ zip -r udev.zip /etc/udev                       
  adding: etc/udev/ (stored 0%)                                                 
  adding: etc/udev/rules.d/ (stored 0%)                                         
  adding: etc/udev/rules.d/70-persistent-cd.rules (deflated 29%)                
  adding: etc/udev/rules.d/README (deflated 50%)                                
  adding: etc/udev/hwdb.d/ (stored 0%)                                          
  adding: etc/udev/udev.conf (deflated 24%)                                         
sysadmin@localhost:~/mybackups$ ls -l udev.zip                                  
-rw-rw-r-- 1 sysadmin sysadmin 2000 Feb  9 18:25 udev.zip                                          
sysadmin@localhost:~/mybackups$
```
The ```tar``` command discussed earlier in this lab automatically descends through any subdirectories of a directory specified to be archived. With the ```bzip2```, ```gzip```, and ```zip``` commands the recursive ```-r``` option must be specified in order to perform recursion into subdirectories.
### 7.2.14 Step 14
To view the contents of a ```zip``` archive, use with the ```-l``` option with the ```unzip``` command:
```
unzip -l udev.zip
```
Your output should be similar to the following:
```
sysadmin@localhost:~/mybackups$ unzip -l udev.zip                               
Archive:  udev.zip                                                              
  Length      Date    Time    Name                                              
---------  ---------- -----   ----                                              
        0  2021-02-08 15:07   etc/udev/                                         
        0  2021-02-08 15:08   etc/udev/rules.d/                                 
      306  2021-02-08 15:08   etc/udev/rules.d/70-persistent-cd.rules           
     1157  2021-02-08 15:08   etc/udev/rules.d/README                           
        0  2021-01-06 21:04   etc/udev/hwdb.d/                                  
      218  2021-02-08 15:08   etc/udev/udev.conf                                
---------                     -------                                           
     1681                     6 files
sysadmin@localhost:~/mybackups$
```
### 7.2.15 Step 15
To extract the ```zip``` archive, use the ```unzip``` command without any options. In this example we first need to delete the files that were created in the earlier tar example:
```
rm -r etc
unzip udev.zip
```
Your output should be similar to the following:
```
sysadmin@localhost:~/mybackups$ rm -r etc                                       
sysadmin@localhost:~/mybackups$ unzip udev.zip                                  
Archive:  udev.zip                                                              
   creating: etc/udev/                                                          
   creating: etc/udev/rules.d/                                                  
  inflating: etc/udev/rules.d/70-persistent-cd.rules                            
  inflating: etc/udev/rules.d/README                                            
   creating: etc/udev/hwdb.d/                                                   
  inflating: etc/udev/udev.conf                                                                                       
sysadmin@localhost:~/mybackups$
```
