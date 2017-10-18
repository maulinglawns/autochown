# autochown
### A `setuid` workaround for directories
___

### Purpose:
This small script aims to solve the problem of automatically changing owner to `<username>` upon creating - or moving - new files to `<directory>`.
Similar to the `setgid` bit, except this works on users.

### Usage:
```
autochown [-h] -d <directory> -u <user> 
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

### Example:
```
# whoami 
root
# touch /sftp/file_before_autochown
# ls -l /sftp/
total 0
-rw-r--r--. 1 root root 0 18 okt 20.27 file_before_autochown
# ./autochown -d /sftp/ -u sftpuser &
[1] 3822
# touch /sftp/file_after_autochown
# ls -l /sftp/
total 0
-rw-r--r--. 1 sftpuser root 0 18 okt 20.27 file_after_autochown
-rw-r--r--. 1 root     root 0 18 okt 20.27 file_before_autochown

```
