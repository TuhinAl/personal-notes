### Login to Local, Remote Graphical and Text Mode:

SSH: Secure Shell (SSH) is a cryptographic network protocol for operating network services securely over an unsecured network. The best known example application is for remote login to computer systems by users.

Telnet: Telnet is a network protocol used on the Internet or local area networks to provide a bidirectional interactive text-oriented communication facility using a virtual terminal connection.

but SSH is more secure than Telnet because it uses encrypted communication.
* `$ ip link` - is used to check the network interfaces.
* `$ ip addr` - is used to check the IP address of the network interfaces.
* `$ ssh username@ipaddress` - is used to login to the remote machine.
* `$ telnet ipaddress` - is used to login to the remote machine.
* `$ ip a` - is used to check the IP address of the network interfaces.

Computer(SSH Client) -> Server(SSH Daemon)

## Essentials Commands:
* **Create, Delete, Copy and Move files and directories:**

* `$ ls -la `  #**l**ist **a**ll files and directories in the current directory.
* `$ ls -lah` # h for human redable i.e 6238 to 6.2KB

1  2     3    4     5  6                 7                    8    9  10  11   12 <br>
d**rwx**r-x**r-x**  2 root              root                 4096 Feb  5 07:02 Documents <br>

1. disk/file/entry type
![Create Link](essential-comman-image/file-type.png) <br>
2. permissions for the owner <br>
3. permissions for the group <br>
4. permissions for everyone else <br>
![Create Link](essential-comman-image/permission.png) <br>

5. number of hard links <br>
6. owner <br>
7. group <br><br>
![Create Link](essential-comman-image/evaluating-permission.png) <br><br>
![Create Link](essential-comman-image/adding-permission.png) <br><br>
![Create Link](essential-comman-image/remove-permission.png) <br><br>
![Create Link](essential-comman-image/exact-permission.png) <br><br>
![Create Link](essential-comman-image/chaining-permission.png) <br><br>
![Create Link](essential-comman-image/octal-permission.png) <br><br>
![Create Link](essential-comman-image/octal-permission-2.png) <br><br>

8. size <br>
9. date and time of last modification <br>
10. name <br>
11. -> link <br>
12.  <br>

![Create Link](essential-comman-image/change-directory.png) <br>


**File and directory access:**

To access a file or directory on our command line and specify its file path or its directory path. 
1. **Absolute path:** The absolute path is the full path to a file or directory starting from the root directory. Its starts with root directory that represented by a forward slash (/) .
2. **Relative path:** The relative path is the path to a file or directory starting from the current directory. 
To understand a relative path we must explore what the current directory means. this also means the working directory.
now to see our working directory, we can type `pwd` command. 


* `$ cd /etc` # Change directory to /etc <br>
* `$ cd ..` # Change directory to the parent directory <br>
* `$ cd ~` # Change directory to the home directory <br>
* `$ cd -` # Change directory to the previous directory <br>
* `$ pwd` # Print the current working directory <br>
* `$ cd ..` #always refer to parent directory of our current directory <br>
* `$ cd /` # Go to root directory <br>
* `$ touch file.txt` # Create a new file <br>
* `$ mkdir directory` # Create a new directory <br>
* `$ cp file.txt file2.txt` # Copy a file <br>
* `$ cp -r directory directory2` # Copy a directory <br>
* `$ mv file.txt file2.txt` # Move a file <br>
* `$ mv directory directory2` # Move a directory <br>
* `$ rm file.txt` # Remove a file <br>
* `$ rm -r directory` # Remove a directory <br>
* `$ ls -lrt` # List files and directories in reverse order of modification time <br>
* `$ ls -l | grep file` # List files and directories and filter the output with grep <br>
* `$ cat file.txt` # Display the content of a file <br>
* `$ less file.txt` # Display the content of a file with a pager <br>
* `$ head file.txt` # Display the first lines of a file <br>
* `$ tail file.txt` # Display the last lines of a file <br>
* `$ wc file.txt` # Count the number of lines, words, and characters in a file <br>
* `$ chmod 755 file.txt` # Change the permissions of a file <br>
* `$ chown user:group file.txt` # Change the owner and group of a file <br>
* `$ ln -s file.txt link.txt` # Create a symbolic link to a file <br>
* `$ ln -s directory link` # Create a symbolic link to a directory <br>
* `$ find / -name file.txt` # Find a file in the filesystem <br>
* `$ grep pattern file.txt` # Search for a pattern in a file <br>
* `$ ps` # Display the processes running on the system <br>
* `$ top` # Display the processes running on the system with a pager <br>
* `$ kill PID` # Terminate a process by its process ID <br>
* `$ killall process` # Terminate a process by its name <br>
* `$ shutdown -h now` # Shutdown the system immediately <br>
* `$ reboot` # Reboot the system <br>
* `$ df -h` # Display the disk usage <br>
* `$ du -h` # Display the disk usage of a directory <br>
* `$ free -h` # Display the memory usage <br>
* `$ uname -a` # Display the system information <br>
* `$ date` # Display the current date and time <br>
* `$ cal` # Display the calendar <br>
* `$ history` # Display the command <br>



