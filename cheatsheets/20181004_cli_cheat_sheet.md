*Cheatsheet*
*Rasmus Groth*
*Started: 20181004, Betahaus, Gracia, Barcelona, Spain*
*Edited: 20190821, Utterslev, Copenhagen, Denmark*

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
| `tail -f your.log` | Open a live version of the file your.log in the terminal |
| `history > file1.txt` | replace contents of file1.txt with history | |
| `history >> file1.txt` | append contents of file1.txt with history | |
| `history \ grep "git" > file1.txt` | Find the word "git" in my history and replace the content of file1.txt with the result| |
| `find . -name "file*"` | find files and folders with the characters "file" AS part of the name | |
| `find / -name "postgresql.conf"` | find the file 'postgresql.conf' recursively from the root folder |
| `cd -` | go back to the most recent dir you've been in | |
| `chmod 124 filename.ext` | change permissions  - owner, user, guest| |
| `which python3` | Shows you where the python command is located | |
| `history` | display past commands ||
| `touch scriptname.sh` | create shell script scriptname.sh | |
| `lsof -i tcp:8000` | List open files on tcp port 8000 | |
| `kill -9 pid` | kills the process with the pid | |
| `lsof -t -i tcp:8000 \| xargs kill -9` | kill all processes on port 8000|
| `echo $USER` | print the username to the console |
| `whoami` | Shows your user |
| `sudo su` | Change to root user |
| `ps aux` | report a snapshot of the current processes. a = show processes for all users, u = display the process's user/owner, x = also show processes not attached to a terminal |
| `top` | Show all the running processes within your Linux environment |
| `man <command>` | Shows a manual for `<command>` |
| `defaults write com.apple.finder AppleShowAllFiles TRUE` | Shows hidden files in Finder |
| `killall Finder` | Restarts the Mac Finder program |
| `reboot` | Reboot computer |


### Background tasks
|Commmand|Description|
|:--|:--|
| `python3 script.py &` | Run python script in the background |
| `nohup python3 script.py &`| Run python script in the background and detach from session |


### Postgres
|Commmand|Description|
|:--|:--|
| `sudo service postgresql stop` | Stop postgres database |
| `sudo service postgresql start` | Star postgres database |



### Networking
| Command | Description |
| :--- | :--- |
| `curl ifconfig.me` | Get own ip number |
| `curl https://freegeoip.app/xml/143.204.247.98` | Get the geolocation of an ip number using the [freegeoip](https://freegeoip.app/) service |
| `curl https://freegeoip.app/xml/bitmex.com` | Get the geolocation of an ip number |
| `dig 143.204.247.98` | DNS lookup utility |
| `dig bitmex.com` | DNS lookup utility |
| `traceroute 143.204.247.98` | print the route packets take to network host |
| `traceroute bitmex.com` | print the route packets take to network host |


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
