# LinuxPracticeProject
## 1. Sudo Command
Short for "Super User Do", a command that gives you an access to administrative or root permissions.

As shown below, it was used to run apt update with requires a root permission.


<img width="456" alt="1  sudo apt update" src="https://github.com/AndromedaIsComingg/LinuxPracticeProject/assets/140917780/57a452f5-0a7a-4663-a650-c565fce6a8cb">

## 2. pwd Command
Short for "Present working directory", by simply entering pwd, terminal returns the full current working path as seen below.
<img width="176" alt="2  pwd" src="https://github.com/AndromedaIsComingg/LinuxPracticeProject/assets/140917780/e94332ea-41df-42c9-be5c-7e2be0437e1e">

## 3. cd Command
Short for "Change Directory", used to navigate through linux files and directories.
<img width="448" alt="3  cd command" src="https://github.com/AndromedaIsComingg/LinuxPracticeProject/assets/140917780/1af59022-0cbb-4c06-b89a-28cd9c7a6bb5">

## 4. ls Command
Used to list the files in a directory. It can also be used along side flags as seen below.
<img width="982" alt="4  ls" src="https://github.com/AndromedaIsComingg/LinuxPracticeProject/assets/140917780/83eb646e-6ad5-412e-b4cd-fdb04823c26d">

## 5. cat Command
Short for "Concatenate", used to list, write, and combine file content to its standard output.

Two text documents(test and test2) were read and concatenated to test3 as seen below.
<img width="1036" alt="5  cat command" src="https://github.com/AndromedaIsComingg/LinuxPracticeProject/assets/140917780/2f82d4fa-bbd4-4c80-8d15-042868c37a38">

## 6. cp Command
This command is used to cop files or directories and their content.

As seen below, where the file "test3" is copied to a new directory, the content of the file "test" is copied to the file "test2" and the whole directory "new-directory" was copied to another directory "new-directory2"
<img width="497" alt="cp command" src="https://github.com/AndromedaIsComingg/LinuxPracticeProject/assets/140917780/52d4f68b-0f0d-4493-a1e8-1ae00d56c2fb">

## 7. mv Command
The mv command is primarily used to move and rename files and directories

The file "test3" was moved from the current directory to a new directory called "new-directory", also the file "test2 was renamed to "test3".
<img width="399" alt="mv command" src="https://github.com/AndromedaIsComingg/LinuxPracticeProject/assets/140917780/b1efbc93-0544-45b9-8500-1a8e9846c185">

## 8. mkdir Command
This command is used to make one or more directories at once and also to st permissions for each of them.

As shown below, we created a directory "music" and went futher to create another directory "songs" inside the "music" directory
<img width="785" alt="8  mkdir  command" src="https://github.com/AndromedaIsComingg/LinuxPracticeProject/assets/140917780/2d381401-dab9-4f20-ab77-1f0015bae0f9">

## 9. rmdir Command
The rmdir command is used to permanently delete an empty directory so long as the useer has sudo privilages to the parent directory.

As shown below, the folder "songs" was permanently deleted from the "music" folder.

<img width="366" alt="9  rmdir command" src="https://github.com/AndromedaIsComingg/LinuxPracticeProject/assets/140917780/a9ac02bb-5be2-4efe-aa00-a42de51af868">

## 10. rm Command
This command is used to delete files within a directory so long as the user has the write permission.

As shown below, the file "test file" was deleted from the containing folder.
<img width="789" alt="10  rm command" src="https://github.com/AndromedaIsComingg/LinuxPracticeProject/assets/140917780/e13c2ac2-5a89-4a38-b2ef-2dce0173e8e1">

## 11. touch Command
The touch command allows you to create an empty file or generate and modify a timestamp in the linux command line.

The web file sqlite_command.sh was created
<img width="817" alt="11  touch command" src="https://github.com/AndromedaIsComingg/LinuxPracticeProject/assets/140917780/0d52e04c-fb0c-4d0a-9ca0-311bdae13c5f">

## 12. locate Command
The locate command is used to find a file in a database system. The -i argument is used turn of case sensitivity in case of uncertainty and asterisk(*) is used if we need to search for more than one keyword.
<img width="1043" alt="12  locate command" src="https://github.com/AndromedaIsComingg/LinuxPracticeProject/assets/140917780/05a41b8e-7064-4dba-852e-3914b64361a5">

## 13. find Command
Used to search for file within a specified directory.

it was used to search for the the file "test3" in the directory as shown below.

<img width="318" alt="13  find commanr" src="https://github.com/AndromedaIsComingg/LinuxPracticeProject/assets/140917780/84b8ce02-a62f-48f7-9a57-4f23a8f78efb">

## 14. grep Command
Short for "global regular expression print", used to find a word by searching through all the texts in a specified file.

The word "test" was searched for in the file "test3"