**Create and Manage Hard Link:**
To understand *hard links* and *soft links*, first, we must learn some very basic things about *file systems*. Let's imagine a Linux computer is shared by two users, **Aaron** and **Jane**. Aaron logs in with his own username and password, and Jane logs in with her own username and password. This lets them use the same computer, but have different desktops, different program settings and so on. Now Aaron takes a picture of the family dog and saves it into `/home/Aaron/pictures/family_dog.jpg`. <br>

Now there's a command in Linux that lets us see some interesting things about files and directories, this is `stat`. Now we'll notice an inode number.

![Create Link](essential-comman-image/inodes.png) <br>

File system like XFS, ext4 and other keep track of data with the help of inodes. Our picture might have blocks of data scattered all over the disk, but the inode remembers where all those pieces are stored. It also keeps track of metadata, things like permissions, last modified date, last accessed, and so on. But it would be inconvenient to tell your computer, hey, show me inode `52946177`. So we work with files instead. The one called `family__dog.jpg`. The one called family underscore dog dot jpg. In this case, the file points to the inode, and the inode points to all of the blocks of data that we require. And we finally get to what interests us here.<br><br>


Inodes are data structures that store metadata about files and directories, such as their permissions, size, and location on the disk. When we create a file or directory, the file system allocates an inode to it and stores the file or directory data in blocks on the disk.
suppose my *dummy.pdf* might have blocks of data scattered all over the disk, but inode remembers where all the blocks are stored.<br><br>

There's already one Link(see the image, **Links-1** ) to our inode.<br><br>
![Create Link](essential-comman-image/links.png) <br><br>
Yes there is. When we create a file something like this happens. We tell Linux, hey save this data under the file `family__dog.jpg`. And Linux says okay we'll group all the file's data under inode 52946177. Data blocks and inode created. We'll hard link the file family underscore dog jpg to inode 52946177. <br><br>

Now when we want to read the file we'll say hey Linux, give me the data for `family__dog.jpg` file. And Linux says okay let me see what I know this links to. Here's all the data you requested for inode 52946177. So the number shown as links in the output of the `stat` command is the number of hard links to this inode from files or filenames.<br><br>

**Easy to understand, but why would we need more than one hard link for this data?** <br>
Well, Jane has her own folder of pictures at `/home/**Jane**/pictures/family_dog.jpg`. How can Aaron share this picture with Jane? Now, the easy answer is to just copy `family__dog.jpg` to slash `/home/**Jane**/pictures/`, family underscore dog jpg, no problem. Right. <br><br>

![Create Link](essential-comman-image/hard-link-1.png) <br><br>

But now imagine we must do this with 5000 pictures. We would have to store 20 GB of data twice. Why use 40 GB of data when you could just use 20 GB? So how can we do that instead of copying `/home/**Aaron**/pictures/family_dog.jpg` to `/home/**Jane**/pictures/family_dog.jpg`? We could hard link it to `/home/**Jane**/pictures/family_dog.jpg`. And the syntax of the command is: <br>
`$ ln path/to/the/target/file path/to/the/link/file.`<br> 
The target file is the file that you want to link with. The link file is simply the name of the new hard link that we create. Technically, the hard link created at the destination is a file like any other. The only special thing about it is instead of pointing to a new Inode, it points to the same Inode as the target file. File Point to the Inode -. Inodes points to the all of the blocks of data we required.<br><br>

