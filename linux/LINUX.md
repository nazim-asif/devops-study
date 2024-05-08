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


