# SHELL SCRIPTING HANDS-ON PROJECT

## Inroduction to Shell Scripting and User Input

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


##### - Command Substitution:
This function allows us the capture the output of a command and used it as a value still within the script.

This is done using the backtick or the $() syntax.

Here is an example using the backtick ``` current_date=`date +%Y-%m-%d` ```

and here using $() ```current_date=$(date +%Y-%m-%d)```

For both cases, the command at the right hand side of the equality sign was substituted with the variable `current_date` such that it will be usable within the same script.

<img width="471" alt="command sub" src="https://github.com/AndromedaIsComingg/Other-Projects/assets/140917780/b55c84ee-a795-430a-9209-945231ceba5b">


##### - Input and Output:
Bash provides different ways of taking user input and displaying output. User input can be taken using the `read` command and displayed using the `echo` command. These input and output can be redirected using operators like, >(output to a file)>, >(input from a file)>, |(pipe the output of a command as input to another).

###### We will run the following commands to :
Accept user input: 
`echo "Enter your name:"` (for this we will create a bash file named `name.sh` and edit with the vi editor)
`read name`

Output Text to Terminal:
`echo "Hello World"` (this is also be executed in the same bash file named `name.sh`)


<img width="195" alt="echo name" src="https://github.com/AndromedaIsComingg/Other-Projects/assets/140917780/d63cbb18-001d-48ac-87b0-0fea4cfd7a0a">


<img width="361" alt="name run" src="https://github.com/AndromedaIsComingg/Other-Projects/assets/140917780/ba00adb1-84e5-42b4-96f7-5c519f913ae0">


Output the result of a command into a file:
`echo "hello world" > index.txt`
Then we will read the text file with the `cat` command for confirmation
`cat index.txt`

Pass the content of a file as input to a command
`grep "pattern" < index.txt` (using the previously created index.txt file)

Pass the result of a command as input to another command
`echo "hello world" | grep "pattern"`

<img width="497" alt="grep run" src="https://github.com/AndromedaIsComingg/Other-Projects/assets/140917780/45687855-d1dd-4844-ae82-6f2922871b20">


##### - Functions:
A function or subroutine is a sequence of program instructions that performs a specific task, packaged as a unit. This unit can then be used in programs wherever that particular task should be performed. Bash allows us to declare a function by using the function keyword or by declaring the function name followed by parentheses.

For example we will be writing a function to greet a user using the code below by creating a shell file named `greet.sh`

```bash
#!/bin/bash

# Define a function to greet the user
greet() {
    echo "Hello, $1! Nice to meet you."
}

# Call the greet function and pass the name as an argument
greet "John"
```

<img width="485" alt="vi john" src="https://github.com/AndromedaIsComingg/Other-Projects/assets/140917780/54c4adde-a9b1-4fb7-b554-862030d49880">


We will use the following command to write and exit the vi editor then run the script. `:wq!`

<img width="373" alt="greet john" src="https://github.com/AndromedaIsComingg/Other-Projects/assets/140917780/c2f2ee19-7bc7-40f3-bb46-6d2626d04efd">


## Writing a Shell Script
- From terminal we are going to create a folder for this called "shell-scripting" where we will keep the scripts for the following operations. usinf the command `mkdir shell-scripting`
- Then we will create a file called user-input with the command `touch user-input.sh`
- In this file, using the vi editor we will paste the following code which is meant to take the name of a user and     display a greeting.

  <img width="409" alt="shell 2nd fold" src="https://github.com/AndromedaIsComingg/Other-Projects/assets/140917780/473610fa-155f-4ff5-9f81-1dd1d2b12359">


```bash
#!/bin/bash

# Prompt the user for their name
echo "Enter your name:"
read name

# Display a greeting with the entered name
echo "Hello, $name! Nice to meet you."

```
- We will use the following command to write and exit the vi editor. `:wq!`


- Now that we have our file created, we will grant the file execution permission in order the make the file            executable
  we will be doing this with the command `chmod +x user-input.sh` before we run the file.


- Now that we have made the file executable, we are going to run it using any of the following methods.


  By putting `bash` in front of the file name or `./` that is, `bash user-input.sh` or `./user-input.sh`


<img width="307" alt="vi user input 2" src="https://github.com/AndromedaIsComingg/Other-Projects/assets/140917780/87688c14-cd0c-427d-b783-de70d584839f">


<img width="406" alt="run name input" src="https://github.com/AndromedaIsComingg/Other-Projects/assets/140917780/a7964a9e-4eb3-480a-b60d-1127fc4506b7">


