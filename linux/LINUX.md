# linux Concepts and commands

### Soft Link
A soft link, also known as a symbolic link or symlink, is a type of file in Unix-like operating systems, including Linux. A symbolic link is a special type of file that contains a reference to the target file or directory's pathname.

Command for same host

    `ln -s /home/user/documents/original_file.txt link_to_original.txt`


If we delete original file then linked file is not working.

### Hard Link

In Linux, a hard link is a mechanism that allows multiple filenames (links) to refer to the same inode (data structure representing a file) on a filesystem. Unlike symbolic links (soft links), which point to filenames, hard links directly point to the underlying data blocks of a file.

Command: ` touch original_file `

         ln original_file hard_link    


### System information

command ` uname -a `

### OS information

command ` cat /etc/os-release `

### Environment variable

1. local environment variable. it is available only for same terminal.
    command 
``` 
    export MYNAME=asif
    echo MYNAME
```
2. Global environment variable. Need to set variable in bashrc. It is available for all.


### User Management

. **User List**: To see user List. Command ` cat /etc/passwd `

. **useradd**: Create new user in linux. Command: ` sudo useradd test ` 

. **User add with Group**: Command: ` sudo useradd test -g 1002 `

. **User details**: `  test:x:1002:1002::/home/test:/bin/sh` . First portion is username. Second one is password here is empty. 3rd is user's unique identifier. 4th is group id. 5th is some information regarding user. 6th is Directory where user first land after log in. 7th is default terminal.

. **Delete user**: command: ` sudo userdel test `

. **adduser**: For creating user in most descriptive way, use adduser command. ` sudo adduser test `

. **usermod**: Usermod use for update information after creating it.

. **Change password**: Change password after creating user. Command: ` sudo passwd test `

### Groups in Linux

. To add a group in Linux, use the groupadd command: ` sudo groupadd demo `

. If you want to create a group with a specific group ID (GID), use the --gid or -g option. Command: ` sudo groupadd -g 1009 demo1 `

. You can change the group ID of any group with the groupmod command and the --gid or -g option: Command: ` sudo groupmod -g 1011 demo1 `

. You can rename a group using groupmod with the --new-name or -n option. Command: ` sudo groupmod -n test demo1 `

. Suppose you have existing users named user1 and user2, and you want to add them to the demo group. Use the usermod command with the --append --groups options (-a and -G for short). Command
```
    
    sudo usermod --append --groups demo user1

    sudo usermod -aG demo user2
    
    
```

. To remove a specific user from a group, you can use the gpasswd command to modify group information. Command: ` sudo gpasswd --delete user1 demo  `

### ACL (Access Control List)

List of commands for setting up ACL :

1) To add permission for user

   ``` setfacl -m "u:user1:rwx" /path/to/file ```

2) To add permissions for a group

   ``` setfacl -m "g:group1:rw" /path/to/file ```

3) To allow all files or directories to inherit ACL entries from the directory it is within

   ``` setfacl -dm "entry" /path/to/dir  ```

Example: 
    ``` setfacl -dm u:user1:rw /data/projects ```

4) To remove a specific entry

   ``` setfacl -x "entry" /path/to/file ```

Example:

``` setfacl -x u:user1 /data/projects/example.txt ```

5) To remove all entries

   ``` setfacl -b path/to/file```

6) To show the status 

``` getfacl /data/projects/example.txt  ```

There has another option to give permission which is **chmod** but problem is Limited to basic owner, group, others model where setfacl is Provides detailed and granular control over permissions for multiple users and groups.

### Help command in linux

There are three help command in linux

1. man (Manual Pages): The man command provides a comprehensive set of manual pages for most commands and applications. 

```man <command> ```

Example: ``` man ls ```

2. --help Option: Most command-line utilities provide a --help or -h option that displays a summary of the command's usage and available options. Usage:
``` <command> --help ```
Example: ``` ls --help ```

3. whatis Command: The whatis command provides a brief description of a command. Usage:

```whatis <command>```
Example: ```whatis ls ```
