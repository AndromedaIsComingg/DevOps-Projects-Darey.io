# INRODUCTION TO SHELL SCRIPTING AND USER INPUT

Being familiar with the use of terminal from our experiences and previous projects, we can see that we carried out some tasks with certain commands which executed corresponding outputs.

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
The flow of execution of a script can be controlled in bash. Statements like if-else, for loops and while loops can be used to make decision, iterate over lists and strings and execute differrent commands.

##### Using bash to execute an if-else statement.
We will begin this by creating a bash file named `if-else.sh` inside which we will input the following lines of code using any prefered text editor. For this we will be using the vi editor. Which is a script meant to check if a number is positive, negative, or zero.

```bash
#!/bin/bash

# Example script to check if a number is positive, negative, or zero

read -p "Enter a number: " num

if [ $num -gt 0 ]; then
    echo "The number is positive."
elif [ $num -lt 0 ]; then
    echo "The number is negative."
else
    echo "The number is zero."
fi
```
We will use the following command to write and exit the vi editor. `:wq!`

<img width="376" alt="touch vi if-else" src="https://github.com/AndromedaIsComingg/Other-Projects/assets/140917780/729d6a29-5767-483a-9618-5d695ccaff14">


<img width="500" alt="vi if-else" src="https://github.com/AndromedaIsComingg/Other-Projects/assets/140917780/133541eb-6d1c-4ead-bda2-c479cafcdc45">

Now that we have our file created, we will grant the file execution permission in order the make the file executable
we will be doing this with the command `chmod +x if-else.sh` before we run the file.

<img width="404" alt="chmod if-else" src="https://github.com/AndromedaIsComingg/Other-Projects/assets/140917780/c66fd936-b1a4-43f1-a994-f6983e9486ec">

Now that we have made the file executable, we are going to run it using any of the following methods.


By putting `bash` in front of the file name or `./` that is, `bash if-else.sh` or `./if-else.sh` after which we will input a number greater than zero, less than zero and also zero to test the script.

<img width="351" alt="running if-else" src="https://github.com/AndromedaIsComingg/Other-Projects/assets/140917780/55cac7a3-6529-40f6-8168-1efe9e5162fe">

##### Iterating through a list using a for loop
We will begin this by creating a bash file named `for-loop.sh` inside which we will input the following lines of code using any prefered text editor. For this we will be using the vi editor. Which is a script meant to display number 1 to 5 using a for loop.

```bash
#!/bin/bash

# Example script to print numbers from 1 to 5 using a for loop

for (( i=1; i<=5; i++ ))
do
    echo $i
done
```

<img width="375" alt="touch for-loop" src="https://github.com/AndromedaIsComingg/Other-Projects/assets/140917780/7a7e0ef0-4fd6-4c55-8d94-4efe758a10c0">

We will use the following command to write and exit the vi editor. `:wq!`

<img width="472" alt="vi for-loop" src="https://github.com/AndromedaIsComingg/Other-Projects/assets/140917780/37cbdadc-310c-40d6-8177-73e1779cf251">


Now using the same method as above to make the file executable, we will grant the file an execution privilage and then run the script file using same method as above.

<img width="400" alt="run+chmod for-loop" src="https://github.com/AndromedaIsComingg/Other-Projects/assets/140917780/3f1339bd-bad8-4599-8f16-3d7bec0994eb">








