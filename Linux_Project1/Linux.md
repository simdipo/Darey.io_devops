# Linux Practice Project
## File Manipulation 
### 1. sudo command
This is a superuser do command that enable user to perform a task that requires administrative or root permissions.
![Sudo Apt Upgrade](Linux_Images/Sudo.PNG)
### 2. pwd command
This simply means a present working directory, this makes us to know the directories we are working from.
![Print working directory](Linux_Images/PWD.PNG)
### 3. cd command
This command is used to change directory, that is to navigate fom one directories to another, just like move from one folder to another.
![change directory](Linux_Images/CD.PNG)
![change directory](Linux_Images/CDCD.PNG)
### 4. ls command
Ls command is simply usd to list directories or files
![List directory](Linux_Images/LS.PNG)
![List directory](Linux_Images/LS2.PNG)
### 5. cat command
Cat command is used to write or read file contents to the standard output.
![Cat directory](Linux_Images/CAT.png)
### 6. cp command
Cp command is used to copy files or folder from one source to another.
![Copy directory](Linux_Images/CP.png)
### 7 mv command
mv command: 
The primary use of the mv command is to move and rename files and directories
![Move directory](Linux_Images/MV.PNG)
### 8. mkdir command:
Use the mkdir command to create one or multiple directories at once and set permissions for each of them.
![Make directory](Linux_Images/mkdir.png)
### 9. rmdir command:
To permanently delete an empty directory, use the rmdir command.
![remove directory directory](Linux_Images/rmdir.png)
### 10. rm command:
The rm command is-used to delete files within a directory.
![Remove file directory](Linux_Images/rm.png)
### 11. touch command:
The touch command allows you to create an empty file or generate and modify a timstamp in a linux command line.
![Touch directory](Linux_Images/touch.PNG)
### 12. locate command:
The locate command can find a file in the database system.
![Locate directory](Linux_Images/locate.PNG)
### 13. find command
The find command to search for files within a specific directory and perform subsequent operations.
![Find directory](Linux_Images/find.png)
### 14. grep command:
Another basic Linux command on the list is grep or global regular expression print. It lets you find a word by searching
through all the texts in a specific file.
![Grep directory](Linux_Images/grep.png)
### 15. df command:
The df command to report the system's disk spare usage, shown in percentage and kilobyte (KB).
![DF directory](Linux_Images/df.png)
### 16. du command:
du command is used to check how much space a file or a directory takes up.
![Du directory](Linux_Images/du.png)
### 17.head command:
The head command allows you to view the first ten lines of a text. Adding an option lets you change the number of lines shown below:

![Head directory](Linux_Images/head.png)
### 18. tail command:
The tail command displays the last ten lines of a file. It allows users to check whether a file has new data or to read error messages.

![tail directory](Linux_Images/tail.png)
### 19. diff command:
Short for difference, the diff command compares two contents of a file line by line. After analyzing them, it will display
the parts that do not match.
![diff directory](Linux_Images/diff.png)

### 20. tar command:
The tar command archives multiple files into a TAR file - a common Linux format similar to ZIP, with optional compression.
![tar directory](Linux_Images/tar.png)
## Introduction to Linux and Basic Commands
Linux is a family of open-source Unix operating systems based on the Linux Kernel. They include Ubuntu, Fedora,
Debian, openSUSE, and Red Hat. Using Linux to manage a Virtual Private Server (VPS) is common practice.
When operating Linux, you need to use a shell - a program that gives you access to the operating system's services. Most
Linux distributions use a graphical user interface (GUI), making them beginner-friendly.

However, we recommend utilizing the command-line interface (CLI) because it's quicker and offers more control. Tasks
that require multiple steps on the GUI can be done in a matter of seconds by entering commands into the CLI.
So if you want to use Linux, learning the common utilities or commands will go a long way.

## What Is a Linux Command?
A Linux command is a program or utility that runs on the CLI - a console that interacts with the system via texts and
processes. It's.similar to the Command Prompt application in Windows.
Linux commands are executed on Terminal by pressing Enter at the end of the line. You can run commands to perform
various tasks, from package installation to user management and file manipulation.

