*Permissions Cheatsheet*
*Rasmus Groth*
*Started: 20200331, Utterslev, Copenhagen, Denmark*
*Edited: 20200331, Utterslev, Copenhagen, Denmark*


### Permissions

```shell
$ ls -l
-rw-r--r-- 1 my_user my_group 100 Nov 28 15:29 filename.ext
```

| Part | Meaning |
| :-- | :-- | 
| `-rw-r--r--` | permissions| 
| `1` | number of links to this file
| `my_user` | owner | 
| `my_group` | group | 
| `100` | size in bytes |
| `Nov 28 15:29` | date |
| `filename.ext` | filename |

Use option `-R` to recursively modify subdirectories and files

---

#### `chown` - Change owner
Find out what user you are
```shell
whoami
```
Or who is logged in
```shell
who
```

```shell
chown <options> <owner> <file>
```

Examples
```shell
chown username filename.ext
```
Changes the owner of filename.ext to username

```shell
chown -R username directoryname
```
Changes the owner of directoryname and all it's subdirectories and files to username


---


#### `chgrp` - Change Group
Find out what groups you are in:
```shell
groups
```

```shell
chgrp <options> <group> <file>
```
Examples
```shell
chgrp groupname filename.ext
```
Changes the group of filename.ext to groupname

```shell
chown -R username directoryname
```
Changes the group of directoryname and all it's subdirectories and files to groupname


---


##### `chmod` - Change permissions/mode

```shell
chmod <options> <permissions> <file>
```

| Notation | Filetype | Owner | Group | User |
| :-- | :-- | :-- | :-- | :-- |
| | - | - - - | - - - | - - - |
| Symbolic | - | rwx | rwx | rwx |
| Octal | - | 421 | 421 | 421 |


| [Octal value][1] | [Symbolic value][2] | Description | 
| :--- | :--- | :--- |
| 777 | -rwxrwxrwx | read(4), write(2) and execute(1) permissions for owner(7), group(7) and user(7) |
| 444 | -r--r--r-- | read(4) permissions for owner(4), group(4) and user(4) |
| 400 | -r-------- | read(4) permissions for owner(4) |

Examples
```shell
chmod 777 filename.ext
```
Changes the permissions of filename.ext to 777 - ie `rwxrwxrwx`

```shell
chmod -R 575 directoryname/
```
Changes the permissions of directoryname and all it's subdirectories and files to 575 - ie `r-xrwxr-x`

---

[1]: http://www.filepermissions.com/articles/understanding-octal-file-permissions#Break-Down-of-Octal-Notation
[2]: http://www.filepermissions.com/articles/what-are-file-permissions-in-linux-and-mac#Breakdown-of-Symbolic-Notation
