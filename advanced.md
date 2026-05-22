## Git tricks

Here is a (very small) selection of additional `git` commands that I have found to improve my workflow.  Feel free to submit pull requests if you have additional tricks!

### Additional command options

#### `git add -p`

Sometimes you find yourself taking a slight detour when editing a file, e.g. noticing and fixing a typo somewhere else while in the midst of a bigger edit.  You might want to snapshot the typo fix as a separate commit so it doesn't get lost with the bigger edit, making it harder to potentially undo later.  Instead of using `git add` to add the entirety of the changes made to a file, `git add -p` (for **p**atch) will step you through each change separately, allowing you to add or ignore it when you next commit.

If you've used `git add -p` and selectively chosen some sections of the same file to add and others to not, `git status` will show that file both in the staging area as well as having uncommitted changes.

This only separates edits by splitting across unchanged sections of the file.  If you want finer resolution than that, `git add -p` also offers an option to `e`dit an individual changed chunk, which is powerful but out of the scope of this tutorial.

#### `git diff`

By default, `git diff` shows changes by line.  Sometimes you want to see only which words within a line have changed; this is especially useful for small changes and/or long lines.  To do that:
```
$ git diff --color-words
```

This command allows an option to specify what constitutes a "word", but that is out of the scope of this tutorial.  Look it up if you find yourself still unhappy about how the diffs appear on your screen.

If you find yourself doing this a lot, you can set this up as an explicit command, e.g. `git wdiff`:

```
$ git config --global alias.wdiff "diff --color-words"
```

This allows you to directly call the alias, i.e.:
```
$ git wdiff
```

#### `git log`

If you think the full `git log` shows too much information, but the shorter `git log --oneline` leaves out too much (in particular, committer info and date), there are a huge number of formatting options at your disposal.  I like to use this:
```
$ git log --graph --pretty=format:'%C(auto)%h %Cgreen(%ar) %C(cyan)<%an>%Creset %s %C(auto)%d%Creset'
```

As above, you can make this a global alias:
```
$ git config --global alias.lgb "log --graph --pretty=format:'%C(auto)%h %Cgreen(%ar) %C(cyan)<%an>%Creset %s %C(auto)%d%Creset'"
```

Note: the `--graph` in the command is what shows all the branching in your repo, hence the `b` at the end of the `lgb` alias.  It's easy enough to make another alias `lg` that does not include the `--graph` option and so will only show a single sequence of commits.

### Additional commands

#### `git stash`

Any `git` command that changes the files on disk (i.e. `revert`, `reset`, `pull`, `merge`, `switch`) **requires** that the working state be **clean**, i.e. that all changes are added and committed.  Sometimes you might decide that you want to do something unrelated in the middle of a longer edit that needs one of those commands, even though you're not at a good place to create a tidy logical commit.  A typical solution would be to add what you have, commit it with a message indicating that you're only partially through your intended edit (perhaps noting that it's a Work In Progress with the keyword "WIP"), do your other action, then finish what you were doing with a final commit.  This ends up splitting a single logical action across multiple commits, making it harder to undo should you need to.

An alternate option is to pause what you're doing, do the other thing, and then resume where you left off:

```
$ git stash
$ <other git things>
$ git stash pop
```

The first `git stash` command stores the current working state of your repo behind the scenes, but then returns the repo to the outcome of the last commit (as if you'd done a `git restore`, but without losing the changes forever).  This allows you to do whatever other git operations you want.  Then when you're ready to return, `git stash pop` tries to bring back the changes it had stashed earlier.  The same merge conflict and resolution process will apply.  If there was no conflict, the saved stash data will be deleted since it has been applied to the current working state, otherwise git will keep it just in case.

You can cascade the `stash` and `pop` operations, but that's out of the scope of this tutorial.

#### `git cherry-pick`

If you want to apply a single commit (typically from a different branch) onto your current working state without having to merge the whole thing:

```
$ git cherry-pick <hash>
```

Will try to merge the single commit into your current branch.  Similar merge conflicts and resolution processes apply.

If you want to bring over the changes without explicitly commiting the results, the `-n` option i.e. `$ git cherry-pick -n` brings over the changes without actually adding / committing, leaving the changes as "not staged for commit".

#### `git rebase`

**Warning: here be dragons**

Sometimes a different branch will have a bunch of commits, all before the branch you're currently working on has any.  You could merge them in, but that creates a fork in the history and an extra commit.  It is an accurate representative of your editing process, but it's a bit ugly to look at.  If you want to keep the history pretty looking, you can **fast-forward** your branch to the end of the other one, as if you'd done the `git switch -c` after all the other changes (instead of before) with:
```
$ git rebase <hash>
```
(as opposed to a `git merge`).

If you actually haven't made any changes on your new branch, this will be just fine.

You can try to do this even if you have made some changes, and it will probably work, especially if your changes and the other branch's changes are in different parts or different files.  If not though, and you encounter a merge conflict, you're probably going to have a bad time.  A resolution process exists but it can occasionally be a lot more complicated.  Best to stay away in that case, and stick with a regular `git merge` instead.

### Git configuration and utilities

#### `.gitignore`
