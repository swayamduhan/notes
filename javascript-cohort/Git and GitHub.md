## Overview
git install krliyo yaad se
Version Control System - keeps track of changes of files, easy to revert to a previous state, we can also see who made changes, compare changes

#### 2 types - Centralized and Distributed
Centralized needs to be up all the time so that people can collab with each other. but as soon as it goes down, you cant collab. good for smol teams, smol scale. eg : subversion, team foundation server
Distributed is very cool. everyone has their own copy of the code along with all history and logs. so even if server is down, you can still work locally in your own copy then push them online. moreover, other people also can pull your updated code. eg : Git


### GITHUB 
web based hosting services for git repositories. we can use git without github

LOCAL REPOSITORY - private copy of code
PUSH - send a change to another repo online (may require permission)
PULL - grab a change from repo

#### Basic workflow of Git
Working Directory -> `git add` -> Staging Area -> `git commit` -> repository
(modify file)                                                                            (changes permanently stored)

###### BLOB (Binary Large OBject)
each version of file is represented by blob. doesnt hold metadata only file content. binary file, named as SHA-1 hash of that file in git database
(in git, everything is content addressed, not by names)

###### Tree
an object that represents the directory. holds blob as well as other sub-directories. binary file.

### GIT COMMANDS

`clone` to bring locally
`add` to track your files n changes in git
`commit` to save files
`push` to upload commits on github
`pull` - download changes from online to local

### HOW TO?
`git init` to initialise an empty repo. a file with .git extension is created
`git status` to check the file git status
`git add .` to make all files ready for commit
`git rm --cached <file>` to remove certain files
`git commit -m <message> -m <moreMessage>` to commit files and -m to put message
`git remote -v` to check if any repo is configured
`git remote add origin <url.git>` to add a repo config
`git push origin master` to push code to master branch

also , `git commit -am <message>` to do both add and commit in same line

`git clone <url>` to make local workspace for repo

- to work in linux or MacOS we will need to generate SSH Key from our terminal and copy the ssh key code and paste it in github settings in ssh authentication typa shit. testauthkey.pub

## Git Branching
there is a master branch that contains the version of code that is running perfectly on the net and is being used by people.
if many people are working on that project, then a new branch is created for development and testing which is later pushed into main code. Feature Branch.
This branch is then 'MERGED' later
for fixing small bugs, we create a HOTFIX branch and then merge it later into main branch

`git branch` to know current branch
`git checkout -b <branchname>` to create new branch 
`git checkout <branch>` to switch branch
`git checkout` to undo changes done to a file
`git diff <branch>` to compare given branch to current branch and see differences
`git branch -d <name>` to delete a branch
`git push -u origin <branch>` to push to the branch
we then create a pull request (PR) to pave way for our changes to the main branch

## Merge Conflicts 
when many people are working on the master branch and you create a PR, git doesnt know which changes to keep and what to not keep
eg : if there was a file whose same part was changed both in master branch and feature branch, then it creates a conflict
git pauses the merging process
`git status` to check the unmerged files
you can either choose the main branch file or the new branch file or manage the contents manually 
HEAD is the content that is present in main
and the other one is present in our branch

`git log --merge` for list of commits causing conflict
`git reset --mixed`  undo changes to working dir n staging area
`git merge --abort` exit merge process and return back to state before merging 
`git reset` used at time of merge conflict to reset conflicted files to original state


## Issues in Github
to create potential additions or bug fixes or modifications
each issue has its own number
these issues can be fixed by making PRs. 
in your PR description you need to mention the issue and what to do with the issue

eg : closes #3
it will close the issue with number 3 when the PR is merged!
- more methods are given in the github docs, check them out
- eg : `close, closes, closed, fix, fixes, fixed, resolve, resolves, resolved`
- you can even fix issues in different repository or multiple issues