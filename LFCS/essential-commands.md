# Linux Boot Process:

### **Boot Up Linux**
Booting up Linux refers to the process by which a Linux-based operating system is started from a powered-off state. This involves multiple stages, starting from the BIOS/UEFI firmware initialization, loading the Linux kernel, mounting the root filesystem, and finally launching the system's services and user interface.

---

## **🔹 The Linux Boot Process: Step-by-Step**
When you power on a Linux system, the boot process follows these stages:

### **1️⃣ BIOS/UEFI Initialization**
- The **BIOS (Basic Input/Output System)** or **UEFI (Unified Extensible Firmware Interface)** is the first software that runs when a computer is powered on.
- It performs **POST (Power-On Self-Test)** to check hardware components (CPU, RAM, disks).
- It searches for a bootable disk and loads the **bootloader** (GRUB, systemd-boot, etc.) from the Master Boot Record (MBR) or EFI partition.

### **2️⃣ Bootloader Execution (GRUB, systemd-boot, etc.)**
- The bootloader is responsible for **loading the Linux kernel into memory**.
- **Common Linux Bootloaders:**
  - **GRUB (GRand Unified Bootloader)** – Most widely used
  - **systemd-boot** – Used in systemd-based distributions
  - **LILO (Linux Loader)** – Older and rarely used today

- The bootloader provides:
  - A **menu** to select the kernel version (if multiple are installed).
  - Options to modify boot parameters (e.g., safe mode, recovery mode).
  - It loads the kernel and passes control to it.

### **3️⃣ Linux Kernel Initialization**
- The **Linux kernel** is the core of the operating system and handles:
  - Hardware communication (CPU, RAM, disk, network, peripherals)
  - Memory management
  - Process management (scheduling tasks)
  - Device drivers
- It mounts an initial **temporary filesystem (initramfs or initrd)** for loading essential drivers.

### **4️⃣ Initial RAM Disk (initramfs/initrd)**
- The **initramfs** (initial RAM filesystem) or **initrd** (initial RAM disk) is a small temporary root filesystem that helps the kernel load required drivers (e.g., filesystem, disk controllers).
- After loading necessary modules, the real root filesystem (`/`) is mounted.

### **5️⃣ System Initialization (init/systemd)**
- Once the root filesystem is mounted, the system's **init process** starts.
- Different init systems used in Linux:
  - **systemd** (Modern Linux distros like Ubuntu, RHEL, Fedora)
  - **SysVinit** (Older Unix-based distros)
  - **OpenRC** (Used in Alpine Linux, Gentoo)

- The init system performs:
  - Mounting additional filesystems
  - Setting up networking
  - Launching services like SSH, database servers, web servers

### **6️⃣ User Space Initialization (Login Prompt or GUI)**
- If running a **server**, you will see a **command-line login prompt** (`tty`).
- If running a **desktop environment (GNOME, KDE, XFCE)**, the system starts the **display manager** (GDM, LightDM, SDDM).
- After login, the **user session** starts, loading the desktop or terminal shell.

---

## **🔹 Linux Boot Process Diagram**
```
1. Power On
2. BIOS/UEFI -> Hardware Check (POST)
3. Bootloader (GRUB/systemd-boot) -> Select Kernel
4. Linux Kernel -> Load Device Drivers
5. initramfs/initrd -> Prepare Root Filesystem
6. Init System (systemd/SysVinit) -> Start Services
7. User Login (TTY or GUI)
```

---

## **🔹 Practical Real-Life Example**
Imagine you're a **DevOps Engineer** managing cloud servers. You may encounter:
- **A server fails to boot** after a kernel update.
- **A misconfigured service (Apache, MySQL) is preventing login**.

You can debug issues using:
1. **Check Boot Logs:**
   ```bash
   journalctl -b
   ```
2. **Reinstall GRUB Bootloader (if boot fails):**
   ```bash
   sudo grub-install /dev/sda
   sudo update-grub
   ```
3. **Restart a Failed Service:**
   ```bash
   sudo systemctl restart apache2
   ```

---

## **🔹 Summary: Why Is Booting Important?**
- **Ensures hardware & software are initialized correctly.**
- **Loads the kernel & essential drivers to interact with hardware.**
- **Starts system services required for operation (networking, database, SSH, etc.).**
- **Allows users to interact with the system via a shell or GUI.**

Would you like any specific details on troubleshooting Linux boot issues? 😊


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
**SUID** - when this is set on a file, it means that whenever the file is executed, it going to be executed as the User ID of the owner of the file Instead of the User ID of the person who is running the file.<br>
Capital **S** in the permission means that the file has the SUID permission but it is not executable. <br>
Small **s** in the permission means that the file has the SUID permission and it is executable. <br>
`$ chmod 4664 testsuidfile` <br>
`$ chmod 4764 testsuidfile` <br>
![Create Link](essential-comman-image/suid.png) <br>

