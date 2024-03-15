### Practical 1:  Introduction to Linux and command lines: A recap

•	Learning outcome from this exercise
a)	How to connect to remote server/virtual machine
b)	Basic linux commands for file and folder operations

•	How to connect to your virtual machines
I used azure lab (labs.azure.com) to create individual linux virtual machines. You already got an invitation from me to join virtual lab at labs.azure.com. Once you register, you will see your machine. This portal is to start/switch off your server outside the scheduled hour (1000-1600). However, process of connecting to a server is not automatic and you need to do it yourself when you need to do some work in the server. 

When you press registration link, it will take you labs.azure.com. Once you are done with registration, you will see a linux virtual machine in your home page (labs.azure.com). You cannot do anything until you set a password. Press “reset password” button (one row of 3 dots) to set a password. It will take ca. two minutes to finish password setting. Then you will see computer icon close to that row of 3 dots. Click start and wait until you get “running” there. Now press that icon to get popup window with ssh command line to connect your virtual machine. Copy that command line. 

•	Following steps will apply for Mac only:
Type terminal in Launchpad and press terminal. Select terminal and paste that command there and Press enter.  Type yes in next command (fingerprint question). Type password you set. You should be in now. 

•	For windows users only:
Option 1
If you have power terminal (PowerShell) in your windows (type PowerShell in search bar), then things are easy. Open the power terminal and paste the command line you copied from labs.azure.com, type password (you won’t see any anything, it is hidden as they are passwords!!!!). You are in. 

Option 2
Download and install MobaXterm from here: https://mobaxterm.mobatek.net/download-home-edition.html and download installer version. Unzip the downloaded files. Follow the instructions and finish the process, make sure you install the program in the same folder.  You should be able to see the interface after starting the MobaXterm-application (please follow the basic_usage_of_mobaXterm.pdf. 
Now you are in the server. Read the welcome message. 

We also need to install filezilla, a file transferring GUI system. Download copy of that from here: https://filezilla-project.org/download.php?type=client and connect it to the server together. 

•	History of terminal

Terminal is just a tool to connect commands with the machine, just like a keyboard and mouse.  Simple!!! You have already experienced how most of the linux machine look like: there is no graphical user interface (GUI) between you and the server. GUI do exist for personal machines. We use ‘commands’ to communicate with the server/virtual machine.

•	Basics of Linux command line

First, we will find out where (which directory/folder) are we right now in our machine. 
Run command: pwd (Print Working Directory).
Now you see two different things on the screen: 
a) some weird:  username@servers-network-name: ~ $
b) /home/YOURUSERNAME 

So, a) is called prompt, that is the way computer informing you that “I am ready to take your instructions”.

b) reply for the command you executed: pwd: It gives you current working directory (remember from part 1, R?).  Whatever command you execute will be outputted in relation to this directory. 

•	Navigation between the directories
We use a command called cd (Change Directory). 
cd  specify which directory you want to go 
Example:  cd .. (Take you one level up) or cd /. 

cd / will take you to the “root” directory. Yes, it is analogous to root from a Tree. All the other directories in the server are branching from this directory. 

You can also use ‘..’ more than once if you have to move up through multiple levels of parent directories:
cd ../..
pwd
The path we used means “starting from the working directory, move to the parent ‘/’ from that new location move to the parent again”.

•	Relative and absolute paths
Relative path: The place you end up depends on your current working directory.
 Try cd etc or cd mnt
Absolute path: no matter where you are (current folder) you will still reach to the folder you want to enter. 
Try, 
cd /
cd /etc 
Other way to reach a folder you want without step by step is simply is using the ‘tilde’ character (”~”) at the start of your path similarly means “starting from my home directory”.
Try cd ~

•	Creating folders and files
We should use mkdir command to create folder. 
mkdir –help or man mkdir
mkdir NAME_OF_A_FOLDER to create a folder. mkdir is make directory. 
mkdir is command and NAME_OF_A_FOLDER is called parameter.
mkdir NAME_OF_1_FOLDER NAME_OF_2_FOLDER NAME_OF_3_FOLDER (3 folders at a time)
mkdir -p NAME_OF_1_FOLDER/NAME_OF_2_FOLDER /NAME_OF_3_FOLDER
mkdir -p dir1/dir2/dir3 (what happens here and how it different from command just above)

