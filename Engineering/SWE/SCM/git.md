# git


## diff

```bash
git difftool abc123~1 abc123
```

## squash

### top N commits

```bash
git reset --soft HEAD~N
git commit
```

### Selected Commits

Select the commits for squash
```bash
git log --pretty=oneline
a931ac7c808e2471b22b5bd20f0cad046b1c5d0d c
b76d157d507e819d7511132bdb5a80dd421d854f b
df239176e1a2ffac927d8b496ea00d5488481db5 a
```

Here, a is the first commit, then b and finally c. After committing c we device to squash b and c together:
Run -
```bash
git rebase --interactive HEAD~2
```
Gives interactive editor with -
```bash
pick b76d157 b
pick a931ac7 c

# Rebase df23917..a931ac7 onto df23917
#
# Commands:
#  p, pick = use commit
#  r, reword = use commit, but edit the commit message
#  e, edit = use commit, but stop for amending
#  s, squash = use commit, but meld into previous commit
#  f, fixup = like "squash", but discard this commit's log message
#
# If you remove a line here THAT COMMIT WILL BE LOST.
# However, if you remove everything, the rebase will be aborted.
#
```
Changing b's pick to squash will result in the error you saw, but if instead you squash c into b (newer into the older) by changing the text to
```bash
pick   b76d157 b
squash a931ac7 c
```
and save-quitting your editor, you'll get another editor whose contents are
```bash
# This is a combination of 2 commits.
# The first commit's message is:

b

# This is the 2nd commit message:

c
```
When you save and quit, the contents of the edited file become commit message of the new combined commit:
```bash
$ git log --pretty=oneline
18fd73d3ce748f2a58d1b566c03dd9dafe0b6b4f b and c
df239176e1a2ffac927d8b496ea00d5488481db5 a
```

# Hashtags

#git #rebase #squash