### Login to Local, Remote Graphical and Text Mode:

SSH: Secure Shell (SSH) is a cryptographic network protocol for operating network services securely over an unsecured network. The best known example application is for remote login to computer systems by users.

Telnet: Telnet is a network protocol used on the Internet or local area networks to provide a bidirectional interactive text-oriented communication facility using a virtual terminal connection.

but SSH is more secure than Telnet because it uses encrypted communication.
`$ ip link` - is used to check the network interfaces.
`$ ip addr` - is used to check the IP address of the network interfaces.
`$ ssh username@ipaddress` - is used to login to the remote machine.
`$ telnet ipaddress` - is used to login to the remote machine.
`$ ip a` - is used to check the IP address of the network interfaces.

Computer(SSH Client) -> Server(SSH Daemon)

## Essentials Commands:
* **Create, Delete, Copy and Move files and directories:**

`$ ls -la `  #**l**ist **a**ll files and directories in the current directory.
`$ ls -lah` # h for human redable i.e 6238 to 6.2KB

1  2     3    4     5  6                 7                    8    9  10  11   12 
d**rwx**r-x**r-x**  2 root              root                 4096 Feb  5 07:02 cups
1 # disk type / entry type
![Create Link](essential-comman-image/file-type.png) <br>
2 # permissions for the owner
3 # permissions for the group
4 # permissions for everyone else
![Create Link](essential-comman-image/permission.png) <br>

5 # number of hard links
6 # owner
7 # group
![Create Link](essential-comman-image/evaluating-permission.png) <br>
![Create Link](essential-comman-image/adding-permission.png) <br>
![Create Link](essential-comman-image/remove-permission.png) <br>
![Create Link](essential-comman-image/exact-permission.png) <br>
![Create Link](essential-comman-image/octal-permission.png) <br>
![Create Link](essential-comman-image/octal-permission-2.png) <br>
8 # size
9 # date and time of last modification
10 # name
11 # -> link
12 # 

**File and directory access:**

To access a file or directory on our command line and specify its file path or its directory path. 
1. **Absolute path:** The absolute path is the full path to a file or directory starting from the root directory. Its starts with root directory that represented by a forward slash (/) .
2. **Relative path:** The relative path is the path to a file or directory starting from the current directory. 
To understand a relative path we must explore what the current directory means. this also means the working directory.
now to see our working directory, we can type `pwd` command. 


`$ cd /etc` # Change directory to /etc
`$ cd ..` # Change directory to the parent directory
`$ cd ~` # Change directory to the home directory
`$ cd -` # Change directory to the previous directory
`$ pwd` # Print the current working directory
`$ cd ..` #always refer to parent directory of our current directory
`$ cd /` # Go to root directory

`$ touch file.txt` # Create a new file
`$ mkdir directory` # Create a new directory
`$ cp file.txt file2.txt` # Copy a file
`$ cp -r directory directory2` # Copy a directory
`$ mv file.txt file2.txt` # Move a file
`$ mv directory directory2` # Move a directory
`$ rm file.txt` # Remove a file
`$ rm -r directory` # Remove a directory
`$ ls -lrt` # List files and directories in reverse order of modification time
`$ ls -l | grep file` # List files and directories and filter the output with grep
`$ cat file.txt` # Display the content of a file
`$ less file.txt` # Display the content of a file with a pager
`$ head file.txt` # Display the first lines of a file
`$ tail file.txt` # Display the last lines of a file
`$ wc file.txt` # Count the number of lines, words, and characters in a file
`$ chmod 755 file.txt` # Change the permissions of a file
`$ chown user:group file.txt` # Change the owner and group of a file
`$ ln -s file.txt link.txt` # Create a symbolic link to a file
`$ ln -s directory link` # Create a symbolic link to a directory
`$ find / -name file.txt` # Find a file in the filesystem
`$ grep pattern file.txt` # Search for a pattern in a file
`$ ps` # Display the processes running on the system
`$ top` # Display the processes running on the system with a pager
`$ kill PID` # Terminate a process by its process ID
`$ killall process` # Terminate a process by its name
`$ shutdown -h now` # Shutdown the system immediately
`$ reboot` # Reboot the system
`$ df -h` # Display the disk usage
`$ du -h` # Display the disk usage of a directory
`$ free -h` # Display the memory usage
`$ uname -a` # Display the system information
`$ date` # Display the current date and time
`$ cal` # Display the calendar
`$ history` # Display the command