`$ touch testsuidfile` <br>
`$ chmod 2664 testsuidfile` <br> 
`$ chmod 4664 testsuidfile` <br> #  
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

![Create Link](essential-comman-image/SUID.png) <br>
![Create Link](essential-comman-image/suid-ans.png) <br>


**Search for File:**
* / (slash mode): Matches **any** of the specified permissions. <br>
*  \- (dash mode): Matches **all** of the specified permissions. <br>
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

* `$ find -mmin 5` # Find files modified **exactly** 5 minutes ago <br>
* `$ find -cmin +5` # Find files created **more** than 5 minutes ago <br>
* `$ find -amin -5` # Find files accessed **less** than 5 minutes ago <br>
* `$ find / -type f -name file.txt` # Find a file in the filesystem <br>
* `$ find / -type d -name directory` # Find a directory in the filesystem <br>
* `$ find / -user user` # Find files owned by a user in the filesystem <br>
* `$ find / -group group` # Find files owned by a group in the filesystem <br>
* `$ find / -size +1G` # Find files larger than 1GB in the filesystem <br>
* `$ find / -mtime +5` # Find files modified **more** than 5 days ago in the filesystem <br>
* `$ find / -ctime -5` # Find files created **less** than 5 days ago in the filesystem <br>
* `$ find / -atime -5` # Find files accessed **less** than 5 days ago in the filesystem <br>
* `$ find / -name file.txt` # Find a file in the filesystem <br>
* `$ grep pattern file.txt` # Search for a pattern in a file <br>
* `$ ps` # Display the processes running on the system <br>
* `$ top` # Display the processes running on the system with a pager <br>
* `$ kill PID` # Terminate a process by its process ID <br>
* `$ killall process` # Terminate a process by its name <br>
* `$ reboot` # Reboot the system <br>
* `$ df -h` # Display the disk usage <br>
* `$ du -h` # Display the disk usage of a directory <br>
* `$ free -h` # Display the memory usage <br>
* `$ uname -a` # Display the system information <br>
* `$ grep pattern file.txt` # Search for a pattern in a file <br>
* `$ top` # Display the processes running on the system with a pager <br>
* `$ find -name "f*" -size 512k`       #AND Operator <br>
* `$ find -name -o "f*" -size 512k`       #OR Operator <br>
* `$ find -not -name -o "f*"` # NOT Operator <br>
* `$ find \! -name -o "f*"` # alternate NOT Operator, here \ meaning to tell bash to ignore the special meaning of this characted and just consider it a regular character
* `$ find -perm 664` # find files with **exactly** 664 permission <br>
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
* `$ tail -n 20 /var/log/dnf.log` <br> # Display the last 20 lines of a file <br>
* `$ head -n 20 /var/log/dnf.log` <br> # Display the first 20 lines of a file <br>
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

**SED: Stream Editor:**
* `$ sed 's/old/new/' file.txt` # Replace the first occurrence of a string in a file <br>
* `$ sed 's/old/new/g' file.txt` # Replace all occurrences of a string in a file <br>
* `$ sed 's/old/new/2' file.txt` # Replace the second occurrence of a string in a file <br>
* `$ sed 's/old/new/3g' file.txt` # Replace all occurrences starting from the third in a file <br>
* `$ sed 's/old/new/i' file.txt` # Replace the first occurrence of a string case-insensitive in a file <br>
* `$ sed 's/old/new/gi' file.txt` # Replace all occurrences of a string case-insensitive in a file <br>
* `$ sed 's/old/new/2i' file.txt` # Replace the second occurrence of a string case-insensitive in a file <br>
* `$ sed 's/old/new/3gi' file.txt` # Replace all occurrences starting from the third case-insensitive in a file <br>

![Search Name](essential-comman-image/sed.png) <br>
`sed` just showed what can do, but not edit the file. but if I want to edit the file, then I need to add -i (--in-place)
with the command. <br>
![Search Name](essential-comman-image/sed-2.png) <br>

![Search Name](essential-comman-image/serch-perm.png) <br>
![Search Name](essential-comman-image/search-perm-ans.png) <br>

**CUT Command:** <br>
`cut` command is used to extract part/sections from each line of file. By default, it treats each line of a file as a separate record and each field as a separate column. <br>
* `$ cut -c 1-5 file.txt` # Extract the first five characters of each line <br>
* `$ cut -d ' ' -f 1 file.txt` # Extract the first field of each line with a space delimiter <br>
* `$ cut -d ':' -f 1 file.txt` # Extract the first field of each line with a colon delimiter <br>
* `$ cut -d ',' -f 1 file.txt` # Extract the first field of each line with a colon delimiter <br>