•	Listing the content of a folder /directory
Use ls to list what is there. ls stands for list. 
Type: man ls to read the help

Try all these commands after reading the manual
mkdir --parents --verbose dir4/dir5
mkdir -p --verbose dir4/dir5
mkdir -p -v dir4/dir5
mkdir -pv dir4/dir5


You might be thinking why I used NAME_OF_A_FOLDER rather NAME OF A FOLDER. In this case we will create 4 different directories. 
Try yourself! mkdir NAME OF A FOLDER
Computer will treat space as separating parameter. If you want (I discourage using space) then you should use this option.

mkdir "folder 1"
mkdir 'folder 2'
mkdir folder\ 3
mkdir "folder 4" "folder 5"
mkdir -p "folder 6"/"folder 7"
ls

•	Creating a file
Stay in the folder you are in right now.  What we will do now is redirect the output of ls command to a file.
ls >ls.txt
How to open ls.txt if you are in a system which lacks graphical user interface?
Use cat filename. This is to open and read the content of a file. But you cannot do anything than seeing the content of the file. There are other tools like nano, to see and modify the content (feasible only with files with few content)

•	Now how to write a file from scratch?
Use echo command to write something and or redirect it to a file.
echo "This is a test" > test_1.txt
echo "This is a second test" > test_2.txt
or you can open an empty file and type the content and save: nano test1.txt and nano test2.txt

How to read multiple files together? Use cat again. cat is concatenate
cat test_1.txt test_2.txt 
cat test_1.txt test_2.txt >concatenated_file.txt
 If there is consistent pattern you can use wild card such as * and? .
Example:
cat test_* > combined.txt
cat t*>combined.txt
If you want to read a text file, then use less or more. Or I use nano. 
Try to read the file one or other way
Tips: 
1.	Don’t use spaces in the file name
2.	Don’t use capital letters in the naming: need to switch of caps lock every now and linux command are always in small letters
3.	Use names as sensible as possible so that it gives you lot more information.
4.	Don’t use closely related file names or files names which are not very different from each other. 
5.	Always use an extension to a file. Example: .txt, .csv, .tsv 

•	Moving and manipulating a file
Let’s move the file from current directory to another directory. 
We use a command called mv, which stands for move. One 

mv combined.txt dir1

Confirm the result by ls dir1. Or just run ls in the current directory. If it is not present in the current directory, then it is moved to dir1.

You can use mv command to move more than one element from a directory. Last parameter in the mv command will be the one which gets the other elements. 

If you want to bring back combined.txt to where it was before moving, then use mv dir1/combined.txt.

Now we will keep a copy of the file before we move that file anywhere else.
      cp combined.txt combined_copy.txt

mv command can be used as renaming tool like cp. But cp will keep a copy of the original file in the destination, while mv not.

•	Delete a file
 
Now will try most destructive command of all the linux commands: rm (stands for remove).
Now remove a file. rm combined_copy.txt
Remove a folder now. rmdir example_folder. 
Tips  

1.	Think twice before you run the command rm. 
2.	Be careful with using rm command in wild card setup.
3.	rm command doesn’t move the files to thrash/recycle bin. It simply deletes file from the system with no way to recover it (it is possible the big servers). 
4.	If you are unsure try to use -i with rm command to enable interactive mode, so that you have second chance to think before you say YES. 

•	Plumbing work
You want to know how many lines there in text file are. It is easy if you use a graphical interface utility (or a text editor which gives you line number, example nano). But you want to know the line number quickly, you need to use command line to figure that out. 

How many lines are there in combined.txt?
Use wc -l combined.txt. wc stands for word count. When you use -l it gives you total number of lines instead of just character count (when you use wc only)
Results will be displayed on screen. We call this standard output (STDOUT).

•	Piping
How many files are there in a folder? 
Test this using: ls | wc -l. Here I piped an output from a command called ls to another command wc -l. Here wc -l takes STDOUT of ls as INPUT (STDIN). 
When you have few lines, then use less. Example ls | less.
Result will be organised on a screen in text processor (also called pager). Use q to quit. 

