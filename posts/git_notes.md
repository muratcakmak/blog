---
title: Git notes
publish_date: 2019-03-14
description: Personal notes on Git
---

### Random Git Notes for my future self

_Merging_ is the process of taking two separate branches and combining them into one branch. This process is used in Git to incorporate changes from one branch into another

_Rebasing_ is the process of taking all the changes committed on one branch and applying them onto another. This means that the original branch is "rebased" onto the new branch, which may contain additional changes. The result is a single branch with all the changes from both branches, without any merging.

Some teams opt for rebasing over merging with the main branch. Both approaches have advantages and disadvantages.

Pros:

- Rebasing can help reduce merge conflicts, since only one branch (the new one) will be modified.
- Rebasing keeps the commit history clean and linear, which makes it easier to navigate.
- Rebasing is faster than merging, since only one branch is modified

Cons:

- Rebasing can be tricky and difficult to understand.
- Rebasing can also be dangerous, since it can potentially overwrite or discard important commits.
- Rebasing requires a greater level of expertise to execute correctly.

#### .gitignore

Git sees every file in your working copy as one of three things.

- Tracked
- Untracked
- Ignored

#### Ignoring a previously committed file

```bash
$ echo debug.log >> .gitignore
$ git rm --cached debug.log
rm 'debug.log'
\$ git commit -m "Start ignoring debug.log"
```

### Undoing commits & changes

#### Aborting merge conflict

```bash
git reset --hard HEAD

git reset
```

#### Reverting a rebase

```bash
git reflog
git reset —hard HEAD@{2}
```

#### Remove all your local git branches but keep main

It can be in the `.zshrc` or `.bashrc` file as an alias for the convenience.

```bash
git branch | grep -v "main" | xargs git branch -D
```

#### Push a rebased local branch by using `--force-with-lease`

```
git push —force-with-lease
```

#### Polish my git feature branch before merging or submitting for review

```
git rebase -i COMMITHASH
```

to the commit

```
git commit —fixup COMMITHASH
```

```
git rebase -i —autosquash COMMITHASH
```

#### Auto Squash

```
git merge --squash app-refactoring
```

#### To take out entire commit

```
`git reset HEAD~`
```

Undo a commit that has already been pushed to the remote repository

```
git revert c011d0f
```

Temporarily store some work in progress because I have to jump to another branch

```
git stash
git stash list
git stash pop
git stash apply
```

Delete all the branches other than main

```
git branch | grep -v "main" | xargs git branch -D
```

Keep the file as is in the main, exclude local changes from git

```
# To skip git
git update-index --skip-worktree <file>

# Revert
git update-index --no-skip-worktree <file>
```

```
# To find commits of the author
git log --author=Oguzhan

# Check commit with message
git show --color --pretty=format:%b c2b88ed806fb5728a376bddab0c0e6d13d1ee15a

```

List all the commit from a specific commit on without commit hash

```
git log --pretty=oneline  commit-hash..HEAD --format="$ad- %s [%an]"
```
