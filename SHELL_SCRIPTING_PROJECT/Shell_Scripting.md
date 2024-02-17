# Introduction to Shell Scripting and User Input
## Introduction to Shell Scripting and User Input
In our git course, we have been writing commands on the terminal and getting corresponding output. The commands are
instructions to the computer to carryout certain task.

For instance, when we want to clone a git repo, we type the command `git clone` and pass in the link to the repository.
In less than no time we see the repo downloaded into our local machine.

Lets say you are given a task to clone 1000 repositories. Yes you can type the `git clone` command 1000 times. That
gets the job done Someone with not so great patience maybe unable to complete the task.

This is where shell scripting commes in. Shell scripting helps you automate repetitive task. We can simply write a script
that does the job of cloning the 1000 repositories. We call it once and the job is done. We have the advantage of using it
agalin whenever we are signed same task.

Bash scripts are essentially a series of comnmands and instructions that are executed sequentially in a shell. You can
create a shell script by saving a collection of commands in a text file with a .sh extension. These scripts can be executed
directly from the command line or called from other scripts.
## Shell Scripting Syntax Elements
1. Variables: Bash allows you to define and work with variables. Variables can store data of various types such as numbers, strings and arrays. You can assign values to variable using the = operator, and access their values using the variable name preceeded by a $ sign.

Example: Assigning value to a variable:

`name-"John"`
![Images](SHELL_SCRIPT_IMAGES/1.PNG)


Example: Retrieving value from a variable:

`echo $name`
![Images](SHELL_SCRIPT_IMAGES/2.PNG)

2. Control Flow: Bash provides control flow statements like if-else, for loops, while loops, and case statements to
control the flow of execution in your scripts. These statements allow you to make decisions, iterate over lists,and
execute different commands based on conditions.
Example: Using if-else to execute script based on a conditions