# Linux for Beginners:
===================


## Essentials Commands:
* **Create, Delete, Copy and Move files and directories:**

`$ ls -la `  #**l**ist **a**ll files and directories in the current directory.
`$ ls -lah` # h for human redable i.e 6238 to 6.2KB

1  2     3    4     5  6                 7                    8    9  10  11   12 
d**rwx**r-x**r-x**  2 root              root                 4096 Feb  5 07:02 cups
1 # disk type
2 # permissions for the owner
3 # permissions for the group
4 # permissions for everyone else
5 # number of hard links
6 # owner
7 # group
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

`$ touch file.txt` # Create a new file
`$ mkdir directory` # Create a new directory
`$ cp file.txt file2.txt` # Copy a file
`$ cp -r directory directory2` # Copy a directory
`$ mv file.txt file2.txt` # Move a file
`$ mv directory directory2` # Move a directory
`$ rm file.txt` # Remove a file
`$ rm -r directory` # Remove a directory