If you want to know what a particular command does and how to use it. just type man COMMAND
Example:  man mv 
man cp
man wc 




•	How to do a multiple piping
Example: sort combined.txt | uniq | wc -l
Tell me what this above command will do? Use man to know what sort and uniq.
When you have a file with multiple columns, and you want to cut a particular column, then use cut. Use man cut.   If you want to find something from a file, then use grep. 
grep ‘somethingyouwantto’ filename.txt

Find and replace can be performed using sed.
sed 's/findword/replaceword/' file.txt

Type “linux cheat sheet” in the google you get 100s of list.  And try those commands

•	File permissions
In Linux everything is a file. Folders are files, files are files and external devices are files. All the files in linux system have file permissions. It says all about who can read and write and execute a file. Each file has different level of access restrictions.
If you do ls -lh in a folder, 
you see drwxrwxr-x on your screen. They tell you who have permission to use this folder and what purpose (reading, modifying/writing, executing).

 

Here are three types of access restrictions (from linux related webpages): 
Permission	Action	chmod option
read	(view) 	r or 4
write	(edit) 	w or 2
execute	(execute) 	x or 1


There are also three types of user restrictions: 
User	ls output
owner	-rwx------
group	----rwx---
other	-------rwx

•	Folder/Directory Permissions
Directories have directory permissions. The directory permissions restrict different actions than with files or device nodes. 
Permission	Action	chmod option
read	(view contents, i.e. ls command) 	r or 4
write	(create or remove files from dir) 	w or 2
execute	(cd into directory) 	x or 1
1.	read restricts or allows viewing the directories contents, i.e. ls command 
2.	write restricts or allows creating new files or deleting files in the directory. (Caution: write access for a directory allows deleting of files in the directory even if the user does not have write permissions for the file!) 
3.	execute restricts or allows changing into the directory, i.e. cd command

Look into your folder and say how these permissions are organized? 

Generally, owner of the file has permission to change the accessibility of file or folder. Another user who can override even the owner of the file is a ROOT user (su, sudo).  Briefly, root user is owner of the system. Root user is a super user (su) and executes commands as sudo. sudo is a safety net for super user not to commit any command without second thought. First user of the system is always a root. Then root can use discretion to empower other users to root level. Not all the users can become root user. Superuser power comes with super responsibilities. Super User has all the power in a system, even to destroy the system itself. 
If you are owner of the file or folder, you should use chmod to change the ownership/sharing/or to impart selective permission.
 Type chmod, you will get help. 
chmod {options} filename
Options	Definition
u 	owner 
g 	group 
o 	other 
a 	all (same as ugo) 
x 	execute 
w 	write 
r 	read 
+ 	add permission 
- 	remove permission 
= 	set permission

Or you can use bit numbers. 
First number related Owner, second number related group and 3rd number related to other users (not part of the group) 
  
(from google)

TO DO: 
TRY out the commands and their usage: ps, top, htop, zcat, unzip, gzip, history. Find out what they do.



•	Scripting
Now we probably know many things about how the Linux and command line work. Now we will go for a next level called scripting. You already know little bit about scripting from data science part. Scripting is nothing but automatization of commands /instructions you need to run every now and then. 

Scripting essentially uses shell, which is a microprocessor allows for an interactive or non-interactive command execution in combination with nano (my favorite text editor to create a new file containing set of instructions in a separate line. 

Terminal is input output environment (a mean to talk to computer)

Your terminal contains shell (an interface). A shell is a user interface for access to an operating system's services. 

Now we will write a very small script using bash as interpreter (which is default in any unix based system, there are also python, perl and so on). 

run: echo $SHELL

Write a small script: 

Open nano
Type all small commands such as date, cal, ls in separate lines and save it as test.sh. I am using .sh because I am using bash as interpreter of my commands.  

There is small script uploaded in the bioinformatics section of the canvas which is related to the taking backup of a folder. 

Variables
Variables are the essence of programming. Variables allow a programmer to store data, alter and reuse them throughout the script. 
Check welcome.sh script and backup.sh script. 

References for this exercise:
Some part of this exercise comes from linux tutorials published by Linux (ubuntu) people. All resources in their tutorials are open source.