unq: Display unique lines of files. <br>
* `$ uniq file.txt` # Display unique lines of a file <br>
uniq command has a limitation that it only removes adjacent duplicate lines. <br>
to solve this problem, we can use `sort` command before `uniq` command. <br>

![Search Name](essential-comman-image/uniq-and-sort.png) <br>

![Search Name](essential-comman-image/cut.png) <br>

Pager: A pager is a program that allows you to view the contents of a file one page at a time. <br>
Hold Shit + Press N -> To s

**Search File:**
* `$ grep -i 'pattern' /etc/os-release` # case insensitive search <br>
* `$ grep -r 'pattern' /etc/` # recursive search <br>
![Search Name](essential-comman-image/recursive-grep-search.png) <br>
* `$ grep -w 'pattern' /etc/os-release` # whole word search <br>
* `$ grep -wi 'password' /etc/ssh/sshd_config` # book and booking is not same word
* `$ grep –vi 'centos' /etc/os-release` # **invert** match <br>
![Search Name](essential-comman-image/word-grep-search.png) <br>
![Search Name](essential-comman-image/only-matching.png) <br>


**Regex Operators:**
* ^ --> Start of the line
* $ --> End of the line
* . --> Match any ONE character (period)
* \* --> Match the previous element Zero or more times
* \+ --> One or more occurrences
* {} --> Previous Element can exist "this many" times. Range of occurrences.
* [] --> Character class, Ranges Or Sets
* () --> Grouping
* ? --> Make the previous element optional. Zero or one occurrence
* | --> Alternation (vertical pipe), Match One Thing Or The Other
* [^] --> Negation

* `$ grep '^#' /etc/login.defs` # Means that we are looking for lines that start with a hash symbol. <br>
* `$ grep –v '^#' /etc/login.defs` # Means that we are looking for lines that do not start with a hash symbol. <br>
* `$ grep '^PASS' /etc/login.defs` # Means that we are looking for lines that start with the word PASS. <br>
![Search Name](essential-comman-image/dollar-regex.png) <br>
![Search Name](essential-comman-image/match-any.png) <br>
* `$ grep '.' /etc/login.defs` #  <br>
* `$ grep '\.' /etc/login.defs` <br>
* `$ grep 'let*' /etc/` # let, lett, lettt <br>
* `$ grep '/.*/' /etc/` # Begins with /; has 0 or more characters between; ends with a / <br>
![Search Name](essential-comman-image/start-match.png) <br>
![Search Name](essential-comman-image/star-match.png) <br>
![Search Name](essential-comman-image/plus-match.png) <br>
![Search Name](essential-comman-image/word-grep-search.png) <br>

**Extended Regular Expression:**
* `$ grep -E 'pattern' /etc/os-release` # extended regular expression <br>
![Search Name](essential-comman-image/extend-grep.png) <br>
![Search Name](essential-comman-image/prev-elem.png) <br>
* `$ egrep -r '0{min,max}' /etc/` # min and max are the minimum and maximum number of occurrences. <br>
* `$ egrep -r '0{2,4}' /etc/` # 0{2,4} means that we are looking for two to four zeros in a row. <br>
* `$ egrep -r '0{2,}' /etc/` # 0{2,} means that we are looking for two or more zeros in a row. <br>
* `$ egrep -r '0{,4}' /etc/` # 0{,4} means that we are looking for up to four zeros in a row. <br>
* `$ egrep -r '0{2}' /etc/` # 0{2} means that we are looking for exactly two zeros in a row. <br>
* `$ egrep -r 'disabled?' /etc/` #Make The Previous Element Optional <br>
* `$ egrep -r 'enabled|disabled' /etc/` # Alternation (vertical pipe), Match One Thing Or The Other <br>
* `$ egrep -r 'c[au]t' /etc/` # search the value of cat and cut <br>
* `$ egrep –r 'http[^s]' /etc/` # This command used for search the value of http but not https <br>


