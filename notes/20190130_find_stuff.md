# Find stuff

Find all files by the name {name of file}
```
find {path} -iname {name of file}
```

Find all files with the text to find in the current directory
```
grep -l  [text to find] [files to look in]
```

Example:

```
grep -l hello *.txt
```
Finds all txt files with the word "hello" inside



Show hidden files in finder

    defaults write com.apple.finder AppleShowAllFiles TRUE
    killall Finder
