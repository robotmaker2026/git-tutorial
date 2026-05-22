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

#### `git cherry-pick`

#### `git stash`

#### `git rebase`

### Git configuration and utilities

#### Fast-forward

#### `.gitignore`
