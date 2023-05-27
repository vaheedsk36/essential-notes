# linux-essentials
This repo covers all essential commands, which will be handy if you are using a personal virtual linux machine or a linux pc

## Topics Covered
- Understanding permissions in linux
- Changing file permissions
- Understanding Users and Groups

## Understanding permissions in linux
  In Linux, file permissions are a way to control access to files and directories. They determine who can read, write, and execute a file or directory. Understanding permissions is crucial for managing security and controlling access to sensitive data.

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

### Changing file permissions



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
 - 
