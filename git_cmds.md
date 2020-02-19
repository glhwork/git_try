<!-- Cheat sheet of git commands in terminal -->
# Cheat sheet of git commands in terminal

## **Set Configurations**
### 1 Show configurations 
Show the global/local configurations as a list
```terminal
$ git config --global --list
$ git config --local --list
```
### 2 Set developer configurations
"core.editor" tag is used to set default editor for git files(commit, etc.)
```terminal
$ git config --global user.name "your name"
$ git config --global user.email "email address"
$ git config --global core.editor default-editor
```
### 3 Git alias
To make git simpler

Remember, do not write alia-name beginning with 'git ...'
```terminal
$ git config --global alias.<custom-name> alia-name
$ git config --global alias.<custom-name> 'alia-name(long command)'
```
If the command is external rather than a Git sub-command
```terminal
$ git config --global alias.<custom-name> '!<comannd-name>'
```
Example
```terminal
$ git config --global alias.list '!ls'
```
Then "git list" takes the same effect as "ls" in terminal

## **Undo Things**
### 1 Modify last commit
If we forget something to be added to last commit or if we just want to modify the latest commit message, use this command 
```terminal
$ git commit --amend 
$ git commit --amend <file-name>
```
Examples:
```terminal
$ git commit -m "commit message"
$ vim <file-name>
$ git add <file-name>
$ git commit --amend
```
or
```terminal
$ git commit -m "commit message"
$ vim <file-name>
$ git commit --amend <file-name>
```
### 2 Unstage files
If we mistakenly add some files to stage, use this command
```terminal
$ git reset HEAD <file-name>
```
### 3 Unmodify files
If we want to discard the latest modification, use this command

**But attention! This command is dangerous, unless we are very clear about what content we are going to remove**
```terminal
$ git checkout -- <file-name>
```

## **Add Tags**
List all the existing tags
```terminal
$ git tag
```
Search for certain tags
```terminal
$ git tag -l "<tag-name>"
$ git tag --list "<tag-name>"
```
Add annotated tags (recommended) and show the information of this tag

"-a" options refers to "annotated"
```terminal
$ git tag -a <tag-name> -m "tag message"
$ git show <tag-name>
```
Add lightweight tag and show the information of this tag
```terminal
$ git tag <tag-name>
$ git show <tag-name>
```
Add tag with a certain commit message
```terminal
$ git tag -a <tag-name> <part-of-commit-checksum>
```
If we want to add this tag to remote server, use this command
```terminal
$ git push origin <tag-name>
$ git push origin --tags
```
Delete tags locally
```terminal
$ git tag -d <tag-name>
```
Delete tags from a remote server
```terminal
$ git push origin :refs/tags/<tag-name>
```
or
```terminal
$ git push origin --delete <tag-name>
```

## **Search History**
<!-- git log -->

## **Branching**
### 1 Create branch
In order 

    A. create a new branch 
    B. switch to new branch 
    C. create a new branch and switch to it at once
    D. view which branch is currently on
    E. delete branch
    F. force to delete branch

```terminal
$ git branch <branch-name>
$ git checkout <branch-name>
$ git checkout -b <branch-name>
$ git log --decorate
$ git branch -d <branch-name>
$ git branch -D <branch-name>
```
The new branch will start at where the current branch we are on

### 2 Merge
Merge the \<branch-name\> with the current branch the HEAD is on
```terminal
$ git merge <branch-name>
```
Another way to merge branchs is rebasing
```terminal
$ git rebase <branch-name>
```
Rebase patches which start where branch-b diverges from branch-a to \<branch-master\>
```terminal
$ git rebase --onto <branch-master> <branch-name-a> <branch-name-b>
```
If the "rebase" of another developer makes us mess up our own development, this helps us out
```terminal
$ git rebase <remote-name>/<branch-name>
```


### 3 Branch management
If we want to show the lastest commit of each branch, use this command
```terminal
$ git branch -v
```
Show whether each branch is merged into the current branch we are on
```terminal
$ git branch --merged
$ git branch --no-merged
```
Show whether each branch is merged into the \<branch-name\> 
```terminal
$ git branch --merged <branch-name>
$ git branch --no-merged <branch-name>
```

## Git On Server
### 1 Protocols
#### 1.1 Local protocol
Clone from local filesystem
```terminal
$ git clone <local-git-repo-address>
$ git clone file:://<local-git-repo-address>
```
Example
```terminal
$ git clone file::///srv/git/project.git
```
Add a local repository to a git project
```terminal
$ git remote add <local-project-name> <local-git-repo-address>
```
#### 1.2 HTTP protocol
<!-- To be edited -->

#### 1.3 SSH protocol
Pay attention to when to use / or :
```terminal
$ git clone ssh://[user@]<server-address>/<project-name>.git
$ git clone [user@]<server-address>:<project-name>
```