## Directory Manipulation and Navigation
To perform this we will create a file named `navigating-linux-filesystem.sh` using the `touch` command
Then using a text editor, we will be using vi, we will paste the following code which is mean to perform the following operations
-  Display current directory
-  Create a new directory
-  Change to the new directory
-  Create some files
-  List the files in the current directory
-  Move one level up
-  Remove the new directory and its contents
-  List the files in the current directory again

```bash
#!/bin/bash

# Display current directory
echo "Current directory: $PWD"

# Create a new directory
echo "Creating a new directory..."
mkdir my_directory
echo "New directory created."

# Change to the new directory
echo "Changing to the new directory..."
cd my_directory
echo "Current directory: $PWD"

# Create some files
echo "Creating files..."
touch file1.txt
touch file2.txt
echo "Files created."

# List the files in the current directory
echo "Files in the current directory:"
ls

# Move one level up
echo "Moving one level up..."
cd ..
echo "Current directory: $PWD"

# Remove the new directory and its contents
echo "Removing the new directory..."
rm -rf my_directory
echo "Directory removed."

# List the files in the current directory again
echo "Files in the current directory:"
ls
```

- We will use the following command to write and exit the vi editor. `:wq!`


- Now that we have our file created, we will grant the file execution permission in order the make the file            executable
  we will be doing this with the command `chmod +x navigating-linux-filesystem.sh` before we run the file.


- Now that we have made the file executable, we are going to run it using any of the following methods.


  By putting `bash` in front of the file name or `./` that is, `bash navigating-linux-filesystem.sh` or `./navigating-linux-filesystem.sh`

#####                            Entering Commands
<img width="527" alt="command opp" src="https://github.com/AndromedaIsComingg/Other-Projects/assets/140917780/51210f92-d235-4edc-8301-9f218a06c7ba">


#####                             vi Editor
<img width="339" alt="vi operations" src="https://github.com/AndromedaIsComingg/Other-Projects/assets/140917780/b431dbf6-ede9-4dd9-b12f-c944a9dfbeb2">

#####                         Running the Script
<img width="540" alt="run operations" src="https://github.com/AndromedaIsComingg/Other-Projects/assets/140917780/fc9da9c6-4782-478c-bd9d-f06ab6225bde">


## File Operations and Sorting
In this operation we will create a shell script that will perform some file operations and sorting.
The file name will be `sorting.sh` and it will execute the following operations when we run it.
- Create three files, file1.txt, file2.txt, file3.txt
- Display the files in their current order
- Sort the files alphabetically
- Display the sorted files
- Remove the original files
- Rename the sorted file to a more descriptive name
- Display the final sorted file

```bash
#!/bin/bash

# Create three files
echo "Creating files..."
echo "This is file3." > file3.txt
echo "This is file1." > file1.txt
echo "This is file2." > file2.txt
echo "Files created."

# Display the files in their current order
echo "Files in their current order:"
ls

# Sort the files alphabetically
echo "Sorting files alphabetically..."
ls | sort > sorted_files.txt
echo "Files sorted."

# Display the sorted files
echo "Sorted files:"
cat sorted_files.txt

# Remove the original files
echo "Removing original files..."
rm file1.txt file2.txt file3.txt
echo "Original files removed."

# Rename the sorted file to a more descriptive name
echo "Renaming sorted file..."
mv sorted_files.txt sorted_files_sorted_alphabetically.txt
echo "File renamed."

# Display the final sorted file
echo "Final sorted file:"
cat sorted_files_sorted_alphabetically.txt
```
- We will use the following command to write and exit the vi editor. `:wq!`


- Now that we have our file created, we will grant the file execution permission in order the make the file            executable
  we will be doing this with the command `chmod +x sorting.sh` before we run the file.


- Now that we have made the file executable, we are going to run it using any of the following methods.


  By putting `bash` in front of the file name or `./` that is, `bash sorting.sh` or `./sorting.sh`

#####                            Entering Commands
<img width="383" alt="command sort" src="https://github.com/AndromedaIsComingg/Other-Projects/assets/140917780/ba36d91b-9d37-43cf-a206-38f60f262850">



#####                             vi Editor
<img width="428" alt="vi sorting" src="https://github.com/AndromedaIsComingg/Other-Projects/assets/140917780/8b287bc4-1290-42ca-8518-62288ce86a58">


#####                         Running the Script
<img width="983" alt="run sort" src="https://github.com/AndromedaIsComingg/Other-Projects/assets/140917780/532ed0ff-8db5-4640-aa17-22a415566dc8">


