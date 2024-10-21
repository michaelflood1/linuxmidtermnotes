Questions week 2
1. what is a qcow2 file
A qcow2 file is a disk format well equipped for virtualization. 
contains a complete file system and disk structure.
key features- copy on write. (stores on changes made to the original image rather than duplicating the whole disk)

compression support

easy snapshots for recovery and backup



2 what is a Droplet in digital ocean
VPS (virtual private server)
A A Digital ocean droplet is a single virtual instance that is ran off of their servers. containing a set amount of storage, ram, cpu speed etc. each droplet can be customized to match the requirements of whatever project.

3. What command is used to generate an ssh key pair
~/.ssh Keygen -t ed25519 -f ~/.ssh/do-key -C "email"
-t ed25519 specifies type of key 
-f specifies the save file 


4 what is the purpose of sudo pacman Syu
sudo (superuser)
pacman is archs packet manager
-S is sync used to install packages
-y Refreshes the package database to check latest info
-u upgrades all currently installed packages



packet installer and updater depending on modifiers i.e -S install -Syu update

5 describe different vim modes
i = interact, for editing
v = visual mode, used for copy and deleting bulk
: = commandline mode, used for saving and quitting

6 command to save and exit vim
-wq (write quit)
q! force quit
q quit
save w


7 how do you connect to your ssh.
i open my windows powershell and type ssh linux.
optionally you can use
ssh -i ~/.ssh/do-key arch@*dropletIP*

-i specifies path -i = identify file

arch is the username must be changed depending on your user name

the ip address found on digital ocean




questions oreilly
1 what is the root directory in a linux filesystem and what is its designation
root is the top level dir has supreme command of every other file system. parent of all parents

2. name three essential directories found in root and their purpose.
etc/ config files
	etc/passwd: user account info
	etc/shadow/ hashed info
	etc/group group account info
	etc/fstab filesystem mnt info
tmp/ basically ram files 
home/ contains home dir for ueach user storing personal files and settings
	home/user1/blah
bin/ executables
	contains ls bash cat grep
usr/ user utilities and apps
	usr/bin nonessential commands for apps
	usr/share independent data i.e documentation
lib/essential shared libraries
var/ holds variable data logs,databases
	var/log
	var/mail
	var/tmp

3. difference between symbolic links and regular files
symbolic links are basically pointers to other files. regular files are the standard, contain data such as text img or executables

4 what command is used to change file permissions
chmod 
example usage chmod ugo+x file.txt
chmod 777 file.txt

5 how do you view file perms
ls -l

6 concept of mounting filesystems
for storage outside of your default hierarchy you can position it inside of the default for ease of use
mount -t
7 purpose of proc and sys dirs
proc is the directory controlling and monitoring processes
sys directory or system is in charge of your kernel 

8 command to go to parent directory
cd ../

9search for specific file within a directory
find
i.e
find ~ /documents -name *.txt

10 what does pwd do
prints working directory

oreilly chapter 3

## filesystem










linux uses the forward / structure and is hierarchical from root directy to working directoy

root/
root is the start of the tree.

/boot
boot contains static files and stores data used before the kernel executes user mode programs

/dev contains special or device files



important directories

/bin
executable files

/etc
configuration files

/home
user home directories

/lib
shared libraries

/usr
user utilities and applications

/var
variable data such as logs or databases

all items in linux are "files" there are different designations
-d directory
-f file
symbolic links

    ln -s ~/Documents/config.yaml ~/config
    # creates
    ls -l 
    # will show symlinks
    cat ~/configurations`
    # will view contents of the symlinks pointed file

special files such as device files /proc /sys


all files have distinct permissions and owners
__________.
File type, Owner, Group, other. the "." at the end is extended attributes

modifying linux file perms

$ chmod ug+rwx "filename" 
this will adjust owner and group to have read write execute ability
in this method 
u = owner
g =group
o = others

changing chmod settings in octal
r = 4
w = 2
x = 1
still maintains owner group other

chmod 777 "file" give all owners groups and others full rwx  ability
333 is all write and xecute

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



to find permissions for a file use ls -l "filename"


mounting filesystems i.e multiple storage devices withing the same directory hierarchy

mount command is used for this

mount -t #type of device dir
mount /dir


standard linux commands

ls- lists contents of directory
cd changes dir
pwd prints current dir
find searches for files 

 enviorenment variable vs regular variable  vs local regular variable
ENVIORENMENT VARIABLE
set with EXPORT
export MY_VAR="butt"
global variables
echo "${MY_VAR}"
available to all child processes
examples PATH HOME USER SHELL

REGULAR VARIABLE
shell variables
my_var="butt"
scoped to that current shell
echo "${my_var}"

LOCAL REGULAR VARIABLE
local my_var="butt"
function scoped not callable outside of the function it is created in
only real during function runtime


basic bash sctipting fundamentals

!#/bin/env bash 
vs
!#bin/bash

bin/bash is the direct route so it will look for bash in your bin folder
env bash will run through your enviorenment variables better for multi enviorenments

set xecutable fo file
chmod +x your_script.sh
command line prompt to run a script ./your_file.ext


!!!!!!!!!!!!!! numeric operators [-eq, -ne, -gt, -lt,-ge, -le] or equal, not equal, greater than, less than, greater or equal, less or equal
!!!!!!!!!!!!! string operators [=,!=,-z,-n,<,>] or equal, not equal, null, not null, less than, greater than.
basic if statement

```bash

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

### FOR LOOPS

```bash

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
- has multiple branches for independant projests
- you can work with other people

made in 2005 by linus torvalds
git is a ***command line program*** installed on your local machine.
variety of GUI tools to interact with it.



## basic git commands

    git config --list

    git init # initializes repo

    git status
    git clone git@your-repo # clones repo
    git add file-name
    git commit -m 'yourbshere'
    git push

## cloud-init

comes set up on many linux distros
assists with managing a server with initial configuration

creating a cloud config

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


## Boot Process
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