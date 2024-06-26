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


### PIPE (|)

A pipe is used by the shell to connect the output of one command directly to the input of another command

the symbol is ` Command1 | command 2 `

Example: ` ls -l | tail -1 `

### Some important commands.

1. **cp** for copy. Example: ` cp file.txt /backup `.
2. **rm** for remove. Example: `rm myfile1 `.
3. **mv** for move. Example: `mv oldname.txt newname.txt `.
4. **mkdir** for creating directory. Example: ` mkdir newdirectory `. Create nested directories (including parents if they don't exist): Example: ` mkdir -p parentdir/childdir/grandchilddir `.
5. **rmdir** remove and empty directory. Example: ` rmdir emptydirectory `.
6. **rm -r** remove files and directories recursively. Example:  ` rm -r directoryname `
7. **cat** (concatenate and display file content)

    - Display the contents of a file: `cat filename.txt`

    - Concatenate and display multiple files: `cat file1.txt file2.txt`

    - Redirect the content of a file to another file: `cat file1.txt > file2.txt`

    - Append the content of a file to another file: `cat file1.txt >> file2.txt`

8. **more** (view file content page by page)
   
   - Display the contents of a file one screen at a time: `more filename.txt`

   - Navigate using more:

      - Press **Space** to go to the next page.
      - Press **Enter** to go to the next line.
      - Press **q** to quit. 

9. **less** (view file content with backward and forward navigation)
   - Display the contents of a file with more navigation options: ` less filename.txt `
   - Navigate using less:
     - Use Page Up and Page Down to navigate.
     - Use the arrow keys to move line by line.
     - Press q to quit.
     
10. **head** (output the first part of files)
     - Display the first 10 lines of a file: ` head filename.txt `
     - Display the first N lines of a file (e.g., 20 lines): ` head -n 20 filename.txt `
    
11. **tail** (output the last part of files)
     - Display the last 10 lines of a file: ` tail filename.txt `
     - Display the last N lines of a file (e.g., 20 lines): ` tail -n 20 filename.txt `
     - Display the last lines of a file and keep updating (useful for log files): ` tail -f filename.txt `

12. **cut** (remove sections from each line of files)
     - Cut the first 10 characters of each line: ` cut -c 1-10 filename.txt `
     - Cut the 2nd and 4th fields of each line (fields are separated by a delimiter, e.g., a comma): ` cut -d ',' -f 2,4 filename.csv `
    
13. **awk** (pattern scanning and processing language)
     - Print the 1st and 3rd fields of each line (fields are separated by a space by default): ` awk '{print $1, $3}' filename.txt `
     - Sum the values in the second column: ` awk '{sum += $2} END {print sum}' filename.txt `
     - Print lines where the second column is greater than 100: ` awk '$2 > 100' filename.txt `
    
14. **grep** (print lines that match patterns)
     - Search for lines containing the word "pattern": ` grep 'apple' example.txt `
     - Search for lines containing the word "pattern" (case-insensitive): ` grep -i 'pattern' filename.txt `
     - Search for lines that do not contain the word "pattern": ` grep -v 'pattern' filename.txt `
    
15. egrep (extended grep, supports extended regular expressions)
     - Search for lines containing "pattern1" or "pattern2": ` egrep 'pattern1|pattern2' filename.txt `
     - Search for lines starting with "pattern": ` egrep '^pattern' filename.txt `
     - Search for lines ending with "pattern": ` egrep 'pattern$' filename.txt `
    
16. sort (sort lines of text files)
     - Sort lines alphabetically: ` sort filename.txt `
     - Sort lines in reverse order: ` sort -r filename.txt `
     - Sort lines numerically: ` sort -n filename.txt `
    
17. uniq (report or omit repeated lines)
     - Remove duplicate lines (file should be sorted first): ` sort filename.txt | uniq `
     - Count the number of occurrences of each line: ` sort filename.txt | uniq -c `
     - Only print duplicate lines: ` sort filename.txt | uniq -d `

18. The **wc** (word count) command in Unix/Linux is used to display the number of lines, words, and bytes in a file or the standard input. It can also be used to count the characters and the maximum line length.

    - Count the number of lines, words, and bytes in a file: ` wc filename.txt `
    - Count the number of lines: ` wc -l filename.txt `
    - Count the number of words: ` wc -w filename.txt `
    - Count the number of characters: ` wc -m filename.txt `
    - Count the number of bytes: ` wc -c filename.txt `
    - Find the length of the longest line: ` wc -L filename.txt `
    - Count lines and words: ` wc -lw filename.txt `
    - Count the number of lines in the output of a command: ` ls | wc -l `
19. **diff** Command
    - The diff command compares two files line by line and outputs the differences between them. It is typically used to show changes between two versions of a file. ` diff file1.txt file2.txt `
    
20. **cmp** Command
    - The cmp command compares two files byte by byte and is useful for binary files. It provides a more detailed comparison than diff. ` cmp file1.bin file2.bin `.
    
21. **tar** Command
    - The tar (tape archive) command is used to create, maintain, modify, and extract files from an archive file. ` tar -cvf archive.tar file1.txt file2.txt directory/ `
    - Extract a tar archive. ` tar -xvf archive.tar `.

22. **gzip** Command

    - Compress a file: ` gzip file.txt `.
    - Decompressing a File. ` gzip -d file.txt.gz `

23. The **truncate** command in Unix/Linux is used to shrink or extend the size of a file to a specified size. If the file is larger than the specified size, it will be reduced in size. If the file is smaller, it will be extended, and the extended part will be filled with null bytes.

    - Set the size of a file to a specific value. ` truncate -s 100 filename.txt `.
    - Increase the size of a file by a specific amount. ` truncate -s +50 filename.txt `.

### Combining and Splitting file

1. **Combining file**: 
    - Combine multiple text files into one: ` cat file1.txt file2.txt > combined.txt `.
    - Combine multiple files line by line: ` paste file1.txt file2.txt > combined.txt `.
    - Split a file based on context: ` csplit largefile.txt '/pattern/' '{*}' `.
2. **Splitting file**:
    - Split a file into smaller parts: ` split -b 1M largefile.bin smallfile_ `.
    - Split a file into smaller parts based on lines: ` split -l 1000 largefile.txt smallfile_ `.


### Monitor Users

1. **who** Command: The who command shows who is currently logged into the system. ` who `.
2. **last** Command: The last command shows a list of the most recent logins on the system. ` last `.
3. **w** Command: The w command shows who is logged on and what they are doing. ` w `.
4. **id** Command: The id command shows user and group information for a specified user or the current user.
    - Show the current user’s ID and groups: ` id `.
    - Show the ID and groups for a specific user: ` id username `.


### Communicating with users

1. **users** Command: The users command shows a quick list of users currently logged into the system. ` users `.
2. **wall** Command: The wall (write all) command is used to send a message to all users currently logged into the system. ` wall "System maintenance will begin in 10 minutes." `
3. **write** Command:
    - Send a message to a specific user:
      - Start writing a message: ` write user2 `.
      - Type the message: ` Hello, can you check the server logs? `.
      - End the message with Ctrl+D.

### system utility command

1. **date** Command: 
    - Display the current date and time: ` date `.
    - Custom format (e.g., Year-Month-Day Hour:Minute ): ` date +"%Y-%m-%d %H:%M:%S" `.
2. **uptime** Command: The uptime command shows how long the system has been running, along with the number of users and the system load averages. ` uptime `.
3. **cal** Command: ` cal `.
4. **bc** Command: ` bc `.
5. **hostname** Command: 
    - Display the current hostname: ` hostname `.
    - Set the hostname (requires superuser privileges): ` sudo hostname newhostname `.
6. **uname** Command:
    - Display basic system information: ` uname `.
    - Display all system information: ` uname -a `.
   
   Example: ` Linux myhostname 5.4.0-74-generic #83-Ubuntu SMP Fri May 14 19:00:11 UTC 2023 x86_64 x86_64 x86_64 GNU/Linux `
      
     This output shows:

      - Kernel name (Linux)
      - Hostname (myhostname)
      - Kernel release (5.4.0-74-generic)
      - Kernel version (#83-Ubuntu SMP Fri May 14 19:00:11 UTC 2023)
      - Machine (x86_64)
      - Processor (x86_64)
      - Hardware platform (x86_64)
      - Operating system (GNU/Linux)
7. **which** : it gives directory path of where the command exists. ` which ls `. 

### systemctl command

1. Start a service: ` systemctl start service_name `.
2. Stop a service: ` systemctl stop service_name `.
3. Restart a service: ` systemctl restart service_name `.
4. Reload the configuration of a service without interrupting its operation: ` systemctl reload service_name `.
5. List all active services: ` systemctl list-units --type=service `.

### **ps** command

1. Basic process listing: ` ps `.
2. Detailed process listing (user-oriented): ` ps aux `.
3. Detailed process listing (full format): `  ps -ef `.
4. Find specific processes by name: ` ps aux | grep process_name
   ps -ef | grep process_name `.
5. List processes for a specific user: `  ps -u username `.

### **top** command

1. Basic Usage: ` top `.
2. Common Interactive Commands:

    - q: Quit
    - h: Help
    - k: Kill process
    - r: Renice process
    - P: Sort by CPU usage
    - M: Sort by memory usage
    - N: Sort by PID
    - T: Sort by time

3. Filtering by User: ` top -u username `.
4. Batch Mode: ` top -b -n 1 > top_output.txt `.


### **crontab** command:

1. Basic Usage: ` crontab [options] `

   Common Options
   - `crontab -e`: Edit the current user's crontab file.
   - `crontab -l`: List the current user's crontab entries.
   - `crontab -r`: Remove the current user's crontab file.
   - `crontab -u user`: Specify a different user (requires superuser privileges).

2. Crontab File Format: See internet for format.
3. Example: Automating a Backup Script
    - Open the crontab editor: ` crontab -e `.
    - Add the following line to the crontab file: ` 0 3 * * * /home/user/scripts/backup.sh `.
    - Save and exit the editor.

### **at** command:

The at command in Unix/Linux is used to schedule commands to be executed at a specific time in the future. Unlike cron, which is used for recurring tasks, at is designed for one-time tasks.

1. Basic Usage: ` at [OPTION] TIME `.

   Common Options:
    - l or atq: List pending jobs for the current user.
    - d or atrm JOB_ID: Remove a scheduled job.
    - f FILE: Read the job to be scheduled from a file.

### process management commands

for process management we can use **bg** for background. for **fg** for retruning back from background to forground. Use **nohup** for running process as background and **nice** command for prioritise running the process.

### system monitoring command

1. **top**
2. **vmstat** command: ` vmstat [options] [delay [count]] `
    - delay: The time interval (in seconds) between each report.
    - count: The number of reports to generate.
    - Common Options:
      - a: Display active and inactive memory.
      - d: Report disk statistics.
      - p <partition>: Report statistics for a specific partition.
      - s: Display a table of various event counters and memory statistics.
      - t: Add a timestamp to each line of output.
      - w: Wide output mode (for systems with many CPUs).
    - Output Columns: When you run vmstat, it provides a tabular output with multiple columns, each representing different metrics. Here’s a breakdown of the key columns:

      - Process
        - r: The number of runnable processes (running or waiting for CPU).
        - b: The number of processes in uninterruptible sleep (usually IO).
      - Memory
        - swpd: The amount of virtual memory used (swap space) in kilobytes.
        - free: The amount of idle memory in kilobytes.
        - buff: The amount of memory used as buffers in kilobytes.
        - cache: The amount of memory used as cache in kilobytes.
      - Swap
        - si: The amount of memory swapped in from disk (per second).
        - so: The amount of memory swapped out to disk (per second).
      - IO
        - bi: Blocks received from a block device (per second).
        - bo: Blocks sent to a block device (per second).
      - System
        - in: The number of interrupts per second, including the clock.
        - cs: The number of context switches per second.
      - CPU
        - us: Time spent running non-kernel code (user time, including nice time).
        - sy: Time spent running kernel code (system time).
        - id: Time spent idle.
        - wa: Time spent waiting for IO.
        - st: Time stolen from a virtual machine (hypervisor).
        
3. **iostat** command: The iostat command provides statistics on CPU and input/output (I/O) device utilization.
    - Basic usage: ` iostat `.
    - Detailed output with device statistics: ` iostat -xd `.

4. **free** command: The free command displays the amount of free and used memory in the system.
    - Basic usage: ` free `.
    - Human-readable format: ` free -h `.

5. **df** , **du**, **mpstat**, **netstat**, **ss**, **sar**, **uptime**, **dstat**, **lsof**
    