**Create and Manage Hard Link:**

File system like XFS, ext4 and other keep track of data with the help of inodes.
Inodes are data structures that store metadata about files and directories, such as their permissions, size, and location on the disk.
When we create a file or directory, the file system allocates an inode to it and stores the file or directory data in blocks on the disk.
suppose my *dummy.pdf* might have blocks of data scattered all over the disk, but inode remembers where all the blocks are stored.

![Create Link](essential-comman-image/inodes.png) <br>

File Point to the Inode -. Inodes points to the all of the blocks of data we required.
example: `stat dummy.pdf` 

![Create Link](essential-comman-image/links.png) <br>

![Create Link](essential-comman-image/hard-links.png) <br>

If aaron delelte the image:

![Create Link](essential-comman-image/one-side-hard-link-deletepng) <br>

Limitations of Hard Links:
1. Hard links for files, not directories.
2. Only Hard links within the same file system.
3. External mounted drive (/mnt/Backups/files) can't be hard linked from (/ssd/home/file)

Considerations when hard link:
1. Make sure you have the proper permissions to create the link file at the destination.
2. Make sure that all users involved have the proper permissions to access the file.
i.e for two user *John* and *Aaron*, this might mean that we need to add both their username to the same group for example family group then we would use a command to let the group family read anf write to this file.
remember you only need to change permission on of the hard links. That's because you are actually changing permission stored y the INode

`$ useradd -a -G family John` # Add a user to a group
`$ useradd -a -G family Aaron` # Add a user to a group
`$ chown :family file.txt` # Change the group of a file
`$ chmod 660 /home/aaron/Pictures/family_dog.jpg` # Change the permissions of a file


**Create and Manage Soft Link:**
* computer shortcuts
* Softlink is nothing more than a file that points to a path.
* Symbolic link



`$ ln file.txt link.txt` # Create a hard link to a file
`$ ln directory link` # Create a hard link to a directory
`$ ls -i file.txt link.txt` # Display the inode number of a file
`$ find / -inum inode_number` # Find a file by its inode number
`$ rm file.txt` # Remove a file
`$ rm link.txt` # Remove a hard link
`$ rm -i file.txt` # Remove a file with confirmation
`$ rm -f file.txt` # Remove a file without confirmation
`$ rm -r directory` # Remove a directory
`$ rm -rf directory` # Remove a directory without confirmation
`$ rm -i link.txt` # Remove a hard link with confirmation
`$ rm -f link.txt` # Remove a hard link without confirmation
`$ rm -i directory` # Remove a directory with confirmation
`$ rm -rf directory` # Remove a directory without confirmation
`$ ls -l` # List files and directories
`$ ls -lh` # List files and directories with human-readable sizes
`$ ls -lS` # List files and directories by size
`$ ls -lt` # List files and directories by modification time
`$ ls -lR` # List files and directories recursively
`$ ls -la` # List all files and directories
`$ ls -l | grep file` # List files and directories and filter the output with grep
`$ ls -l | sort -k 5` # List files and directories and sort the output by the fifth column
`$ ls -l | sort -k 5 -r` # List files and directories and sort the output by the fifth column in reverse order
`$ ls -l | sort -k 5 -n` # List files and directories and sort the output by the fifth column numerically
`$ ls -l | sort -k 5 -nr` # List files and directories and sort the output by the fifth column numerically in reverse order
`$ ls -l | sort -k 5 -n | head -n 5` # List files and directories and sort the output by the fifth column numerically and display the first five lines
`$ ls -l | sort -k 5 -n | tail -n 5` # List files and directories and sort the output by the fifth column numerically and display the last five lines
`$ ls -l | sort -k 5 -n | head -n 5 | tail -n 3` # List files and directories and sort the output by the fifth column numerically and display the first five lines and the last three lines
`$ ls -l | sort -k 5 -n | head -n 5 | tail -n 3 | wc -l` # List files and directories and sort the output by the fifth column numerically and display the first five lines and the last three lines and count the number of lines
`$ ls -l | sort -k 5 -n


**18. List, Set and Change Standard File Permission:**
* Only the Owner of a file or directory can change permission 
* Root user can change permission of any file or directory
* To change the group of a fileor directory we can use the `chgrp` command
* To change the owner of a file or directory we can use the `chown` command