<img width="394" alt="14  grep command" src="https://github.com/AndromedaIsComingg/LinuxPracticeProject/assets/140917780/7c0e8e2f-5a29-4f4d-85db-6107349a1d0f">

## 15. df Command
Used with flags, df -h is used to report the system's disk space usage, shown in percentage and kilobyte.

df -m displays information on the file system usage in MBs

<img width="719" alt="15  df command" src="https://github.com/AndromedaIsComingg/LinuxPracticeProject/assets/140917780/baedf9dc-0e2f-4e1a-aecd-36720f8fdaf1">

## 16. du Command
Used to check how much space a file or directory takes up, and can also be combined with flags like

-s shows the total size of the specified folder

-m provides file and folder information in MB

-h shows the last modification dates of the displayed files and folder.

<img width="283" alt="du 2" src="https://github.com/AndromedaIsComingg/LinuxPracticeProject/assets/140917780/1ab7b68d-dd05-4ac9-87a9-4c277e7e7070">

## 17. head Command
This command allows you to view the first ten lines of a text, and adding a command changes the number of lines.

cat command was used to view the full text lines.

<img width="351" alt="17  head command" src="https://github.com/AndromedaIsComingg/LinuxPracticeProject/assets/140917780/4eec3da7-e1d4-4e45-9ec5-01407abe24e1">

## 18. tail Command
This command allows you to view the lastt ten lines of a text, and adding a command changes the number of lines.

cat command was used to view the full text lines.

<img width="366" alt="tail command" src="https://github.com/AndromedaIsComingg/LinuxPracticeProject/assets/140917780/0d790b37-f117-46f5-ab1b-61244027b8cf">

## 19. diff Command

This command compares two content of a file and displays the difference after analysing.

It was used to analyze the difference betwween the files "test" and "test2"

<img width="487" alt="19  diff command" src="https://github.com/AndromedaIsComingg/LinuxPracticeProject/assets/140917780/89219c32-5f07-4689-bfa6-75c8cd07209c">

## 20. tar Command
The tar command add multiple files into a single .tar file. It also has options like

List:    tar -tf <archive-filename>
Extract: tar -xf <archive-filename>
Create:  tar -cf <archive-filename> [filenames...]
Help:    tar --help

As seen below, a single file called "newachive" was created combining the files "test" and "test2" and listed the files in the new archive file

<img width="473" alt="20  tar command" src="https://github.com/AndromedaIsComingg/LinuxPracticeProject/assets/140917780/9dc04e8d-73c0-4102-ae8f-83bb7e6023bd">

## 21. chmod Command
This command modifies a file directory's read, write, and execute permissions.

For example, to allow other members have access to the file test3, we change the permission type with the numeric value 777 as seen below.

<img width="352" alt="21  chmod command" src="https://github.com/AndromedaIsComingg/LinuxPracticeProject/assets/140917780/4ef82456-0d03-44e5-88c1-119356b1ed3f">

## 22. chown Command
This helps to change the ownership of a file, directory or symbolic link to a specified username.

This changed the ownership of the "file test3" to the user "Andromeda"

<img width="392" alt="22  chown command" src="https://github.com/AndromedaIsComingg/LinuxPracticeProject/assets/140917780/4c795d54-a580-42e0-8163-7257c4179395">

## 23. jobs Command
This command displays all running processes with their statuses

<img width="205" alt="23  jobs command" src="https://github.com/AndromedaIsComingg/LinuxPracticeProject/assets/140917780/89153906-4230-437c-bcdb-9af2dd6b6935">

## 24. kill Command
This commnad is used to terminate an unresponsive program manually


To kill a program, you must know the process identification number(PID) which can be listed with the command ps ux

Then the following syntax is used kill [signal_option] pid

for example if the option is SIGKILL, the syntax becomes kill SIGKILL 63773
<img width="577" alt="24  kill command" src="https://github.com/AndromedaIsComingg/LinuxPracticeProject/assets/140917780/ee5b8e24-5dad-460c-8352-6de906314f05">

## 25. ping Command
The ping command is used to check whether a network or server is reachable, it is also used to trouble various connectivity issues.

we can check if we can connect to Google.com and also check the response time as seen below.
<img width="462" alt="25  ping command" src="https://github.com/AndromedaIsComingg/LinuxPracticeProject/assets/140917780/3c6163b4-dfc3-409d-b91b-ff1c94eb61e1">

## 26. wget Command
This command works in the background to download files from the internet.

For example, enter the following command to download the lastest version of wordpress. wget https://wordpress.org/latest.zip

The files will be downloaded as a zipped file in the current directory.

<img width="1265" alt="26  wiget command linux" src="https://github.com/AndromedaIsComingg/LinuxPracticeProject/assets/140917780/3e2cd425-3137-45ac-8687-10d880611eea">

## 27. uname Command
This command prints detailed information about the system information

the syntax is uname [option]

