# INRODUCTION TO SHELL SCRIPTING AND USER INPUT

Being familiar with the use of terminal from our experiences and previous projects, we could see that we carried out some tasks with certain commands which executed corresponding outputs.

Basically, the idea of shell scripting is to automate and execute repeatative tasks, for example, in a situation where we have to download a thousand different times from the web, this task can be executed using a script that will perform this repeatitive tasks.
Bash is a dialeect of shell syntax called the Bourne shell. Bash scripts are usually a series of commands saved in a text file with a .sh extension

## Shell Scripting Syntx Elements
##### - Variables:
Bash allows us to be able to declare variables. This variables can be assinged to values which can be strings, numbers, or arrays. We can always call these variables by putting a dollar sign ($) in front of the name of the variable whenever there is a need to use it. 
###### Assingning Value to a Variable and Retrieving Value from a Variable
Assingning variable to a value is done with an equality sign (=)

name="John" 

We can also retrieve this value by using the `echo` command

echo $name

<img width="342" alt="variable   echo" src="https://github.com/AndromedaIsComingg/Other-Projects/assets/140917780/7637a7be-e7ea-4e70-ad85-fde480459728">


##### - Control Flow:

