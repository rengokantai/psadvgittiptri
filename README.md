#### psadvgittiptri
#####Introduction
######The Tools
```
git rebase --onto HEAD~2(new base commit) HEAD~1(old base commit)
```
######3
Three concepts:  
Commits, snapshots, references

#####The Command Line
######Command Line Utilities
install git on windows using powershell: posh-git
```
Install-Module posh-git
```
mac: git-completion.bash  

######aliases
```
git config --global alias.st "status --short --branch"
```
quick merge
```
git config --global alias.qm "!git checkout $1;git merge @{-1}'
```
######Pretty History
```
git log --pretty='%h | %d %s (%cr) [%an]'
```
more complicated: note reset color
```
git log --pretty='%Cred%h%Creset | %C(yellow)%d%Creset %s %Cgreen(%cr)%Creset %C(cyan)[%an]%Creset
```
######Diffs
```
git config --global core.pager 'less -RFX'
```
```
git diff --word-diff --unified=10
```

other pattern
```
git diff --patience
```
```
git config --global diff.algorithm histogram
```
######Show Commits
```
git cat-file -p head
```
both are ok.
```
git diff head~2..head --stat
git diff head..head~2 --stat
```
#####Crafting Commits
######Verifying Commits
```
git stash save --keep-index --include-untracked "message" //only stage working dict, not index
```
```
git stash list
git stash pop(remove stash from list)/apply(not remove)
```
#####Searching History
######Reachability
```
git log a..b     //commit can reach by B but not A
git log a...b     //commit can reach by B or A ,but not both
```
```
git log --ancestry-path a..b  //show all commit not only ancestor of b, but descendent of a (for example,merge commit)
```
```
git show-branch a b c
```
######Tracking Commits
show merged branch
```
git branch --merged (name)
```
not merged branch
```
git branch --no-merged (name)
```

show topic
```
git show-branch --topic master a b   //show all commits in branch a and b but not in master
```
######
search which commit contains specific string change(only c and c++)
```
git log -L:funcname:filename
```
set .gitattributes
```
*.java diff=java
```
######Tracking Authors
```
git blame filename
git blame filename -L14:16
git-shortlog -s -n |head -10
```
#####Branching and Merging
show all branch's head
```
git show-ref --heads
```
when delete a branch, we just delete the ref, make the commits dangling.
```
git branch -D b
```
check all dangling commits
```
git fsck --dangling --no-progress //dangling ref
git fsck --unreachable --no-progress//dangling commits
git branch deletedbranch 12345
```
######Cherry-picking
cherry pick from b branch to master
```
git cherry-pick $(git merge-base master b)..b
```
######Resolving Conflicts
```
git merge --abort
```
#####Rewriting History
######Editing Commits
```
git rebase -i --root --autosquash
```
undo
```
git config --blobal alias undo '!f(){git reset --hard $(git rev-parse --abbrev-ref HEAD)@{@{1-1}};}; f'
```