while the options include
-a prints all system information
-s prints kernel name
-n prints system node's hostname
<img width="999" alt="26  uname command" src="https://github.com/AndromedaIsComingg/LinuxPracticeProject/assets/140917780/7019d933-d221-4ad6-93ba-432ae6e45634">


## 28. top Command
This displays all the running processes and a dynamic realtime view of the current system. 

It sums up resources utilization from CPU to memory usage.

<img width="1280" alt="28  top command" src="https://github.com/AndromedaIsComingg/LinuxPracticeProject/assets/140917780/eca84b8f-1b9d-4a55-9abe-cc6a74e2dc4d">

## 29. history Command
With this command, the system will list upto 500 previously excecuted commands, enabling them to be reused withou re-entering them.

Only users with sudo privilages can execute this.

<img width="370" alt="29  history command" src="https://github.com/AndromedaIsComingg/LinuxPracticeProject/assets/140917780/1073608f-97ac-42a1-bd63-05203311ae31">

## 30. man Command
This command provides a user manual of any command or untilities you can run in terminal

For example you want to access the manual fro the ls command you will enter man ls

<img width="574" alt="30  man command" src="https://github.com/AndromedaIsComingg/LinuxPracticeProject/assets/140917780/42295fc7-cd41-4359-ba85-7f544c933452">

## 31. echo Command
This command displays the line of a text or string using the standard output.

when used with -n option, it display the output without the trailing new line

<img width="311" alt="31  echo command" src="https://github.com/AndromedaIsComingg/LinuxPracticeProject/assets/140917780/05948ff1-0935-442a-bcce-81292145f298">

## 32. zip, unzip Commands
The zip command is used to compress files in ZIP file, this is done to reduce dist usage

Its was used to compresss two files names "test" and "test2"

While the unzip command is used to unzip the zipped file.

<img width="419" alt="32  zip   unzip commands" src="https://github.com/AndromedaIsComingg/LinuxPracticeProject/assets/140917780/2ab0c157-989a-4d13-9053-a658610fbf00">

## 33. hostname Command
This command is used to know the system's hostname, it can be run with or without options

-a displays hostname's alias

-A displays the machine's fully qualified domain name

-i displays the machine's ip adresss

<img width="214" alt="33  hostname command" src="https://github.com/AndromedaIsComingg/LinuxPracticeProject/assets/140917780/8a88118d-d4c9-4da7-98fe-c09d3aa868ed">

## 34. useradd, userdel Commands
The useradd command is used to add a user, while the userdel command is used to remove a user. 

After adding a user, the passwd command is used to add a password. Only users with root privilages or sudo can use the useradd command.

<img width="269" alt="34  useradd userdel" src="https://github.com/AndromedaIsComingg/LinuxPracticeProject/assets/140917780/56d086ea-22d0-4226-a949-583b22488777">


## 35. apt-get Command
Used for handling Advanced Package Tool (APT) libraries.

<img width="338" alt="35  sudu apt-get" src="https://github.com/AndromedaIsComingg/LinuxPracticeProject/assets/140917780/b8aa94d5-3425-4b1e-be01-b65420954003">

## 36 nano, vi, jed Commands
This allows users manage and edit files via text editors such as nano, vi and jed. nano and vi comes with the operation system while jed has to be installed.

The nano command was performed on a text document named "test"
<img width="1152" alt="36  nano mac" src="https://github.com/AndromedaIsComingg/LinuxPracticeProject/assets/140917780/5eb4a957-84ce-47bc-b87d-f47de115916e">

## 37 alias unalias Commands
alias allows the create shortcut with same functionality as a command, file name or text. It instructs the shell to replace one string with the another.

unalias on the other hand deletes the existing alias

<img width="260" alt="37  alias unalias" src="https://github.com/AndromedaIsComingg/LinuxPracticeProject/assets/140917780/4d11c5a9-f0cc-479c-b8f1-639186562057">

## 38 su Command
Short for switch user, allows you run a program as another user. Using it with option -p keeps the same shell environment.

user was created with a name "shy" and the user was switched to.

<img width="245" alt="38  su command" src="https://github.com/AndromedaIsComingg/LinuxPracticeProject/assets/140917780/e67f2b31-f57c-4637-aa38-70f302511dca">


## 39 htop Command
This monitors system resources and server processes in realtime. As compared to top command, it has virtual indicators and mouse operations.

For this, user has to first run sudo apt install htop to install htop on linux or brew install htop for mac depending on the uinx environment.

<img width="867" alt="39  htop" src="https://github.com/AndromedaIsComingg/LinuxPracticeProject/assets/140917780/8c4d5af1-1ff0-477f-a278-3701d808c60e">

## 40 ps Command
Short for process status, takes the snapshot of all the running processes.
<img width="577" alt="40  ps" src="https://github.com/AndromedaIsComingg/LinuxPracticeProject/assets/140917780/dbec192c-a61b-4b34-ae95-e6f06cc48f84">