Now our picture is only stored once, but the same data can be accessed at different locations through different file names. If we run the `stat` command now we can see the links are now two. This is because this inode now has two hard links pointing to it. <br><br>
![Create Link](essential-comman-image/hard-links.png) <br><br>

Now another beautiful thing about hard links is this Aaron and Jane share the same 5000 pictures through hard links, but maybe Aaron decides to delete his hard link of `/home/Aaron/pictures/family_dog.jpg`. Now what will happen with Jane's picture? Nothing. She'll still have access to that data. Why Because the inode still has one hard link to it. It had two, but now it has one.<br><br>

![Create Link](essential-comman-image/one-side-hard-link-delete.png) <br>

But if Jane also decides to delete her hard link to slash home slash Jane's slash pictures family underscore dog dot jpg The inode will have zero links to it When there are zero links, the data itself will disappear from the file system.
<br><br>

![Create Link](essential-comman-image/zero-hard-links.png) <br>

Limitations of Hard Links:
1. Hard links for files, not directories. <br>
2. Only Hard links within the same file system. <br>>
3. External mounted drive (/mnt/Backups/files) can't be hard linked from (/ssd/home/file) <br>>

Considerations when hard link: <br>
1. Make sure you have the proper permissions to create the link file at the destination. <br>
2. Make sure that all users involved have the proper permissions to access the file. <br>

i.e for two user *John* and *Aaron*, this might mean that we need to add both their username to the same group for example family group. Then we would use a command to let the group family read and write to this file.
remember you only need to change permission on of the hard links. That's because you are actually changing permission stored by the INode <br>

* `$ useradd -m -G family John` # Add a user to a group. `-m`: Creates a home directory for `John` at the default location, which is usually `/home/John`. <br>
* `$ useradd -m -G family Aaron` # Add a user to a group <br>
* `$ chown :family file.txt` # Change the group of a file <br>
* `$ chmod 660 /home/aaron/Pictures/family_dog.jpg` # Change the permissions of a file <br>


**Create and Manage Soft Link:**
* computer shortcuts <br>
* Softlink is nothing more than a file that points to a path. <br>
* Symbolic link <br>



