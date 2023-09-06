# linux-essentials
This repo covers all essential commands, which will be handy if you are wirking on a linux machine

## Topics Covered
- [Understanding permissions in linux](#understanding-permissions-in-linux)
  - [Changing file permissions](#changing-file-permissions)
  - [Understanding Users and Groups](#understanding-user-and-groups)
- [Increase decrease swap memory](#increase-decrease-swap-memory)
- <a href="https://humanwhocodes.com/snippets/2021/03/create-user-linux-ssh-key/"> Creating a new user with an SSH key on Linux <a/>
- [Changing ownership of a file](#changing-ownership-of-a-file)
- Exploring Symlink
  

<a id="understanding-permissions-in-linux"></a>
## Understanding permissions in linux
  In Linux, file permissions are a way to control access to files and directories. They determine who can read, write, and execute a file or directory. Understanding permissions is crucial for managing security and controlling access to sensitive data.

  Each line corresponds to a file contained within the directory. The information can be broken down into fields separated by spaces. The fields are as follows:


  
 ```
  -rw-r--r-- 1 root   root  18047 Dec 20  2017 alternatives.log       
            
  drwxr-x--- 2 root   adm    4096 Dec 20  2017 apache2  
  ```
  
  The first field actually contains ten characters, where the first character indicates the type of file and the next nine specify permissions. The file types are:
  
  ```
Symbol	File Type	Description
d	directory	A file used to store other files.
-	regular file	Includes readable files, images files, binary files, and compressed files.
l	symbolic link	Points to another file.
s	socket	Allows for communication between processes.
p	pipe	Allows for communication between processes.
b	block file	Used to communicate with hardware.
c	character file	Used to communicate with hardware.
```
  
Linux file permissions consist of three basic permissions: read (r), write (w), and execute (x). These permissions are assigned to three different categories of users: the owner of the file, the group associated with the file, and others (everyone else).

Here's a breakdown of how file permissions work:

Read (r): Allows the user to view the contents of a file or list the files within a directory. For directories, read permission is necessary to access file names inside it.

Write (w): Enables the user to modify the contents of a file or delete the file itself. For directories, write permission allows creating, deleting, and renaming files within it.

Execute (x): Grants the user the ability to execute a file (if it is a program or script) or access a directory. For directories, execute permission is necessary to navigate into the directory and access files inside it.

Permissions are represented using a 10-character string. The first character indicates the file type (e.g., "-" for regular files and "d" for directories). The next three characters represent the owner's permissions, followed by the group's permissions, and finally, the permissions for others.

Each set of permissions consists of three characters. The characters can be one of the following:

`r` for read permission.
`w` for write permission.
`x` for execute permission.
`-` to indicate no permission.

For example, consider the permission string `rw-r--r--`. Here, the owner has read and write permissions, while the group and others have only read permissions.
To view the permissions of a file or directory, you can use the `ls -l` command in the terminal. The output will display the permissions along with other information about the file or directory.

To modify permissions, you can use the chmod command. It allows you to add or remove permissions for the owner, group, and others. For example, chmod +x filename adds execute permission for the file's owner, group, and others.

<a id="changing-file-permissions"></a>
### Changing file permissions
  
  To give a user read, write, and execute permissions to a file, you can use the chmod command in Ubuntu. Here's an example of how to do it:
  ```
  chmod u+rwx /path/to/file
  ```
  In the above command:

  u refers to the user who owns the file.
  +rwx adds read, write, and execute permissions for the user.
  /path/to/file is the path to the file you want to modify.
  After running the command, the user will have read, write, and execute permissions on the specified file.

  You can also use numeric mode to set permissions. For example, if you want to give read, write, and execute permissions to the user, read-only permissions to the group, and no permissions to others, you can use the following command:
  
  ```
  chmod 750 /path/to/file
  ```
  
  In this case:
  7 corresponds to read, write, and execute permissions for the owner (user).
  5 corresponds to read and execute permissions for the group.
  0 corresponds to no permissions for others.
  Again, make sure to replace /path/to/file with the actual path to the file you want to modify.

<a id="understanding-user-and-groups"></a>
### Understanding Users and Groups
 - `less /etc/passwd`
 - `/etc/passwd` is the file that holds the information about users, and less outputs it nicely. Some time ago, passwd also stored user’s passwords, but not           anymore, for security reasons. Here is a sample output from a fresh install of Ubuntu Serve
 The format of the passwd file is the following:
     - username
     - password (replaced with x and stored in /etc/shadow)
     - UID (user id, a number)
     - GID (group id, also a number)
     - user’s full name
     - user’s home directory
     - user’s login shell (the program that runs when you log in. The nologin is a program that does nothing, used to prevent logging in as system users)
 - To modify a Linux user: use the usermod command like this: `usermod <username>`
 - To delete a Linux user: use the userdel command like this: `userdel <username>`
 
<a id="increase-decrease-swap-memory"></a>
## To increase the swap memory in Ubuntu, you can follow these steps:

1. Check the current swap usage and available space by running the **`free -h`** command. This will display the memory usage statistics, including swap.
2. Disable the existing swap space by executing the following command as root or with sudo privileges:
    
    ```
    sudo swapoff -a
    ```
    
3. Back up the existing swap configuration file:
    
    ```
    sudo cp /etc/fstab /etc/fstab.bak
    ```
    
4. Edit the **`/etc/fstab`** file using a text editor of your choice (e.g., nano or vim):
    
    ```
    sudo nano /etc/fstab
    ```
    
5. Look for the line that defines the swap partition or file. It may look similar to this:
    
    ```
    UUID=<swap_UUID> none swap sw 0 0
    
    ```
    
    Note: The actual line might differ based on your system configuration.
    
6. Comment out or remove the existing swap line by adding a **`#`** at the beginning of the line:
    
    ```
    # UUID=<swap_UUID> none swap sw 0 0
    ```
    
7. Add a new line at the end of the file to define the new swap space. If you have a separate swap partition, use the device path (e.g., **`/dev/sdb1`**). If you want to create a swap file, use the file path (e.g., **`/swapfile`**):
    
    For a separate swap partition:
    
    ```
    /dev/sdb1 none swap sw 0 0
    ```
    
    For a swap file:
    
    ```
    /swapfile none swap sw 0 0
    ```
    
8. Save the changes and exit the text editor.
9. If you created a new swap partition, you can enable it by running the following command:
    
    ```
    sudo swapon -a
    ```
    
    If you created a swap file, you need to create and enable it:
    
    ```
    sudo fallocate -l 4G /swapfile
    sudo chmod 600 /swapfile
    sudo mkswap /swapfile
    sudo swapon /swapfile
    ```
    
10. Verify the new swap space by running **`free -h`** command again. It should now show an increased swap size of 4GB.
  
 <a id="changing-ownership-of-a-file"></a>
 ## Changing ownership of a file
  
### There are several cases where you might need to change the ownership of a file or directory. Here are a few common scenarios:

 - User Account Changes: If a file was created or owned by a specific user account that no longer exists or has changed, you may need to update the ownership to reflect the new user account.
 - File Transfer: When transferring files between systems or users, the ownership may need to be changed to ensure that the new user has the appropriate permissions and control over the file. 
 - Collaborative Work: In a multi-user environment or when collaborating on a project, you may need to change the ownership of certain files or directories to allow different users or groups to access and modify them.
 - Administrative Tasks: System administrators often need to change ownership to manage system files, configuration files, or log files. This allows them to control access and perform necessary tasks.
 - Security Considerations: Changing ownership can be necessary for security purposes. For example, if a file has sensitive information, you may want to change the ownership to restrict access only to authorized users.
 - Restoration or Recovery: During data restoration or recovery from backups or snapshots, ownership may need to be adjusted to match the original configuration or to ensure proper access rights.
 - It's important to note that changing ownership should be done with caution, as incorrect ownership settings can lead to security vulnerabilities or unintended access restrictions.
 - Always ensure that the new ownership is appropriate for the file or directory and aligns with your intended use and security requirements.

 - To change the ownership of a file from root:root to vaheedshaik:vaheedshaik, you can use the chown command in Ubuntu. Here's an example of how to do it:

 ```
 sudo chown vaheedshaik:vaheedshaik /path/to/file
 ```
  