## File Permissions and Ownership
### 21. chmod command:
chmod is a common command that modifies a file or directory's read, write, and execute permissions. In Linux, each file is
associated with three user classes - owner, group member, and others.
![chmod directory](Linux_Images/chmod.png)

### 22. chown command:
The chown command lets you change the ownership of a file, directory, or symbolic link to a specified username.
![chown directory](Linux_Images/chown.png)

#### 23. jobs command:
A job is a process that the shell starts. The jobs command will display all the running processes along with their statuses.
Remember that this command is only available in csh, bash, tcsh, and ksh shells.
![jobs directory](Linux_Images/jobs.png)
### 24. kill command:
Use the kill command to terminate an unresponsive program manually. It will signal misbehaving applications and
instruct them to close their processes.
![kill directory](Linux_Images/kill.png)

### 25.ping command:
The ping command is one of the most used basic Linux commands for checking whether a network or a server is
reachable. In addition, it is used to troubleshoot various connectivity issues.
![ping directory](Linux_Images/ping.png)
### 26. wget command:
The Linux command line lets you download files from the internet using the wget command. It works in the background
without hindering other running processes.
![wget directory](Linux_Images/wget.png)
### 27. uname command:
The uname or unix name.command will print detailed information about your Linux system and hardware. 
![uname directory](Linux_Images/uname.png)
### 29.history command:
With history, the system will list up to 500 previously executed commands, allowing you to reuse them without re-
entering. Keep in mind that only users with sudo privileges can execute this command. How this utility runs also depends
on which Linux shell you use
![history directory](Linux_Images/history.png)
### 30. man command:
The man command provides a user manuald of any commands or utilitigs.
![man directory](Linux_Images/man.png)
### 31. echo command:
The echo command is a built-in utility that displays a line of text or string using thé standard output. 
![echo directory](Linux_Images/echo.png)
### 32. zip, unzip commands:
Use the zip command to compress your files into a ZIP file, a universal format commonly used on Linux. It can
automatically choose the best compression ratio.
![zip, unzip directory](Linux_Images/zip.png)
### 33. hostname command:
Run the hostname command to know the system's hostname. You can execute it with or without an option.
![hostname directory](Linux_Images/hostname.png)
### 34. useradd, userdel commands:
Linux is a multi-user system, meaning more than one'person can use it simultaneously. useradd is used to create
account, while the passwd command allows you to add a password. Only those with root privileges or sudo can
useradd command.
![useradd directory](Linux_Images/useradd.png)
### 35. apt-get command:
apt-get is a command line tool for handling Advanced Package Tool (APT) libraries in Linux. It lets you retrieve
information and bundles from authenticated sources to manage, update, remove, and install software and its
dependencies.
Running the apt-get command requires you
![apt-get directory](Linux_Images/apt-get.png)
### 36. nano, vi, jed commands:
Linux allows users to edit and manage files via a text editor, such as hano, Vi, or jed. nano and vid come with the opera
system, while jed has to be installed.
The nano command denotes keywords and can work with most languages. To use it, enter the following 
![editor directory](Linux_Images/editor.png)
### 37. alias, unalias commands:
alias allows you to create a shortcut with the same functionality as a command, file name, or text. When exe
instructs the shellto replace one string with another.
![alias directory](Linux_Images/alias.png)
### 38. su command:
The switch user or su command allows you to run a program as a different user. It changes the administrative ac
the current log-in session. This command is especially beneficial for accessing the system through SSH or using t
display manager when the root user is unavailable
![su directory](Linux_Images/su.png)
### 39. htop command:
The htop command is an inter active program that monitors system resources and server processes in real time. It
available on most Linux distributions, and you can install it using the default package manager.
![htop directory](Linux_Images/htop.png)
### 40. ps command:
The process status or ps command produces a snapshot of all running processes in your system. 
![ps directory](Linux_Images/ps.png)


