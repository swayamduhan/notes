
terminal is a interface to do things on machine (CLI)

#### Basic Shit
- pwd - print working directory
-  cd _folder-name_ - change directory
- cd .. to go back
- ls - print files in folder
- mkdir _folder-name_ - make folder
- `mkdir -p file/furtherdir`  to recursively create directories
- touch _file-name_ - to create folder
- cat - print content of file
- `..` to hop back 1 folder, `../../` to hop back multiple directories
- `&&` to join 2 commands

#### viewing a file
`cat file` to view
`head file` for first 10 rows or `head -20` for first 20
`tail file` for last 10 rows and same as above
`wc file` to get lines, words and characters
#### Editing a file
to edit files
use `vi _fileName_` then press `i` to start editing
to close, `esc` to stop editing then `:q!` to exit without saving or `:wq!` to exit and save
we can also do `cat > filename` to edit
`cat >> file ` to append data to file

#### moving copying
- mv + _file_ + _directoryToMoveTo_  - move files
- `mv currentName.ext newName.ext` to rename
- to do both `mv current directory/newname`
- cp - to copy files (to copy folders instead of files, use -r just after cp)

#### node
- nvm - node version manages
- npm - node package manager

#### grep
`grep` is used to find any shit
eg : `grep "one" file.txt` 
`grep -c` for number of occurences
`grep -h` to see the occurences
`grep -hi` to ignore the case of word and find all cases eg : one, oNe, ONe
to search in a whole directory, use `-r`
`-n` for line number
`-w` to match whole word only
`-v` to get everything except this
`-A noOfLines`  to see lines before some shit
`-B` for after and `-C` for before and after

#### LS

- ls -l (L hai ye) - to print properties of the sub items
- ls -R = for details about sub directories and their properties
- ls -t = to put last modified item first in list
- ls -r = for opposite of above
- we can combine options easily eg: ls -tR
- ls -a = for hidden files
- ls -s = by size
- to find a specific file type use `grep` , eg : `ls -lR | grep .json`
- ls \*.js to get all js files in current directory
- eg : `ls wha*` will search for WhatsApp (`*` is wildcard)

#### pipe character ( | )
gives our output from 1st command to 2nd command
eg : `ls -lR | grep .json`
#### removing files
- `rm file` to delete `rm -r` to delete folder
#### changing permissions
`chmod` command
\+ to add perm and - to sub
u, g, o - user, group, others for whom to change perm
r, w, x - read write execute

usage - `chmod u+rw filename` add a `-R` in front if folder
you can also use numbers for ugo and rwx -
- 4 for r, 2 for w, 1 for x
- add these numbers up and write in respective order for u g and o
eg : `chmod 664 hello.txt`


#### ECHO command and more
- `echo 'Hello'` to display hello
- `echo $PATH` to display current path
### Making a script
bash is a programming language so we can make a whole script
`.sh` extension
specify interpreter in 1st line eg : `#!/bin/bash`
then simply write commands
`bash scriptDirectory` to run it

### Use `sed` for file manipulation (learn if necessary)
### Use `awk` for text processing (only if nec)(these both can replace grep)