![Search Name](essential-comman-image/subexression.png) <br>
[RegEx](https://regexr.com)

## Reges Cheat Sheet:
![RegEx](essential-comman-image/grep/1.png)<br>
![RegEx](essential-comman-image/grep/2.png)<br>
![RegEx](essential-comman-image/grep/3.png)<br>
![RegEx](essential-comman-image/grep/4.png)<br>
![RegEx](essential-comman-image/grep/5.png)<br>
![RegEx](essential-comman-image/grep/6.png)<br>
![RegEx](essential-comman-image/grep/7.png)<br>
![RegEx](essential-comman-image/grep/8.png)<br>
![RegEx](essential-comman-image/grep/9.png)<br>
![RegEx](essential-comman-image/grep/10.png)<br>
![RegEx](essential-comman-image/grep/11.png)<br>
![RegEx](essential-comman-image/grep/12.png)<br>
<br><br>

**Packing Files and Directories With tar:** <br>

![Search Name](essential-comman-image/packing-file.png) <br>

![Search Name](essential-comman-image/packing-file-2.png) <br>

**Compression And Decompression With tar:** <br>

![Search Name](essential-comman-image/compressed-1.png) <br>
![Search Name](essential-comman-image/compressed-2.png) <br>
![Search Name](essential-comman-image/compressed-3.png) <br>

**Lab Task:** <br>
![Search Name](essential-comman-image/hardlink.png) <br>
![Search Name](essential-comman-image/soft-link.png) <br>

# Section - 2: Operations Deployment

## Boot, Reboot and Shutdown a system safely:
To reboot or shutdown a linux machine, will often use the `systemctl` command.
* `$ systemctl reboot` # Reboot the system <br>
* `$ systemctl poweroff` # Shutdown the system <br>

### Mange Startup process and Service:

**systemd unit:** A unit is a configuration file that describes how a service, socket, device, mount point, or other resource should be managed by systemd. <br>
systemd is the the collection of tool, components and application that help to start, operate, manage most of the Linux based OS. <br>

![Systemd](od/systemd-units.png) <br>

Long story short, systemd is a system and service manager for Linux operating systems. It is designed to be backwards compatible with SysV init scripts, and provides a number of features such as parallel startup of system services at boot time, on-demand activation of daemons, support for system state snapshots, or dependency-based service control logic. <br>
systemd is the name of a large collection of tools and components but aalso the name of the application  that is reponsible for system initialization and monitoring the system as a whole to ensure smooth operation. <br>

**service unit:** A service unit is a type of systemd unit that controls a service. service unit have clear instructions about such things as what command to issue to start the service,  stop the service, restart the service and what to do if a program crashes so on<br>
**socket unit:** A socket unit is a type of systemd unit that controls a socket. <br>
**device unit:** A device unit is a type of systemd unit that controls a device. <br>
**mount unit:** A mount unit is a type of systemd unit that controls a mount point. <br>
**target unit:** A target unit is a type of systemd unit that groups other units together. <br>
**snapshot unit:** A snapshot unit is a type of systemd unit that represents a saved state of the system. <br>
**timer unit:** A timer unit is a type of systemd unit that controls a timer. <br>

![Systemd](od/startup-process-1.png) <br>
![Systemd](od/ssh-service.png) <br>
so, systemd service is the responsible for the lifecycle of the ssh daemon.<br>
![Systemd](od/startup-process-2.png) <br>
Here, we can see, If this service is enabled, that means the systemd will automatically start the ssh daemon when the system boots up. <br> 
disabled means it wont automatically start up, but it can be manually started by the administrator. <br>

`$ sudo systemctl stop sshd.service` # Stop the sshd service <br>
`$ sudo systemctl start sshd.service` # Start the sshd service <br>
`$ sudo systemctl restart sshd.service` # Restart the sshd service <br>
`$ sudo systemctl reload sshd.service` # Reload the sshd service <br>
`$ sudo systemctl reload-or-restart sshd.service` # Reload or restart the sshd service<>
`$ sudo systemctl disable sshd.service` # Disable the sshd service <br>
`$ sudo systemctl status sshd.service` # Display the status of the sshd service <br>
`$ sudo systemctl is-enabled sshd.service` # Check if the sshd service is enabled <br>
`$ sudo systemctl enable sshd.service` # Enable the sshd service <br>
`$ sudo systemctl is-active sshd.service` # Check if the sshd service is active <br>
`$ sudo systemctl list-units --type=service` # List all services <br>
`$ sudo systemctl enable --now sshd.service` # 
`$ sudo systemctl disable --now sshd.service` # 
![Systemd](od/startup-process-3.png) <br>

[Real Life Use of Systemd](od/systemd-lab.md)


## Diagnose and Manage Processes
Whenever we launch a program, It lives as a so-called process, on the opreting system. <br>

* `$ ps aux`  # Display all processes <br> a=all. u = user oriented format, x = extemnded format <br>
* `$ ps -e` # Display all processes <br>
* `ps u -U Tuhin`  # If we want to see the processes that have been started by the user Tuhin, u for user oriented format, U for user <br>
* `pgrep -a syslog` # Search for processes related to "syslog", Now sometimes we will want to explore processes that have a specific name to search for any process that contains the word syslog in its name. For instance, we can use `pgrep` or process grep. <br>

Now in Linux, there's this concept of process niceness. Niceness is a way to tell the Linux kernel how nice a process is to other processes. <br>

The niceness value can be a number between -20 and 19. The lower the number, the less nice it is. In other words, a lower number means a higher priority.<br>

Story: Consider `process-A` with a nice value of -20 and `process-B` with a nice value of 19. If both of these are running at the same time, we need to use all CPU resources available. Process-A will leave very little available for process-B. A might use up CPU 95 to 99% of the time, while B will get very little CPU time, only when there's something left to spare. <br>

We'll want important processes to have higher priority, which means we will assign them lower nice values. <br> There are two ways this can be done. <br>
1. At launch time : nice -n [NICE_VALUE] [COMMAND] <br>
`$ nice -n 11 bash` <br> check by `$ ps l` or  `$ ps lax` <br> by NI column.
2. After launch time : renice -n [NICE_VALUE] -p [PID] <br>

Our `nice n 11 bash` command started a new bash shell And we can see that the `ps lax` command inherited the nice value of our bash shell. That's because all processes inherit the niceness of their parent process, the one that launched them. <br>
![Systemd](od/ps-lax.png) <br>

To see which processes are parents for other processes, we can add the f option, which stands for force display because it shows us tree like branches for this child parent relationship.<br>
* `$ ps fax` # Display all processes in a tree-like format <br>
* `$ pstree` # Display all processes in a tree-like format <br>
* `$ pstree -p` # Display all processes in a tree-like format with PIDs <br>
* `$ pstree -p | grep sshd` # Display all processes in a tree-like format with PIDs and filter the output with grep <br>

<br><br>
If we also want to see CPU usage, memory usage, and the columns we're used to, we can throw the U option in here. The order of the f, u x letters is not important.

* `$ ps faxu` # Display all processes in a tree-like format with user-oriented format <br>

Now regular user can only assign nice values between *0 and 19*, To assign lower values for higher priority. We need to use root privileges.<br>
* `$ sudo nice -n -12 bash` # Start a new bash shell with a nice value of -12 <br>

Now the problem with the command `sudo nice dash -n -12 bash` is that it also started our bash shell as the root user.<br>
![Systemd](od/bash-root.png) <br>

* Regular users cannot lower the nice value of a process that it currently has, only root can lower process niceness. <br>

* Linux has this concept of sending processes, so-called signals. These are like high priority messages that tell the process, hey, stop what you're doing. We have the special request for you, but an application can only act on a specific signal if it was programmed to respond to that signal. The only exceptions are signals like **SIGSTOP** and **SIGKILL**. These cannot be ignored by the process. <br>

Now backgrounding and foregrounding processes pausing and exiting. some commands can take a long time to finish their job.
* Ctrl + Z for program pause vim/vi editor. it does not make any progress with its work. It's entirely frozen.
* again type fg to return to the editor. <br>

![Systemd](od/bg-fg.png) <br>

Sometimes we'll want to see what files or directories a process is currently using. First let's find the PID of our bash shell using `pgrep -a bash`. Our PID in this case is 13536. And if you're following along, of course it'll be different. Now to see what files or directories our bash process with PID 13536 is using. <br>

* `$ lsof -p 13536` # List all files and directories a process is using <br>


## Locate and Analyze System Log Files

Linux operating systems are largely server oriented, and on a server you always want to know what happened, who did what, what worked, what didn't work, what errors were encountered, who accessed the system, and so on. Everything important that happens on a Linux system is saved as a text message somewhere, which are called logs. <br>

The Linux kernel and most programs that run on the Linux operating system generate status messages. Error messages, warnings, and so on. There can be tens of different programs generating these messages all the time, so we need a way to collect all of these and organize them nicely into files. And this is the job of **Logging daemons**. This are simply applications that collect, organize and store logs. The most popular one on Linux is  **rsyslog**, and its name comes from Rocket-Fast System for log processing. **ryslog** stores all logs in the `/var/log/` directory.<br>c
![Systemd](od/logging-daemon.png) <br>

Since these are usually regular text files, you can search through them with grep commands or any of the other text oriented utilities that we've learned about. One **important** thing though most of these files cannot be read by regular users.

* `$ which sudo` # Find the location of a command <br>
* `$ journalctl /bin/sudo` # View the syslog file <br>

![Systemd](od/journalctl-summary.png) <br>


## Schedule task to Run at a Set Date and Time:

The **cron** utility is well suited for repetitive jobs that execute once every few minutes or hours, or on specific days or specific times. **Anacron** is also used to create repetitive jobs, but with a few differences. One is that it cannot repeat those jobs every few minutes or hours. The smallest unit it can work with is a day, so it can run a job every day, or every three days, or every week, or even every month or year. But it cannot run a job multiple times per day, just once per day. This utility has been created because cron can miss jobs if the computer is not powered on all the time. For example, if a job is set to run daily at noon and the computer is powered on at 12:01, that job won't run for that day. Anacron, on the other hand, will check if that job for today ever got a chance to run. If it didn't, it will execute it no matter when the system was powered on.



## Manage Software With Package Manager

* `$ dpkg -l` # Display all installed packages <br>
* `$ dpkg -l | grep apache` # Display all installed packages and filter the output with grep <br>
* `$ dpks --listfiles nginx` # Display the files in the nginx <br>
* `$ dpkg --search /usr/sbin/nginx` # Search for a file in the package database <br>
* `$ apt show libnginx-mod-stream` # If we curious about the purpose of a certain package <br>
* `$ apt search --names-only apache` # to lookup all the packages that mention the word apache <br>
* `$ apt search apache module image` # the search function must match all of these words <br>
* `$ sudo apt remove nginx` # remove the package, but the dependencies are sometimees still left  <br>
* `$ sudo apt autoremove nginx` # remove the package and the dependencies that are no longer needed <br>

## Configure the repositories of Package manager:

**main:** This components contains packages that are free and opensources and are officially supported by ubuntu.
**restricted:** free and opensource but may have restrictions on their use or redistribution. 
**universe:** free and opensources but not officially supported by ubuntu.
**multiverse:** not free and opensources and may have other licencing restrictions.

we basically need `main` and `universe`.

## Install Software by Compiling Source Code:

## Create and Enfoforce MAC using SELinux
* sudo systemctl statuse apparmor
    5  sudo systemctl status apparmor
    6  sudo systemctl stop apparmor
    7  sudo systemctl status apparmor
    8  clear
    9  sudo apt install selinux-basics auditd
   10  sudo apt update
   11  sudo apt upgrade
   12  sudo apt install selinux-basics auditd
   13  sestatus
   14  ls -Z /
   15  sudo selinux-activate
   16  sestatus
   17  cat /etc/default/grub
   18  ls -a /
   19  sudo reboot
   20  client_loop: send disconnect: Broken pipe
   21  clear
   22  ls -Z /
   23  ll
   24  sestatus
   25  getinforce
   26  get inforce
   27  getenforce

SELinux is enables 2way: Enforcing and Permissive way

Enforcing: SELinux is enabled and actively enforcing the security policy. <br>
Permissive: SELinux is enabled but not enforcing the security policy. Its observing actions of our system passively <br>


# Networking
**Lecture: Configure IPv4 and IPv6 Networking and Hostname Resolution - Demo**

* `$ ip addr` # Display the IP address <br>
* `$ ip link` #Display the network interface in the device  <br>
* `$ sudo ip link set dev enp1s0 up` # Enable the network interface **enp1s0**<br>
* `$ sudo ip link set dev enp1s0 down` # Disable the network interface **enp1s0**<br>
* `$ sudo ip addr add 10.0.0.40/24 dev enp1s0` # Assign an IP address to the network interface **enp1s8**<br>
Note that: A Network Interface can have multiple IP addresses. <br> To remove IP address from a network interface, we can use the `del` option. <br>
* `$ sudo ip addr del IP_ADDRESS/CIDR dev NETWORK_INTERFACE` # Remove an IP address from a network interface <br>

These are temporary configurations. How do we make it permanent? <br> It depends on the Operating System. <br>
Default network tools have been changed a lot in the past. <br>
Ubuntu currently uses the `netplan` tool to configure network interfaces. <br> This is a set of utilities that reads some configuration files then sends instructions to other networking tools telling them to configure network setting accordingly.<br> 
On the Ubuntu Server Edition, NetPlan send instructions to `systemd-networkd` daemon called Systemd-Network to configure network settings. <br>

So kets see how we can instruct NetPlan to assign some IPs for our devices.<br>
To see the current NetPlan Configuration file, we can type `sudo netplan get`.

* `$ sudo netplan get` # Display the current NetPlan configuration <br>
* `$ sudo cat /etc/netplan/50-cloud-init.yaml` # read the NetPlan configuration file <br>
* `$ sudo nano /etc/network/interfaces` # Edit the network configuration file <br>
we'll copy this text and use it as a template in our new file. Now, let's remember the name of the device that we want to configure. And let's create a new Netplan YAML file.

```99-my-settings.yaml
network:
  version: 2
  ethernets:
    enX0:
      match:
        macaddress: "02:10:03:ea:38:83"
      dhcp4: true
      dhcp6: false
      set-name: "enX0"
```

Its standard practice to prefix the file with a number. This is because the files are read in order. <br>
netplant will process yaml files in this directory in alphabetical order. <br>
* `$ sudo netplan apply` # Apply the NetPlan configuration <br>
* `$ sudo netplan --debug apply` # Apply the NetPlan configuration in debug mode <br>
* `$ sudo netplan try` # Try the NetPlan configuration <br>\
* `$ sudo netplan try --timeout=10` # Try the NetPlan configuration with a timeout <br>
* `$ sudo ip route` # Display the routing table <br>

`sudo vim /etc/netplan/99-mysettings.yaml `<br>
```/etc/netplan/99-mysettings.yaml
network:
  version: 2
  ethernets:
    enp0s8:
      dhcp4: false
      dhcp6: false
      addresses:
        - 10.0.0.9/24
      nameservers:
        addresses:
          - 8.8.4.4
          - 8.8.8.8
        routes:
          - to: 192.168.0.0./24
            via: 10.0.0.0.100
          - to: default
            via: 10.0.0.1
```

then apply our setting by:  `$ sudo netplan try`

* `$ resolvectl dns` # Display the DNS configuration <br>

#### Important
`$ man netplan `
**to read further /usr/share/doc/netplan/examples/ <br>**

### Start, Stop and Check the status of Network Services:
Check Slide:

### Bridge and Bond Devices Configuration.
Check SLide:
## Configure Bridge and Bonding Devices.
### Configure Bridge Devices:
1. First, check the `bridge.yml` file in `ls /usr/share/doc/netplan/examples/`
2. From this exmaples folder, we can copy the `bridge.yml` file to `/etc/netplan/` folder.
      * `sudo cp bridge.yaml /etc/netplan/99-bridge.yaml`
      * change the permission of the file by `sudo chmod 600 /etc/netplan/99-bridge.yaml`
3. Edit the file by `sudo vim /etc/netplan/99-bridge.yaml` and add the following content:

```
99-bridge.yaml
network:
  version: 2
  renderer: networkd
  ethernets:
    enp3s0:
      dhcp4: no
  bridges:
    br0:
      dhcp4: yes
      interfaces:
        - enp3s0 # This is the interface-1 that will be bridged
        - enp4s0 # This is the interface-2 that will be bridged
  ```

then apply our setting by:  `$ sudo netplan try`

If we want to delete the Bridge configuration, then we can delete the file from the `/etc/netplan/` folder and then apply the setting by `sudo netplan try`
then delete the bridge interface: `sudo ip link delete br0`

### Configure Bonding Devices:
1. First, check the `bonding.yaml` file in `ls /usr/share/doc/netplan/examples/`
2. From this exmaples folder, we can copy the `bonding.yaml` file to `/etc/netplan/` folder.
      * `sudo cp bonding.yaml /etc/netplan/99-bonding.yaml`
      * change the permission of the file by `sudo chmod 600 /etc/netplan/99-bonding.yaml`
See the additional details of bond: `cat /proc/net/bonding/bond0`

### Configure a Packet Filtering (Firewall) in a Ubuntu Machine:
**Uncomplicated Firewall (ufw)**

Before we continue, we must make sure to add at least one rule that allow SSH traffic. Otherwise, when we enable UFW, we ownt be able to login through SSH anymore. <br>
This happens because UFW blocks all incoming traffic by default. this is called whitelist approach. <br>
* `$ sudo ufw status` # Display the status of the firewall <br>

lets create our first rule. To enable incoming network packets on port 22 (SSH) <br>
* `$ sudo ufw allow 22` # Allow incoming network packets on port 22 <br>
This will allow connection on both TCP and UDP. SSH uses TCP <br>

Now we can enable UFW by typing 
* `$ sudo ufw enable` <br>
* `$ sudo ufw status verbose` <br>
* `$ sudo ufw allow 53/tcp` <br> # Allow incoming network packets on tcp port 53 <br>

check Local Address and Peer address port
`$ ss -tn ` # 
we can create rule to only allow incoming traffic to port 22

* `$ sudo ufw allow from 10.0.0.192 to any port 22` # Allow incoming network packets from 10.0.0.192 to any port 22 <br>
Now this keyword `any` is necessary here Because when we specify the IP address of the sender, which is from, UFW also wants to know the IP address of the receiver, which is too. By typing in any, we say that this can come to any IP address of this machine. Since the server can have multiple network cards and multiple IPs, if we want to accept traffic only on a certain IP of this machine, we just replace the word any with that actual IP address. But now we have a problem with our rules.

To understand the problem, we can type `sudo ufw status numbered` <br>

* `$ sudo ufw delete 2` # Delete the rule with the number 2 <br>
* `$ sudo ufw delete allow 22` # Delete the rule that allows incoming network packets on port 22 <br>

* `$ sudo ufw allow from 10.0.0.0/24 to any port 22` # Allow incoming network packets from the  10.0.0.0/24 network to any port 22 <br>

* `$ sudo ufw allow from 10.0.0.0/24` # Allow incoming network packets from the 10.0.0.0/24 network  will allow all ports<br>

But let's go one step further. What if we want to accept traffic from all IPs in this range except for one of them? For example, maybe we want to disallow traffic coming from 10.0.0.37. For this purpose, instead of an allow rule, we can add a deny rule. <br>

* `$ sudo ufw deny from 10.0.0.37` # Deny incoming network packets from 10.0.0.37 <br>

However, there will be a problem here. Let's take another look at the current rules.
* `$ sudo ufw status numbered` <br>

And let's remove the first two rules here to simplify the explanation of the problem.
* `$ sudo ufw delete 1`
Okay, we'll type in sudo ufw delete 1. And then we'll run the same command again. Because after we delete the first rule, rule number 2 becomes rule number 1. And rule number 3 becomes rule number 2. And as you can see here, they've all moved up one level.
* `$ sudo ufw delete 1` <br>
Now list of Rules again by `sudo ufw status numbered` <br>

![Network Image](net-img/img-1.png) <br>

here is the problem. because 10.0.0.37 IP exist in  10.0.0.0/24 range, so it will be allowed. <br> To Solve this problem we have to keep denied rule first.

inser rule sung numbered serial:
* `$ sudo ufw insert 1 deny from 10.0.0.37` # Deny incoming network packets from 10.0.0.37 <br>
**By default Firewall Rules processed in order.** <br>

* `$ sudo ufw deny out on enp0s8 to 8.8.8.8` # Deny outgoing network packets on the enp0s8 interface to 8.8.8.8 <br>

now try ping to 8.8.8.8, it will not work. <br>

![Network Image](net-img/img-2.png) <br>

When filtering incoming data, **TO** refers to a destination on this machine, namely on what IP of our machine that this is coming to. And **FROM** refers to the sender, the IP of the external machine that sent this to us. <br>

But when we filter outgoing data, this is reversed. Now, the first **TO** columns do not refer to an IP of our machine, but to an external IP of a different machine. And **FROM** refers to an IP of our machine. If this seems a bit complicated, just think about sending an email. When you receive an email in the To field, people fill out your own email address. But when you are sending an email, the To field refers to a different person, an email address belonging to someone else. Same here, as the receiver the **TO** field refers to this machine. As a sender, the **TO** field refers to a different machine. <br><br>

Lets Build our most complex UFW command where we specify all the details we learned about. <br>

First, let's see an IP address belonging to this machine as we'll use it in our command. It will be 10.0.0.100 in this case.

Now, let's build our command. We'll start with the sudo ufw allow and then type IN to specify that this applies to incoming data ON ENP0S3 to specify this applies to the ENP0S3 interface. Then we continue with FROM 10.0.0.192 to specify the sender's IP address. Then we'll add TO 10.0.0.100 to allow traffic on this IP of our machine. And finally, we'll specify the port and protocol. But we can't type in 80/tcp as we did for a previous command. When we fine-tune the FROM and TO IP addresses in this rule, we need a different approach.

* `$ sudo ufw allow **in** on ENP0S3 from 10.0.0.192 to 10.0.0.100 proto tcp` # Allow incoming network packets on the ENP0S3 interface from 10.0.0.192 to 10.0.0.100 

First, we type the usual port 80, but then we follow this with PROTO TCP to specify the TCP protocol. And for a rule with outgoing traffic, we just change the IN keyword to OUT. But remember, in this case, we apply a rule for our machine as a sender, not a receiver. So we have to reverse the FROM and TO specifications. <br><br>
 
 
So our rule for outgoing traffic would be. 

* `$ sudo ufw allow **out** on ENP0S3 from 10.0.0.100 to 10.0.0.192 proto tcp`

We'll switch the IP addresses here. So it would be sudo ufw allow out on ENP0S3 from 10.0.0.100 to 10.0.0.192 proto tcp. <br>

Now, with `sudo ufw status numbered`, we can see that the rules were added successfully. <br>
![Network Image](net-img/img-3.png) <br>

So if you remember the syntax for these longer UFW commands, you can basically build any rule you want. Even if you forget the syntax, the manual for UFW offers plenty of example commands to serve as a quick reminder.

## Port Redirection and Network Address Translation:
**Port Redirection:** Port redirection is a technique that allows us to redirect incoming traffic on a specific port to a different port. <br>
**Network Address Translation:** Network Address Translation is a technique that allows us to change the source or destination IP address of a packet. <br>



# Configure SSH Servers and Clients:
