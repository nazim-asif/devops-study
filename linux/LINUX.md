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
