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


## filesystem
linux uses the forward / structure and is hierarchical from root directory to working directory


## important directories
#### root/
 the start of the tree.
#### /boot
contains static files and stores data used before the kernel executes user mode programs
#### /dev 
contains special or device files
#### /bin
executable files
#### /etc
configuration files
#### /home
#### /user
home directories
#### /lib
shared libraries
#### /usr
user utilities and applications
#### /var
variable data such as logs or databases

all items in linux are "files" there are different designations
- d directory
- f file
- l symbolic links

symbolic links

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

    Set user password:

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

