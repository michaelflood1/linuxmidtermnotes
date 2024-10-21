[Filesystem.](#filesystem)  
[Important Directories.](#important-directories)  
[Modifying Linux File Permissions.](#modifying-linux-file-permissions)  
[Mounting Filesystems.](#mounting-filesystems)  
[Standard Linux Commands.](#standard-linux-commands)  
[Environment Variable vs Regular Variable vs Local Regular Variable.](#environment-variable-vs-regular-variable-vs-local-regular-variable)  
[Basic Bash Scripting Fundamentals.](#basic-bash-scripting-fundamentals)  
[Basic If Statement.](#basic-if-statement)  
[For Loops.](#for-loops)  
[Git.](#git)  
[Cloud-init.](#cloud-init)  
[Processes.](#processes)  
[Process Control Block.](#process-control-block)  
[Process Creation.](#process-creation)  
[Process Termination.](#process-termination)  
[Inter Process Communication.](#inter-process-communication)  
[Process Scheduling.](#process-scheduling)  
[Common System Calls.](#common-system-calls)  
[Signals.](#signals)  
[Killing.](#killing)  
[Terminating.](#terminating)  
[Boot Process.](#boot-process)  
[Find.](#find)  
[Grep.](#grep)  
[User ID.](#user-id)  
[Creating and Deleting Users.](#creating-and-deleting-users)  
[Shell Scripting Basics.](#shell-scripting-basics)  
[Using Echo.](#using-echo)  
[Variables in Bash.](#variables-in-bash)  
[Environment Variables.](#environment-variables)  
[Using Declare.](#using-declare)  
[Positional Parameters.](#positional-parameters)  
[Special Variables.](#special-variables)  
[Command Line Arguments.](#command-line-arguments)  
[Regex.](#regex)
[Quiz.](#questions)



## based on email

1. Basic Scripting Concepts
Conditional Statements

```bash
    If Statement Example:

    bash

    if [ -f "/path/to/file" ]; then
        echo "File exists."
    else
        echo "File does not exist."
    fi

Loops

    For Loop Example:

    bash

for i in {1..5}; do
    echo "Looping: $i"
done

While Loop Example:

bash

    count=1
    while [ $count -le 5 ]; do
        echo "Count: $count"
        ((count++))
    done

Functions

    Function Definition Example:

    bash

    my_function() {
        echo "This is my function."
    }
    my_function
```

2. Filesystem Structure
Key Locations:

    User Information:
        /etc/passwd - Contains user account information.
    Other Important Directories:
        /etc/shadow - Contains secure user account information (passwords).
        /etc/group - Contains group account information.

3. Command Structure

    General Format:

    bash

command [options] [arguments]

Example:

bash

    ls -l /home/user

        ls: command
        -l: option (long format)
        /home/user: argument (path to list)

4. File Permissions and Ownership

    Ownership:
        Each file can be owned by one user and one group.
    Permissions:
        User (Owner)
        Group
        Others
        Common permissions:
            Read (r)
            Write (w)
            Execute (x)
    Example of Permissions:
        drwxr-xr--
            Owner: read, write, execute
            Group: read, execute
            Others: read

5. Environment Variables vs. Regular Variables

    Environment Variables:
        Available to all child processes and affect the behavior of the shell and applications.
        Example: PATH, HOME

    Regular Variables:
        Local to the shell or script in which they are defined.
        Example: my_var="Hello"

6. SSH Configuration

    Why Restrict Root User SSH Access:
        Security: Prevents brute-force attacks on the root account.
        Encourages the use of normal user accounts for login and privilege escalation through sudo.

7. General Cloud Topics

    Example Question:
        Why are we using the San Francisco region?
        Possible Answer: The San Francisco region may be chosen for proximity to data centers, latency considerations, compliance regulations, or specific service availability.
## filesystem
linux uses the forward / structure and is hierarchical from root directory to working directory


## important directories
#### root/
 the start of the tree.
#### /boot
contains static files and stores data used before the kernel executes user mode programs

    /boot/vmlinuz (the compressed Linux kernel image)
    /boot/initrd.img (initial RAM disk image)
    /boot/grub/grub.cfg (GRUB bootloader configuration file)

#### /dev 
contains special or device files

    dev/null (the null device)
    dev/sda (the first hard disk)
    dev/tty (the terminal device)

#### /bin
executable files

    /bin/bash (the Bourne Again SHell)
    /bin/ls (command to list directory contents)
    /bin/cp (command to copy files)

#### /etc
configuration files

    /etc/passwd (user account information)
    /etc/shadow hashed user info
    /etc/hosts (static table of IP addresses and hostnames)
    /etc/fstab (file system table)
    /etc/group has group account info

#### /home
home directories

    /home/user1/.bashrc (a configuration file for the bash shell for user1)
    /home/user2/documents/report.txt (a text document for user2)
    /home/user3/.ssh/authorized_keys (SSH authorized keys for user3)


#### /lib
shared libraries

    /lib/libc.so.6 (the standard C library)
    /lib/libm.so.6 (the mathematical library)
    /lib/libpthread.so.0 (POSIX threads library)

#### /usr
user utilities and applications

    /usr/bin/python3 (the Python 3 interpreter)
    /usr/bin/git (the Git version control system)
    /usr/bin/vim (the Vim text editor)

#### /var
variable data such as logs or databases

    /var/log/syslog (system log file)
    /var/www/html/index.html (default webpage for a web server)
    /var/lib/mysql/mysql.sock (MySQL database socket file)




all items in linux are "files" there are different designations
- d directory
- f file
- l symbolic links

symbolic links point to name or location of a file
hard link points to inode



    ln -s ~/Documents/config.yaml ~/config
    # creates
    ls -l 
    # will show symlinks
    cat ~/configurations
    # will view contents of the symlinks pointed file

special files such as device files /proc /sys 

**all files have distinct permissions and owners**

File type, Owner, Group, other. the "." at the end is extended attributes

## modifying linux file perms

    $ chmod ug+rwx "filename" 
    this will adjust owner and group to have read write execute ability in this method 
    u = owner
    g =group
    o = others

changing chmod settings in octal

    r = 4
    w = 2
    x = 1

still maintains owner group other

    chmod 777 "file" give all owners groups and others full rwx ability
    333 is all write and execute
    666 is all read and write

chgrp changes the group of a file

chgrp [OPTIONS] GROUP FILE(s)

    chgrp teachers grades.txt

this changes the group of grades.txt to teachers

chown is similar except it changes the owner of a file

    chown [OPTIONS] USER[:GROUP] FILE(s)
    if only user is specified the user becomes the new owner of given file
    if a group is added with no space the group gets a group ownership
    if user is omitted and group is prefixed with : only the group ownership is changed

### to find permissions for a file use 

    ls -l "filename"

### mounting filesystems i.e multiple storage devices within the same directory hierarchy

    mount -t #type of device dir
    mount /dir

### standard linux commands

    ls- lists contents of directory
    cd changes dir
    pwd prints current dir
    find searches for files 

### environment variable vs regular variable vs local regular variable

    ENVIRONMENT VARIABLE
    set with EXPORT
    export MY_VAR="butt"
    global variables
    echo "${MY_VAR}"
    available to all child processes
    examples PATH HOME USER SHELL

### REGULAR VARIABLE

    shell variables
    my_var="butt"
    scoped to that current shell
    echo "${my_var}"

### LOCAL REGULAR VARIABLE

    local my_var="butt"
    function scoped not callable outside of the function it is created in
    only real during function runtime

## basic bash scripting fundamentals


### #!/bin/env bash vs #!/bin/bash

bin/bash is the direct route so it will look for bash in your bin folder
env bash will run through your environment variables better for multi environments

    set executable for file
    chmod +x your_script.sh
    command line prompt to run a script ./your_file.ext

*numeric operators [-eq, -ne, -gt, -lt, -ge, -le] or equal, not equal, greater than, less than, greater or equal, less or equal*
*string operators [=,!=,-z,-n,<,>] or equal, not equal, null, not null, less than, greater than.*

## basic if statement

```bash
#!/bin/env bash
if [[ value -eq value2 ]]; then
    echo "Value greater than value2"
elif [[ value -eq value2 ]]; then
    echo "values are equal"
else
    echo "value less than 10"

if [[ -z $1 ]]; then
    echo "please add arguments"
fi 
file="$1"

if [[ -e "$1" ]]; then
    echo "file exists"
else 
    echo "no file youre bad"
fi
```

## FOR LOOPS

```bash
#!/bin/env bash
for item in [list]; do
    [command]
done

#example
for item in apple banana cherry; do
    # Print each fruit
    echo "I like $item."
done

#c style list
for ((i = 0 ; i <= 1000 ; i++)); do
    echo "Counter: $i"
done

#to break a loop use break
# continue will move to next item in iteration

#troubleshooting
# set makes all executed commands echo to the terminal

#!/bin/bash
set -x
if [[ -f ~/.bashrc ]]; then
    source ~/.bashrc
fi
```

## git

Git is a distributed version control system

3 features 
- keeps track of file versions 
- has multiple branches for independent projects 
- you can work with other people

made in 2005 by linus torvalds 
git is a command line program installed on your local machine. 
variety of GUI tools to interact with it.

### basic git commands

    git config --list

    git init # initializes repo

    git status 
    git clone git@your-repo # clones repo 
    git add file-name 
    git commit -m 'yourbshere' 
    git push

## cloud-init

comes set up on many linux distros .assists with managing a server with initial configuration

### creating a cloud config

    #cloud-config
    users:
        - name: user-name
          primary_group: group-name
          groups: wheel
          shell: /bin/bash
          sudo: ['AKK=(ALL) NOPASSWD:ALL']
          ssh-authorized-keys:
            -sshe-ed255....

    packages:
        - ripgrep
          rsync
          neovim
    
    disable_root: true

in digital ocean you can click advanced options during creation to add the yaml

## processes 

an instance of a running program including
- program code
- current activity
- unique process id PID

Can be in one of sever states
- new -being created
- ready -waiting for a processor
- running -instructions are being executed
- waiting - process is waiting for events to occur
- terminated -finished execution

## Process control block

data structure maintained by the OS to store all process ino including
- state
- PID
- CPU registers
- Memore management info
- accounting info
- I/O status info

## Process creation
created using system calls i.e
- fork() -creates new process by duplicating calling process
- exec() -replaces current process

Parent child relationships.
the process that creates another process is called the parent

## Process termination
various methods
- Normal termination (exit status)
- error termination (abnormal exit)
- Terminated by another process using signals (kill command)

**terminated processes return an exit code/status if it is anything except ***0*** you have an error**

## Inter Process Communication
Methods for communication
- Pipes - allows data flow between
- message queues -store messages sent between 
- shared memory -multiple processes access same mem space
- semaphores -used for controlling access to shared resources

ps snapsots current processes
ps -e views all processes
ps -e | less
ps -e | grep -i bash pulls all processes and searches the pattern to filter for bash
ps -eo comm,pid,%cpu | grep -i systemd 
ps -e --forest | grep -i ssh shows the heirarchy of processes for ssh

## process scheduling
Long term decided which process is admitted to system
short term decides which process to execute next on the CPU
medium term Handles swapping of processes in and out of memory

## Common System Calls
- Key system calls related to processes:
- fork(): Creates a new process.
 - exec(): Executes a new program.
- wait(): Makes a parent process wait for its child to terminate.
- exit(): Terminates a process.

## Signals
A way for users or processes to communicate with running processes
**important signals**

    SIGINT (2) sent when keyboard interrupting (ctrl C)
    SIGTERM (15) requests graceful termination allowing clean up
    SIGKILL (9) forces immediate termination

#### killing
abusive ending

    kill [OPTIONS] [PID]
    kill -9 $(pid) #kills the hotfox

#### terminating
graceful quit

    pkill [options] <PATTERN>
    pkill -15 Chromium #terminates chromium respectfully


### Boot Process
The boot process is the sequence of events from power on until fully operational

    1. power on
        2. BIOS
            3. Master Boot Record (MBR)
                4. Boot Loader
                    5. Kernel
                        6. Initial RAM disk
                            7. parent process
                                8. command shell
                                    9. GUI  
## Find
used to locate files based on criteria

find [options] [path] [expression]

    find ~ -type f #finds regular files in home dir
    find . -type f -name "*.txt" #finds files that end with .txt in working dir
    find . -type f -mmin -10 # finds files modified in the last 10 min

    find . -type f -exec ls -l {} \; # finds all regular files in current dir and subdir then executes ls -l displaying detailed info
    find . -type f -exec ls -l {} + # finds all regular files in current and sub dir then groups multiple files and lists info

## grep
locates patterns in files

grep [options] PATTERNS [FILE]

    grep -i "search-term" # filename.txt #Searches for lines in filename.txt that contain either "word1" or "word2" using extended regular expressions.
    grep -w "word" filename.txt # Searches for the whole word "word" in filename.txt, ensuring it doesn’t match substrings (e.g., it won't match "sword"
    grep -n "search-term" filename.txt # Explanation: Displays the line numbers of lines that contain "search-term" in filename.txt.
    grep -rl "search-term" /path/to/directory #  Recursively searches for "search-term" in all files under the specified directory and lists the names of files that contain the term.
    grep -C 3 "search-term" filename.txt #  Displays 3 lines of context (lines before and after) around each match of "search-term" in filename.txt.

    grep -r search-word directory #recursive search
    grep -c "set" ~/.bashrc #count occurence

## user ID

    Users: Divided into human users (people) and system users (resource isolation).
    User ID (UID): Unique identifier for each user.
        UID 0: root (superuser)
        UIDs 1-999: reserved for system users
        UID 65534: "nobody" user
        UIDs 1000-65535: regular users

User and Group Management Commands
Viewing Users and Groups

    View users: cat /etc/passwd
    View groups: cat /etc/group
    List groups for a user: groups <user-name>

## Creating and Deleting Users

***useradd vs adduser***

| useradd  | adduser   |   
| :--:  | :--:  |
| low level  | high level  |
| creates user  |  creates user |
| on most distros  | mainly just on ubuntu based distros  |
| not much customization  |  lots of customization |

### Create a new user:


useradd <user-name>

### Delete a user:


userdel [OPTIONS] <user-name>

### Delete user and home directory:


    userdel -r <user-name>

### Modifying User Accounts

### Set user password:

passwd <user-name>

### Lock user account:

passwd -l <user-name>

### Unlock user account:


    passwd -u <user-name>

### Managing Groups

    Create a new group:


groupadd <group-name>

### Add user to a group:


usermod -aG <group-name> <user-name>

## Sudo Command

    Purpose: Temporarily elevate user privileges.
    Configuration Files:
        /etc/sudoers: Define who can use sudo.
        /etc/sudoers.d/: Directory for individual config files.

### Granting Sudo Access

    Grant members of the "wheel" group sudo privileges by uncommenting:

    plaintext

    %wheel ALL=(ALL:ALL) ALL

### Changing Permissions and Ownership
### Changing File Permissions

    Using chmod:

    bash

    chmod 644 <file-name>          # Numeric method
    chmod u=rw,g=r,o=r <file-name> # Symbolic method

### Changing File Ownership

    Using chown:

    bash

chown <user-name>:<group-name> <file-name> # Change both user and group
chown :<group-name> <file-name>            # Change only group


## shell scripting basics
The shebang (#!) is the first line in a script that specifies which interpreter to use.
Examples:
 bash

    #!/bin/bash
    printf "hello world\n"

    #!/usr/bin/env python
    print("hello world")

It must be the first line in the file. Lines starting with # after the shebang are comments.

**Single Quotes vs Double Quotes in Bash**

Single Quotes ('): Preserve the literal value of each character.
Double Quotes ("): Allow variable expansion and command substitution.

## Using echo

The built-in echo prints arguments to standard output.
It adds a newline (\n) after executing and can handle multi-line outputs while preserving whitespace:

    echo "
        this
            is
    a multiline
    echo statement
    "

## Variables in Bash

Declaring a variable:

    animal="wolf"

Using a variable:

    echo "$animal"

## Environment Variables
Accessible in subshells.
Defined using:

    export VARIABLE=value
Conventions: Typically uppercase (e.g., PATH, EDITOR).

### Using declare

To provide attributes to a variable:

    declare -r CONFIG=file  # Read-only variable
    declare -i NUM          # Integer variable

### Positional Parameters
Access script arguments:

    echo $0 $1 $2  # $0 is the script name, $1 is the first argument, etc.

### Special Variables

| Special Variable | Description |
| :-----------------: | :----------: |
| $0	            | Name of the bash script |
| $1, $2,           | ...	Script arguments |
| $$	            | Process ID of the current shell |
| $#	            | Total number of arguments |
| $@	            | All arguments |
| $?	            | Exit status of the last executed command |
| $!	            | Process ID of the last executed command |
| $*	            | All arguments treated as a single string |




# command line arguments
### ls
ls [options] [directory]

| ls | args | use |
| :-----------------: | :----------: | :--------------:  |
|     ls     | -l |  shows details like permissions size owner |
|       ls  | -a	| shows hidden files  |
| 	     ls       | -h |  human readable sizes  |
| 	       ls    | -r |  reverse order of output  |
| 	         ls  | -R | recursive listing for all directories and sub directories |

### grep
grep [options] "pattern" [file]

| grep | args | use |
| :-----------------: | :----------: | :--------------:  |
| grep            | -i | case does not matter for patterns  |
| grep        |  -r	| recursivesly searches directories  |
| grep	            | -n  |  shows line numbers for matches  |
| grep	            | -v | inverts match so it sorts for those that dont match   |
| grep	            | --color | highlights matching text |


### find
find [path] [options] [expression]

| find | args | use |
| :-----------------: | :----------: | :--------------:  |
|   find         | -name "pattern" |  searches case sensitively by the pattern given |
|   find      |  -iname "pattern"	| searchs non case sensitively by the pattern given |
| 	find            |  -type [f|d] |  searches for either files or directories  |
| 	find            | -size +# | finds files larger than  given #   |
| 	find            | -exec command| executes a command on found files|


### cat
cat [options] [file...]

| command | args | use |
| :-----------------: | :----------: | :--------------:  |
|  cat          | -n  | numbers all output lines  |
|    cat     | -E	|  shows end of line markers |
| 	cat            | -s |  squeezes multiple blank lines into one  |
| 	cat            | -b |  numbers the non empty lines  |
|
### mkdir
mkdir [options] directory_name

| command | args | use |
| :-----------------: | :----------: | :--------------:  |
|  mkdir          | -p  |  creates parent directories where needed  |
|  mkdir       | -v	|  verbose output, shows directories created |

### sudo
sudo [command]

| command | args | use |
| :-----------------: | :----------: | :--------------:  |
|    sudo        | -i  | starts the shell as root  |
|    sudo     | -u [user]	| runs the command as specified user  |
| 	 sudo           | -k |  resets the sudo timestamp  |

### chmod
chmod options mode file

| command | args | use |
| :-----------------: | :----------: | :--------------:  |
|    chmod        | 777 file  | sets read write and execute for owner group other   |
|    chmod     | r+w+x	file |  sets read write execute for owner group and other  |
| 	 chmod           | -R |  recursively changes perms for all files in a directory  |

### echo
echo [options] [string]

| command | args | use |
| :-----------------: | :----------: | :--------------:  |
|     echo       | -n  | does not output the trailing newline   |
|    echo     | -e	| enables interpretation of \, (newline)  |


### touch
touch [options] filename

| command | args | use |
| :-----------------: | :----------: | :--------------:  |
|   touch         | -c  | do not create the file if it does not exist  |
|    touch     | -t	[[CC]YY]MMDDhhmm[.ss] | set specific timestamp  |


### mv
mv [options] source destination

| command | args | use |
| :-----------------: | :----------: | :--------------:  |
|    mv        | -i | prompt before overwrite  |
|    mv     | -f	| force overwwrite without prompt  |
| 	mv            | -n |  do not overwrite  |

### cp
cp [options] source destination

| command | args | use |
| :-----------------: | :----------: | :--------------:  |
|    cp        | -r  | recursively copies directories  |
|    cp     | -i	|  prompt before overwrite  |
| 	 cp           | -v |  verbose output  |
| 	 cp           | -p |  preserve attributes i.e perms, timestamp  |

|command  | purpose  | key options |
| :---: | :---: | :---: |
| ls |list contents  | -l, -a, -h, -R |
| grep | search for patterns | -i, -r, -n, -v  |
| find | search files | -name, -type, -size, -exec |
| cat | display files | -n, -E, -s  |
| mkdir | create directory | -p, -v |
| sudo | run with admin privelage | 	-i, -u, -k |
| chmod | change permissions | -R, u+x, 755 |
| echo | print text | -n, -e |
| touch | create files | -c, -t |
| mv | move files | -i, -f, -n |
| cp | copy files | -r, -i, -v, -p |

## regex

#### [][]

    [1][a] matches any two character string that the first character is 1 and second is a
    [1-4][a-c] matches any two character string where the first character is between 1 and 4 and the second character is a-c
    i.e 1a 3b 2c

#### *

    *.txt matches all file types that have .txt extension
    egg* all


### table

| **Regex Pattern** | **Description**                                                  | **Example Matches**            |
|-------------------|------------------------------------------------------------------|--------------------------------|
| `.`               | Matches any single character except newline.                    | `a`, `1`, `#`                  |
| `^abc`            | Matches "abc" at the **start** of a string.                    | `abc123`, `abc`                |
| `abc$`            | Matches "abc" at the **end** of a string.                      | `123abc`, `abc`                |
| `a*`              | Matches **zero or more** occurrences of "a".                   | `a`, `aa`, `aaa`, `""` (empty string) |
| `a+`              | Matches **one or more** occurrences of "a".                    | `a`, `aa`, `aaa`               |
| `a?`              | Matches **zero or one** occurrence of "a".                      | `a`, `""`                      |
| `a{n}`            | Matches **exactly n** occurrences of "a".                       | `aaa` (where n=3)              |
| `a{n,}`           | Matches **at least n** occurrences of "a".                      | `aaa`, `aaaaa` (where n=3)     |
| `a{n,m}`          | Matches between **n and m** occurrences of "a".                | `aa`, `aaa`, `aaaa` (where n=2, m=4) |
| `[abc]`           | Matches any **single character** listed inside the brackets.    | `a`, `b`, `c`, `1` (not `d`)   |
| `[^abc]`          | Matches any **single character** **not** listed inside the brackets. | `1`, `2`, `d` (not `a`, `b`, `c`) |
| `(abc)`           | Groups the characters "abc".                                    | Matches `abc` in `abc123`      |
| `a|b`             | Matches either "a" or "b".                                      | `a`, `b`, but not `c`          |
| `\d`              | Matches any **digit** (equivalent to `[0-9]`).                 | `0`, `5`, `9`                  |
| `\D`              | Matches any **non-digit** character.                            | `a`, `#`, ` `                  |
| `\w`              | Matches any **word character** (letters, digits, underscore).  | `a`, `A`, `1`, `_`             |
| `\W`              | Matches any **non-word character**.                             | `#`, ` `, `!`                  |
| `\s`              | Matches any **whitespace character** (spaces, tabs, newlines). | ` `, `\t`, `\n`                |
| `\S`              | Matches any **non-whitespace character**.                       | `a`, `1`, `!`                  |
| `(?=abc)`         | Positive lookahead for "abc".                                   | Matches position before `abc` in `xyzabc` |
| `(?!abc)`         | Negative lookahead for "abc".                                   | Matches position not followed by `abc` |



# Linux Process Control Quiz

## Questions

1. What command is used to view the currently running processes in Linux?
   <details>
   <summary>Answer</summary>
   The `ps` command.
   </details>

2. How can you display detailed information about a specific process in Linux?
   <details>
   <summary>Answer</summary>
   The `ps -p <PID>` command.
   </details>

3. What does the `top` command do in a Linux environment?
   <details>
   <summary>Answer</summary>
   It provides a dynamic view of system processes.
   </details>

4. Explain the purpose of the `ps` command in Linux.
   <details>
   <summary>Answer</summary>
   It displays information about active processes.
   </details>

5. What is the function of the `kill` command?
   <details>
   <summary>Answer</summary>
   It is used to send a signal to a process, often to terminate it.
   </details>

6. Describe what a process ID (PID) is in Linux.
   <details>
   <summary>Answer</summary>
   A unique identifier assigned to each process.
   </details>

7. What command can you use to terminate a process by its name?
   <details>
   <summary>Answer</summary>
   The command `pkill <process_name>`.
   </details>

8. How can you run a command in the background in Linux?
   <details>
   <summary>Answer</summary>
   By appending `&` to the command.
   </details>

9. What does the `&` symbol indicate when running a command in Linux?
   <details>
   <summary>Answer</summary>
   It runs the command in the background.
   </details>

10. Explain the purpose of the `bg` command.
    <details>
    <summary>Answer</summary>
    It resumes a suspended job in the background.
    </details>

11. What does the `fg` command do in a Linux shell?
    <details>
    <summary>Answer</summary>
    It brings a background job to the foreground.
    </details>

12. Describe how you can pause a running process in Linux.
    <details>
    <summary>Answer</summary>
    You can use the `kill -STOP <PID>` command.
    </details>

13. What signal is sent by the `kill` command by default?
    <details>
    <summary>Answer</summary>
    The `SIGTERM` signal.
    </details>

14. What does the command `nohup` do in a Linux context?
    <details>
    <summary>Answer</summary>
    It allows a command to continue running after the user logs out.
    </details>

15. How do you check the status of a background job in Linux?
    <details>
    <summary>Answer</summary>
    By using the `jobs` command.
    </details>

16. What is the purpose of the `nice` command?
    <details>
    <summary>Answer</summary>
    It sets the scheduling priority of a process.
    </details>

17. Explain what a zombie process is in Linux.
    <details>
    <summary>Answer</summary>
    It is a process that has completed execution but still has an entry in the process table.
    </details>

18. How can you prevent a process from being killed by the user?
    <details>
    <summary>Answer</summary>
    By changing its permissions or using `nohup`.
    </details>

19. What command is used to change the priority of a running process?
    <details>
    <summary>Answer</summary>
    The `renice` command.
    </details>

20. Describe the function of the `nice` and `renice` commands.
    <details>
    <summary>Answer</summary>
    `nice` sets the priority for a command at start, while `renice` changes it for running processes.
    </details>

21. What is the significance of the `/proc` filesystem in Linux?
    <details>
    <summary>Answer</summary>
    It contains information about processes and system resources.
    </details>

22. How can you find out how much CPU a process is using?
    <details>
    <summary>Answer</summary>
    By using the `top` or `htop` commands.
    </details>

23. What does the `pstree` command display?
    <details>
    <summary>Answer</summary>
    It displays a tree-like structure of processes.
    </details>

24. How can you see which processes are using a specific file in Linux?
    <details>
    <summary>Answer</summary>
    By using the `fuser` command.
    </details>

25. Explain the role of the `at` command in scheduling tasks.
    <details>
    <summary>Answer</summary>
    It schedules commands to run at a specific time.
    </details>

26. What does the `cron` service do in a Linux environment?
    <details>
    <summary>Answer</summary>
    It runs scheduled tasks at regular intervals.
    </details>

27. Describe how to start a process at boot time in Linux.
    <details>
    <summary>Answer</summary>
    By placing scripts in the `/etc/init.d/` directory.
    </details>

28. What is the purpose of the `systemctl` command?
    <details>
    <summary>Answer</summary>
    It manages system services and units.
    </details>

29. How do you list all running services in a Linux system?
    <details>
    <summary>Answer</summary>
    The command `systemctl list-units --type=service`.
    </details>

30. What command can be used to stop a service in Linux?
    <details>
    <summary>Answer</summary>
    The command `systemctl stop <service-name>`.
    </details>

31. How do you restart a service using the command line in Linux?
    <details>
    <summary>Answer</summary>
    The command `systemctl restart <service-name>`.
    </details>

32. What does the command `service <service-name> status` do?
    <details>
    <summary>Answer</summary>
    It checks the running status of a service.
    </details>

33. Explain the difference between a process and a thread in Linux.
    <details>
    <summary>Answer</summary>
    A process is an independent execution unit, while a thread is a lightweight process that shares resources.
    </details>

34. How can you check memory usage of processes in Linux?
    <details>
    <summary>Answer</summary>
    The `top` command displays memory usage.
    </details>

35. What is the purpose of the `pstree` command in Linux?
    <details>
    <summary>Answer</summary>
    It displays the process tree in a hierarchical format.
    </details>

36. How do you monitor disk usage of processes in Linux?
    <details>
    <summary>Answer</summary>
    The `iotop` command can be used to monitor disk usage.
    </details>

37. What does the `lsof` command do in relation to processes?
    <details>
    <summary>Answer</summary>
    It lists open files and their associated processes.
    </details>

38. Describe how to change the ownership of a process in Linux.
    <details>
    <summary>Answer</summary>
    You can use the `chown` command, but it generally applies to files, not processes directly.
    </details>

39. What is the purpose of the `killall` command?
    <details>
    <summary>Answer</summary>
    It terminates all processes with a given name.
    </details>

40. How can you find the parent process of a given PID?
    <details>
    <summary>Answer</summary>
    By using the command `ps -o ppid= -p <PID>`.
    </details>

41. What signal is sent by the `SIGKILL` command?
    <details>
    <summary>Answer</summary>
    It forcefully kills a process.
    </details>

42. Explain the significance of the `ctrl + Z` keyboard shortcut in Linux.
    <details>
    <summary>Answer</summary>
    It suspends the currently running foreground process.
    </details>

43. How do you list all user processes in Linux?
    <details>
    <summary>Answer</summary>
    By using the command `ps -u <username>`.
    </details>

44. What is the difference between foreground and background processes?
    <details>
    <summary>Answer</summary>
    Foreground processes interact with the user; background processes do not.
    </details>

45. How can you execute a command with elevated privileges in Linux?
    <details>
    <summary>Answer</summary>
    The command `sudo <command>`.
    </details>

46. What command can you use to see the system uptime in Linux?
    <details>
    <summary>Answer</summary>
    The `uptime` command.
    </details>

47. Describe how to view the environment variables of a process in Linux.
    <details>
    <summary>Answer</summary>
    The command `cat /proc/<PID>/environ`.
    </details>

48. How can you limit the CPU usage of a process in Linux?
    <details>
    <summary>Answer</summary>
    Using `cpulimit` or `nice`.
    </details>

49. What command can be used to schedule a command to run at a specific time?
    <details>
    <summary>Answer</summary>
    The `at` command.
    </details>

50. Explain how to view real-time system resource usage in Linux.
    <details>
    <summary>Answer</summary>
    The `htop` or `top` command.
    </details>

