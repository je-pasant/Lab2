# Lab2

```
## 1. List the user commands and redirect the output to /tmp/commands.list
```sh
compgen -c > /tmp/commands.list
```

## 2. Count the number of user commands
```sh
wc -l < /tmp/commands.list
```

## 3. Get all the usernames whose first character in their login is ‘g’.
```sh
awk -F: '$1 ~ /^g/ {print $1}' /etc/passwd
```

## 4. Get the login names and full names (comments) of logins starting with “g”.
```sh
awk -F: '$1 ~ /^g/ {print $1, "-", $5}' /etc/passwd
```

## 5. Save the output of the last command sorted by their full names in a file.
```sh
awk -F: '$1 ~ /^g/ {print $1, "-", $5}' /etc/passwd | sort > /tmp/g_users_sorted.txt
```

## 6. Write two commands: first: to search for all files on the system that named `.bash_profile`. Second: sorts the output of `ls` command on `/` recursively, saving their output and error in two different files and sending them to the background.
```sh
find / -type f -name "bash_profile"
ls -R / > /tmp/ls_output.txt 2> /tmp/ls_errors.txt &
```

## 7. Display the number of users currently logged into the system.
```sh
who | wc -l
```

## 8. Display lines 7 to 10 of /etc/passwd file.
```sh
head /etc/passwd | tail -4
```
Or
```sh
sed -n '7,10p' /etc/passwd
```

## 9. What happens if you execute:
- `cat filename1 | cat filename2`
   - It should output the contents of `filename1` followed by `filename2`. But it will output `filename2` only, because `filename1` will output in buffer, but `filename2` will read from `cat filename2` not from buffer.

- `ls | rm`
   - This attempts to remove all files listed by `ls`, which is dangerous and not recommended.

- `ls /etc/passwd | wc –l`
   - This counts the number of lines outputted by `ls /etc/passwd`, which is 1.

## 10. Issue the command sleep 100.
```sh
sleep 100
```

## 11. Stop the last command.
```sh
kill –STOP %1
```
Or  
```sh
Ctrl + Z
```

## 12. Resume the last command in the background.
```sh
bg
```
Or  
```sh
kill –CONT %1
```

## 13. Issue the jobs command and see its output.
```sh
jobs
```

## 14. Send the sleep command to the foreground and send it again to the background.
```sh
fg %1    
bg %1
```

## 15. Kill the sleep command.
```sh
kill %1
```

## 16. Display your processes only.
```sh
ps -u basant
```

## 17. Display all processes except yours.
```sh
ps aux | grep -v basant
```

## 18. Use the pgrep command to list your processes only.
```sh
pgrep -u basant
```

## 19. Kill your processes only.
```sh
pkill -u basant
```

## 20. Compress a file by compress, gzip, zip commands and decompress it again. State the differences between compress and gzip commands.
To Compress a file “myfile”:
```sh
compress myfile      # Creates myfile.Z  
gzip myfile          # Creates myfile.gz  
zip archive.zip myfile  # Compresses and archives
```

To Decompress:
```sh
uncompress myfile.Z
gunzip myfile.gz
unzip archive.zip
```

Differences:
- **Compression Level**: gzip typically achieves better compression than compress.
- **File Extension**: gzip uses .gz extension, while compress uses .Z.
- **Command Options**: gzip has more options and flexibility than compress.

## 22. What is the command used to view the content of a compressed file?
```sh
zcat
```

## 23. Backup /etc directory using tar utility.
```sh
tar -cvf /backup/etc_backup.tar.gz /etc
```

## 24. Starting from your home directory, find all files that were modified in the last two days.
```sh
find ~ -type f -mtime -2
```

## 25. Starting from /etc, find files owned by root user.
```sh
find /etc -user root
```

## 26. Find all directories in your home directory.
```sh
find ~ -type d
```

## 27. Write a command to search for all files on the system that are named “.profile”.
```sh
find / -name .profile
```

## 28. Identify the file types of the following:
- `/etc/passwd`
- `/dev/pts/0`
- `/etc`
- `/dev/sda`

```sh
file /etc/passwd
file /dev/pts/0
file /etc
file /dev/sda
```

## 29. List the inode numbers of `/`, `/etc`, `/etc/hosts`.
```sh
ls -i /
ls -i /etc
ls -i /etc/hosts
```

## 30. Copy `/etc/passwd` to your home directory, use the commands diff and cmp, edit the copied file, and then use these commands again.
```sh
cp /etc/passwd ~/copied_passwd
diff /etc/passwd ~/copied_passwd
cmp /etc/passwd ~/copied_passwd
vi ~/copied_passwd    # Edit the copied file
diff /etc/passwd ~/copied_passwd
cmp /etc/passwd ~/copied_passwd
```

## 31. Create a symbolic link of /etc/passwd in /boot.
```sh
ln -s /etc/passwd /boot/soft_link
```

## 32. Create a hard link of /etc/passwd in /boot. Could you? Why?
```sh
ln /etc/passwd /boot/hard_link
```
No, I couldn’t.
Because creating a hard link in `/boot` would require root permissions because `/boot` is usually owned by root and may be mounted with special permissions