* `$ ln file.txt link.txt` # Create a hard link to a file <br>
* `$ ln directory link` # Create a hard link to a directory <br>
* `$ ls -i file.txt link.txt` # Display the inode number of a file <br>
* `$ find / -inum inode_number` # Find a file by its inode number <br>
* `$ rm file.txt` # Remove a file <br>
* `$ rm -i file.txt` # Remove a file with confirmation <br>
* `$ rm -f file.txt` # Remove a file without confirmation <br>
* `$ rm -r directory` # Remove a directory <br>
* `$ rm -rf directory` # Remove a directory without confirmation <br>
* `$ rm -rf directory` # Remove a directory without confirmation <br>
* `$ ls -l` # List files and directories <br>
* `$ ls -lh` # List files and directories with human-readable sizes <br>
* `$ ls -lS` # List files and directories by size <br>
* `$ ls -lt` # List files and directories by modification time <br>
* `$ ls -lR` # List files and directories recursively <br>
* `$ ls -la` # List all files and directories <br>
* `$ ls -l | grep file` # List files and directories and filter the output with grep <br>
* `$ ls -l | sort -k 5` # List files and directories and sort the output by the  fifth column
* `$ ls -l | sort -k 5 -r` # List files and directories and sort the output by the fifth column in reverse order<br>
* `$ ls -l | sort -k 5 -n` # List files and directories and sort the output by the fifth column numerically<br>
* `$ ls -l | sort -k 5 -nr` # List files and directories and sort the output by the fifth column numerically in reverse order<br>
* `$ ls -l | sort -k 5 -n | head -n 5` # List files and directories and sort the output by the fifth column numerically and display the first five lines<br>
* `$ ls -l | sort -k 5 -n | tail -n 5` # List files and directories and sort the output by the fifth column numerically and display the last five lines<br>
* `$ ls -l | sort -k 5 -n | head -n 5 | tail -n 3` # List files and directories and sort the output by the fifth column numerically and display the first five lines and the last three lines <br>
* `$ ls -l | sort -k 5 -n | head -n 5 | tail -n 3 | wc -l` # List files and directories and sort the output by the fifth column numerically and display the first five lines and the last three lines and count the number of lines <br>
`$ ls -l | sort -k 5 -n


**18. List, Set and Change Standard File Permission:**
* Only the Owner of a file or directory can change permission 
* Root user can change permission of any file or directory
* To change the group of a fileor directory we can use the `chgrp` command
* To change the owner of a file or directory we can use the `chown` command


**19. SUID, SGID and Sticky Bit:**
SUID A special permission that allows `users` to run an **executable** with the permission of the executable owner. <br>
SGID is a similar permission, but it applies to both **executables** and **directories**. <br>
Sticky Bit is a special persmission that can be set on **directories**, It restricts file deletion in that directory. 
SUID - Set User ID <br>
SGID - Set Group ID <br>
**SUID** - when this is set on a file, it means that whenever the file is executed, it going to be executed as the User IDof the owner of the file Instead of the User ID of the person who is running the file.<br>
Capital **S** in the permission means that the file has the SUID permission but it is not executable. <br>
Small **s** in the permission means that the file has the SUID permission and it is executable. <br>
`$ chmod 4664 testsuidfile` <br>
`$ chmod 4764 testsuidfile` <br>
![Create Link](essential-comman-image/suid.png) <br>

`$ touch testsuidfile` <br>
`$ chmod 2664 testsuidfile` <br>
`$ chmod 4664 testsuidfile` <br>
`$ chmod 4764 testsuidfile` <br>


**SGID** 
Capital **S** in the permission means that the file has the SGID permission but it is not executable.
Small **s** in the permission means that the file has the SGID permission and it is executable.
`$ touch testsgidfile`
`$ chmod 2664 testsgidfile`
`$ chmod 2674 testsgidfile`

Important: sometimes you might ask to find that have the SUID bit or the SGID bit set. 
`$ find . -perm /4000` # Find files with the SUID bit set
`$ find . -perm /2000` # Find files with the SGID bit set
`$ find . -perm /6000` # Find files with the Both(SUID+SGID) bit set
`$ find . -perm /1000` # Find files with the sticky bit set

**Sticky Bit**
The sticky bit is a permission that can be set on directories. 
When the sticky bit is set on a directory, it means that only the owner of the file can delete the file.
* `$ mkdir teststickyfile` # Create a new directory <br>
* `$ ls -ld stickydir/` # List the directory <br>
* `$ chmod +t stickydir/` # Set the sticky bit on the directory <br>
* `$ chmod 1777 stickydir/`  <br>
* `$ chmod 1666 stickydir/` <br>
* `$ chmod 1775 teststickyfile` <br>


**Search for File:**
* / (slash mode): Matches **any** of the specified permissions. <br>
* - (dash mode): Matches **all** of the specified permissions. <br>
* = (exact mode): Matches **exactly** the specified permissions. <br>

* `find / -perm -o=rw`	# Finds files where **others have both** r **and** w.<br>
* `find / -perm /o=rw`	# Finds files where **others have either** r **or** w **or both**. <br>
* `find / -perm =o=rw`	# Finds files where **others have exactly** rw (**and nothing else**).

* `$ find -name file1.txt` # No path –> search current directory
* `$ find / -name file.txt` # Find a file in the filesystem <br>
   ![Search Name](essential-comman-image/search-name.png) <br>
   ![Search Name](essential-comman-image/modified-time.png) <br>
   ![Search Name](essential-comman-image/file-size.png) <br>
   ![Search Name](essential-comman-image/search-expression.png) <br>
   ![Search Name](essential-comman-image/search-exp-2.png) <br>
   ![Search Name](essential-comman-image/search-exp-3.png) <br>
   ![Search Name](essential-comman-image/) <br>
* `$ find -mmin +5` # Find files modified more than 5 minutes ago <br>
* `$ find -mmin -5` # Find files modified less than 5 minutes ago <br>
* `$ find -mmin 5` # Find files modified exactly 5 minutes ago <br>
* `$ find -cmin +5` # Find files created more than 5 minutes ago <br>
* `$ find -cmin -5` # Find files created less than 5 minutes ago <br>
* `$ find -cmin 5` # Find files created exactly 5 minutes ago <br>
* `$ find -amin +5` # Find files accessed more than 5 minutes ago <br>
* `$ find -amin -5` # Find files accessed less than 5 minutes ago <br>
* `$ find -amin 5` # Find files accessed exactly 5 minutes ago <br>
* `$ find / -type f -name file.txt` # Find a file in the filesystem <br>
* `$ find / -type d -name directory` # Find a directory in the filesystem <br>
* `$ find / -user user` # Find files owned by a user in the filesystem <br>
* `$ find / -group group` # Find files owned by a group in the filesystem <br>
* `$ find / -size +1G` # Find files larger than 1GB in the filesystem <br>
* `$ find / -size -1G` # Find files smaller than 1GB in the filesystem <br>
* `$ find / -size 1G` # Find files exactly 1GB in the filesystem <br>
* `$ find / -mtime +5` # Find files modified more than 5 days ago in the filesystem <br>
* `$ find / -mtime -5` # Find files modified less than 5 days ago in the filesystem <br>
* `$ find / -mtime 5` # Find files modified exactly 5 days ago in the filesystem <br>
* `$ find / -ctime +5` # Find files created more than 5 days ago in the filesystem <br>
* `$ find / -ctime -5` # Find files created less than 5 days ago in the filesystem <br>
* `$ find / -ctime 5` # Find files created exactly 5 days ago in the filesystem <br>
* `$ find / -atime +5` # Find files accessed more than 5 days ago in the filesystem <br>
* `$ find / -atime -5` # Find files accessed less than 5 days ago in the filesystem <br>
* `$ find / -atime 5` # Find files accessed exactly 5 days ago in the filesystem <br>
* `$ find / -name file.txt` # Find a file in the filesystem <br>
* `$ grep pattern file.txt` # Search for a pattern in a file <br>
* `$ ps` # Display the processes running on the system <br>
* `$ top` # Display the processes running on the system with a pager <br>
* `$ kill PID` # Terminate a process by its process ID <br>
* `$ killall process` # Terminate a process by its name <br>
* `$ shutdown -h now` # Shutdown the system immediately <br>
* `$ reboot` # Reboot the system <br>
* `$ df -h` # Display the disk usage <br>
* `$ du -h` # Display the disk usage of a directory <br>
* `$ free -h` # Display the memory usage <br>
* `$ uname -a` # Display the system information <br>
* `$ date` # Display the current date and time <br>
* `$ cal` # Display the calendar <br>
* `$ history` # Display the command history <br>
* `$ find / -name file.txt` # Find a file in the filesystem <br>
* `$ grep pattern file.txt` # Search for a pattern in a file <br>
* `$ ps` # Display the processes running on the system <br>
* `$ top` # Display the processes running on the system with a pager <br>
* `$ find -size [size]` <br>
* `$ find -size 512k]` # Find files exactly 512KB [k for kilobytes, M for megabytes, G for gigabytes] <br>
* `$ find -size +512k]` # Find files larger than 512KB <br>
* `$ find -size -512k]` # Find files smaller than 512KB\ <br>
* `$ find -name "f*" -size 512k`       #AND Operator <br>
* `$ find -name -o "f*" -size 512k`       #OR Operator <br>
* `$ find -not -name -o "f*"` # NOT Operator <br>
* `$ find \! -name -o "f*"` # alternate NOT Operator, here \ meaning to tell bash to ignore the special meaning of this characted and just consider it a regular character
* `$ find -perm 664` # find files with **exactly** 664 permission <br>
* `$ find -perm -664` # find files with **at least** 664 permission <br>
* `$ find -perm /664` # find files with **any of these** permission <br>
* `$ find -perm 600` # find owner can read and write with no other permission <br>
* `$ find -perm -100` # Find files that the owner can execute **at least** but the rest of the permission can be anything <br>
* `$ find \! -perm -o=r` # Nobody else can read these files except the user and group that own them  <br>
* `$ find -perm /u=r,g=r,o=r` # Find files that can only be read either by the user, the group, or others, It doesn't matter who it is, but at least  one of them should be able to read it.

**Compare and Manipulate File:**
* cat: Concatenate and display the content of files. <br>
* tac: Concatenate and display the content of files in reverse. <br>
* head: Display the first lines of files. <br>
* tail: Display the last lines of files. <br>
* sort: Sort the lines of files. <br>
* uniq: Display unique lines of files. <br>
* sdiff: Display the differences between two files. <br>
* sed: Stream editor for filtering and transforming text. <br>
* cut: Remove sections from each line of files. <br>

* `$ cat /linux_learn/country.txt` <br>
* `$ tac /linux_learn/country.txt` <br>
* `$ tail -n 20 /var/log/dnf.log` <br>
* `$ head -n 20 /var/log/dnf.log` <br>
* `$ sort /linux_learn/country.txt` <br>
* `$ sort -r /linux_learn/country.txt` # reverse order <br>
* `$ sort -n /linux_learn/country.txt` # numeric order <br>
* `$ sort -nr /linux_learn/country.txt` # numeric reverse order <br>
* `$ sort -k 2 /linux_learn/country.txt` # sort by second column <br>
* `$ sort -k 2 -r /linux_learn/country.txt` # sort by second column in reverse order <br>
* `$ sort -k 2 -n /linux_learn/country.txt` # sort by second column in numeric order <br>
* `$ sort -k 2 -nr /linux_learn/country.txt` # sort by second column in numeric reverse order <br>
* `$ sort -t : -k 2 /linux_learn/country.txt` # sort by second column with delimiter : <br>
* `$ sort -t : -k 2 -r /linux_learn/country.txt` # sort by second column in reverse order with delimiter : <br>

![Search Name](essential-comman-image/sed.png) <br>
![Search Name](essential-comman-image/sed-2.png) <br>
![Search Name](essential-comman-image/cut.png) <br>


**Search File:**
* `$ grep -i 'pattern' /etc/os-release` # case insensitive search <br>
* `$ grep -r 'pattern' /etc/` # recursive search <br>
![Search Name](essential-comman-image/recursive-grep-search.png) <br>
* `$ grep -w 'pattern' /etc/os-release` # whole word search <br>
* `$ grep –vi 'centos' /etc/os-release` # invert match <br>
![Search Name](essential-comman-image/word-grep-search.png) <br>
![Search Name](essential-comman-image/only-matching.png) <br>


Regex Operators:
^ # Start of the line
$ # End of the line
. # Any character
* # Zero or more occurrences
+ # One or more occurrences
{} # Range of occurrences
[] # Character class
() # Grouping
? # Zero or one occurrence
| # Alternation
[^] # Negation

`$ grep '^#' /etc/login.defs` # Means that we are looking for lines that start with a hash symbol.
`$ grep –v '^#' /etc/login.defs` # Means that we are looking for lines that do not start with a hash symbol.
`$ grep '^PASS' /etc/login.defs` # Means that we are looking for lines that start with the word PASS.
![Search Name](essential-comman-image/dollar-regex.png) <br>
![Search Name](essential-comman-image/match-any.png) <br>
`$ grep '.' /etc/login.defs` # 
`$ grep '\.' /etc/login.defs`
![Search Name](essential-comman-image/start-match.png) <br>
![Search Name](essential-comman-image/word-grep-search.png) <br>

**Extended Regular Expression:**
* `$ grep -E 'pattern' /etc/os-release` # extended regular expression <br>
![Search Name](essential-comman-image/extend-grep.png) <br>