## Working with numbers and calculations
In this operation we will create a shell script that will perform some arithemetic operations.
The file name will be `calculations.sh` and it will execute the following operations when we run it.
- Define two variables with numeric values, num1 and num2 (num1 will be assigned to a value of 10 and num2 will be     assigned to a value of 5
- Perform basic arithmetic operations (addition, substraction, multiplication, division and modulus)
- Display the results
- Perform some more complex calculations
- Display the results

```bash
#!/bin/bash

# Define two variables with numeric values
num1=10
num2=5

# Perform basic arithmetic operations
sum=$((num1 + num2))
difference=$((num1 - num2))
product=$((num1 * num2))
quotient=$((num1 / num2))
remainder=$((num1 % num2))

# Display the results
echo "Number 1: $num1"
echo "Number 2: $num2"
echo "Sum: $sum"
echo "Difference: $difference"
echo "Product: $product"
echo "Quotient: $quotient"
echo "Remainder: $remainder"

# Perform some more complex calculations
power_of_2=$((num1 ** 2))
square_root=$(awk "BEGIN{ sqrt=$num2; print sqrt }")

# Display the results
echo "Number 1 raised to the power of 2: $power_of_2"
echo "Square root of number 2: $square_root"
```

- We will use the following command to write and exit the vi editor. `:wq!`


- Now that we have our file created, we will grant the file execution permission in order the make the file            executable
  we will be doing this with the command `chmod +x calculations.sh` before we run the file.


- Now that we have made the file executable, we are going to run it using any of the following methods.


  By putting `bash` in front of the file name or `./` that is, `bash calculations.sh` or `./calculations.sh`

#####                            Entering Commands
<img width="420" alt="command calculatns" src="https://github.com/AndromedaIsComingg/Other-Projects/assets/140917780/90e21e8c-7ec4-49ea-a989-531901d93e09">


#####                             vi Editor
<img width="385" alt="vi calculations" src="https://github.com/AndromedaIsComingg/Other-Projects/assets/140917780/fb949e45-c30a-473e-89af-a02c8b0d3157">


#####                         Running the Script
<img width="452" alt="run calculations" src="https://github.com/AndromedaIsComingg/Other-Projects/assets/140917780/f19de554-844d-4ca1-ac98-f3cdfe52a802">


## File Backup and Timestamping
Here we will be creating a script the will be focused on file backup and timestamp.

we will be creating a shell script named `backup.sh` that will perform the following operations.
- Define the source directory and backup directory
- Create a timestamp with the current date and time
- Create a backup directory with the timestamp
- Create the backup directory
- Copy all files from the source directory to the backup directory
- Display a message indicating the backup process is complete

```bash
#!/bin/bash

# Define the source directory and backup directory
source_dir="/path/to/source_directory"
backup_dir="/path/to/backup_directory"

# Create a timestamp with the current date and time
timestamp=$(date +"%Y%m%d%H%M%S")

# Create a backup directory with the timestamp
backup_dir_with_timestamp="$backup_dir/backup_$timestamp"

# Create the backup directory
mkdir -p "$backup_dir_with_timestamp"

# Copy all files from the source directory to the backup directory
cp -r "$source_dir"/* "$backup_dir_with_timestamp"

# Display a message indicating the backup process is complete
echo "Backup completed. Files copied to: $backup_dir_with_timestamp"
```

- We will use the following command to write and exit the vi editor. `:wq!`


- Now that we have our file created, we will grant the file execution permission in order the make the file            executable
  we will be doing this with the command `chmod +x backup.sh` before we run the file.


- Now that we have made the file executable, we are going to run it using any of the following methods.


  By putting `bash` in front of the file name or `./` that is, `bash backup.sh` or `./backup.sh`

#####                            Entering Commands
<img width="397" alt="command timestamp" src="https://github.com/AndromedaIsComingg/Other-Projects/assets/140917780/d647c806-d0b9-4e1a-a1df-c47b6413f9f4">


#####                             vi Editor
<img width="497" alt="vi timestamp" src="https://github.com/AndromedaIsComingg/Other-Projects/assets/140917780/a0794816-de0c-4309-8653-001fd5e74ce0">



#####                         Running the Script
<img width="989" alt="run timestamp" src="https://github.com/AndromedaIsComingg/Other-Projects/assets/140917780/ce33bc3a-cb8a-4fc0-8ecd-9414f859c3dc">


Hurray!!!! Now we have been properly and practically introduced to shell scripting, taking user input and displaying output, directory manipulation and navigation, file operations and sorting, working with numbers and calculatiions, file backup and timestamping.

---------------------------------![Alt Text](https://cssbud.com/wp-content/uploads/2021/05/thanks-for-your-time.gif)---------------------------------------------


