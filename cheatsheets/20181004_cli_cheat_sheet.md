*Journal*  
Rasmus Groth  
*20181004, Betahaus, Gracia, Barcelona, Spain*

# Command Line

[Github Gist](https://gist.github.com/bliiir/974a80f6f6635042fedf31ddbfbeb1f8)

## Commands

[Cheat Sheets](https://github.com/WebDevStudios/CLI-Cheat-Sheet)

| Command | meaning | example |
| :--- | :--- | :--- |
| `man <command>` | View the manual for given command| |
| `pwd` | Print work directory | |
| `ls` | list files in current directory | |
| `ls -a` | List all files, including hidden files | |
| `ls -l` | List files in current directory as a list | |
| `ls -la` | List all files in current directory as a list | |
| `cd /` | Change directory to root | |
| `cd ~` | Change directory to home | |
| `cp [origin] [destination]` | copy | cp text.txt . | |
| `mv [origin] [destination]` | move (and rename) | cp text.txt . | |
| `rm -rf folder_or_filename` | remove folder_filename forcefully recursively | |
| `echo "hello" > file.txt` | print "hello" to file.txt | |
| `say "hello"` | Use the voice module to read the string "hello"| |
| `cat filename` | print filename | |
| `head filename` | print first x lines of filename | |
| `tail filename` | print last x line of filename | |
| `history > file1.txt` | replace contents of file1.txt with history | |
| `history >> file1.txt` | append contents of file1.txt with history | |
| `history \ grep "git" > file1.txt` | Find the word "git" in my history and replace the content of file1.txt with the result| |
| `find . -name "file*"` | find files and folders with the characters "file" AS part of the name | |
| `cd -` | go back to the most recent dir you've been in | |
| `chmod 124 filename.ext` | change permissions  - owner, user, guest| |
| `which python3` | Shows you where the python command is located | |
| `history` | display past commands ||
| `touch scriptname.sh` | create shell script scriptname.sh | |
| `lsof -i tcp:8000` | List open files on tcp port 8000 | |
| `kill -9 pid` | kills the process with the pid | |
| `lsof -t -i tcp:8000 \| xargs kill -9` | kill all processes on port 8000|
| `echo $USER` | print the username to the console |
| `tail -f your.log` | Open a live version of the file your.log in the terminal |
| `whoami` | Shows your user |
| `sudo su` | Change to root user |


#### CLI options
| option | Effect     |
| :--- | :--- |
| `-r` | recursively |
| `-m` | message |

## Customization

Change `~/.bash_profile`, `.profile` or `~/.zscrc` to set custom command aliases

| alias | Resolves to | Description |
| :--- | :--- | :-- |
| `zshcf` | vim ~/.zshrc | Edit zsh profile settings|

#### Permissions

drwxr

rwx = Read Write Execute

| Directory | Owner | Group | User |
| :-- | :-- | :-- | :-- |
| - | - - - | - - - | - - - |
| d | rwx | rwx | rwx |
| 1 | 421 | 421 | 421 |

##### Examples
```
chmod 777 = read(4), write(2) and execute(1) right for owner(4), group(2) and user(1)
chmod 777  = give owner, group and user read, write and execute rights
chmod 444 = give owner, group and user read access
chmod 400 = give owner read access and all others no rights
```

### Shell Scripting
*Everything is a file!*
```
#!/bin/bash/
echo "starting script...
touch ~/Desktop/virus"
echo "creating virus"
echo "=============="
echo "adding to virus..."
find /Users/vkng/Dropbox/99_code/Python/CodingNomads -name "*week*" >> ~/Desktop/virus
open ~/Desktop/virus
```
```#!/bin/bash/``` is called the shbang
