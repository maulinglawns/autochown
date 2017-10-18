# autochown
### A `setuid` workaround for directories
___

### Purpose:
We cannot (and for good reasons) use `setuid` the same way we can use `setgid` on directories in GNU/Linux.
This small script aims to solve the problem of automatically changing owner to <username> upon creating - or moving - new files to <directory>

### Usage:
```
Mandatory switches and arguments:
-d <directory> = Directory to watch
-u <user> = Change owner to this user
Optional:
-h = Show help and exit
```

### Exit codes:
```
Exit codes:
0: Success.
1: Error. Unknown switch.
2: Error. Directory or username not specified.
3: Error. The directory specified is not a directory.
4: Error. The specified user does not exist.
5: Error. You are not root.
```

### Examples:
Success:
```
[root@localhost ~]# ./autochown.sh -d /sftphome/ -u sftpuser &
[1] 2588
[root@localhost ~]# Setting up watches.
Watches established.

[root@localhost ~]# ls -l /sftphome/
totalt 0
[root@localhost ~]# touch /sftphome/foobar
[root@localhost ~]# ls -l /sftphome/
totalt 0
-rw-r--r--. 1 sftpuser root 0 18 okt 12.21 foobar
```
Various errors:
```
[root@localhost ~]# ./autochown.sh -d /sftphome/ -u sleezeball
No user sleezeball found on this system. Exiting.
[root@localhost ~]# ./autochown.sh -d /ftphome/ -u sftpuser
/ftphome/ is not a directory. Exiting
[root@localhost ~]# ./autochown.sh -d /ftphome/ -z sftpuser
Unknown option. '-d' '-u' and '-h' allowed. Usage:
./autochown.sh -d <directory> -u <username> [-h]
```
