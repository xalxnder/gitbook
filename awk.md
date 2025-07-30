# Awk

| Comand                                       | Explanation                                              |
| -------------------------------------------- | -------------------------------------------------------- |
| `awk '{ print $1 }' list`                    | Print the first line of a file called list.              |
| `awk -F: ' {print $1}' /etc/passwd`          | Print the first field in /etc/passwd                     |
| `awk -F : '/user/ { print $4 }' /etc/passwd` | Search /etc/password for the term user in the 4th filed. |
