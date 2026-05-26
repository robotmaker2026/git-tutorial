## Do it

Learn `git` by using many of its tools in an example project: submitting a recipe to our recipe book.

You will be using the terminal / command prompt for all of the `git` actions (as described in [setup](setup.md)).  Commands that you should enter into the terminal will be represented in code blocks like so:

```
$ pwd
```

You won't type the `$` character---it is usually provided to you by the terminal, but even if not we'll still use it as a placeholder to generically indicate the command prompt.  In this case, you would type the three letter command `pwd` then press the Enter key, and your terminal should respond with the full path to the folder you're in.

With that, let's get started.

- However you usually do it on your computer, create a folder to hold all the different repos you'll create in this course (perhaps named `RobotMaker2026`).

### Getting started

#### Getting started from scratch: `git init`

- Under the `RobotMaker2026` folder, create a new folder named `test-recipe`.  This folder will be the root of your new repo.

- Navigate to `RobotMaker2026/test-recipe` in a command prompt.

- **Initialize** a new, blank repo in that directory:
  ```
  $ git init
  ```

Congratulations, you have now created a new (blank) repo!  This repo will exist only on your computer, and give you access to all of the benefits of `git` (see the [overview](overview.md) if you need a refresher) in a fully offline way.

We'll handle content in the next section, but first let's look at other ways of getting started.

#### Building off of another repo: `git clone`

It turns out we've already created an outline for a recipe.  Rather than starting from nothing, you can build on our repo that lives at <https://github.com/robotmaker2026/my-recipe>.

- In the terminal, navigate back to the **parent directory** where you want this repo, i.e. `RobotMaker2026`
- **Clone** the existing repo to make a brand new one with the exact same history:
  ```
  $ git clone https://github.com/robotmaker2026/my-recipe.git
  ```

Hooray, you now have your own repo pre-populated with some files (and their history of commits).  Don't worry about the original owner anymore, it's all yours now.  You do not need any cloud service account to clone, and from this point on it lives offline, entirely on your own computer, as if you had done everything from the `git init` onwards yourself.

Note 1: The root of the new repo is now in the `my-recipe` subfolder of `RobotMaker2026`, though you're able to specify an alternate name for the root folder during the clone.  For the sake of the rest of this tutorial, delete the folder you just made here, or perhaps rename (move) it to `original-recipe`:
```
$ mv my-recipe original-recipe
```

Note 2: You can clone any existing git repo that you have access to, even the local repository created in the previous step.  Typically you will clone repos from online links though.

#### Adding some cloud: forking

If you want to be able to use the online Github services for yourself: instead of cloning directly from the original repo to your hard drive, **fork** the original repo into your Github account and clone that.

- After logging in to your Github account on the website, navigate in your browser to <https://github.com/robotmaker2026/my-recipe>

- Click on the button in the top right of the screen labeled "Fork".  (It will also have an icon and a number counting the current forks.)

- After forking, you should be taken to an identical repository, only this time under your account instead of ours.  You can now clone this to your local drive.  Copy the URL from the big green button labeled "&lt;&gt; Code" (note, the URL should be under the "SSH" tab, and will start `git@github.com:...`) then repeat the previous section but with that new URL instead of ours.

### Main workflow

Regardless of how you created your `git` repo, the typical workflow from that point on is the same, and is all handled offline and purely locally.

#### New content: `git add` / `git commit`

- Use whatever text editing software you like to create a new plain text file in the `my-recipe` folder named `ideas.md`.
    - **Do not** create a Word document, rich text format, pdf, or any other kind of file---ensure you save the file as "plain text".
    - The `.md` extension denotes a markdown file, which gives you intuitive formatting while still staying readable in plain text.

- For now, the text content of the file can be just a simple heading (including the pound sign `#` at the start of the line to indicate the top-level heading):
  ```
  # Ideas for my recipe
  ```

- Save the file and exit your text editor.

- Tell git about the file:
  ```
  $ git add ideas.md
  ```

- Create a commit with a helpful message indicating what has changed:
  ```
  $ git commit -m "Created initial blank document for food ideas"
  ```

Your repo is now doing something for you!  It is tracking a file, which so far has a history of one commit.  Let's do more with that file in the next section.

#### Making progress according to plan: `git status`

- Open your `ideas.md` file in your text editor

- Add several ideas for recipes by listing out all the foods you like---one per line, each preceeded by a dash `-`, e.g.:
  ```
  - Cereal
  - Fried eggs
  - Tacos
  - Mango lassi
  - ...
  ```

- Save the file and exit your text editor.

- Observe what has changed since your last commit (optional, but often helpful):
  ```
  $ git status
  ```

- Tell git that you'd like to commit the changes you made to the file:
  ```
  $ git add ideas.md
  ```

- Create a commit with a brief helpful message indicating what has changed:
  ```
  $ git commit -m "Started making a list of my favorite foods"
  ```

- Keep making changes to the file: sort and classify the list by type, e.g.:
  ```
  ## Breakfast
  - Cereal
  - Fried eggs
  ## Meals
  - Tacos
  ## Drinks
  - Mango lassi
  ```
  Note the two hashes `##` indicating a section heading.  Subsections can be indicated by three hashes `###`, and so on for further subdivisions, etc.  More options for markdown formatting can be found at e.g. <https://markdowncheatsheet.net/>.

- Create a new commit by adding the file then committing **with a helpful message**.

- Re-open the file, and edit the title to be more appropriate, i.e. "My favorite foods".  Save the file, but feel free to leave the text editor running.  In the terminal, add the file then commit with a helpful message.

- Make a few additional changes to content, formatting, or anything else for this list, adding and committing anytime you have completed a meaningful change to the content.  As always, use your commit messages to briefly summarize the change from the previous commit.

You now have a branch with multiple commits in your repo!  In case you missed it earlier, you can see the branch name from:
```
$ git status
```

Once you're happy with a list of your favorite foods, move on to the next step.

#### Helping future you: `git tag`

Commit messages tell us what has **changed since the last commit**.  Sometimes it may be helpful to know the **overall, cumulative state** of the repo.

- Let's leave a note to summarize where you have gotten so far:
  ```
  $ git tag -a favorites -m "The full list of my favorite foods, classified by type"
  ```
    - `-a` is telling git to add a new tag (actually `a` stands for annotate, but close enough)
    - The single word after `-a` is the tag **name**: a short identifier for us to refer to later
    - The **message** after `-m` is the note you're leaving to yourself

### Fancy undo

To show off the value of `git` when it comes to undoing mistakes, let's create some more edits.

- Decide that "drinks" (or some other category that you have) shouldn't count as a favorite food:  Open `ideas.md` in a text editor, delete that entire section, save and close, add, commit.
- Decide that you don't have enough options, so open `ideas.md` and add some more items to your list in the other categories you do have.  Save and close, add, commit.
- Decide that you should only list the foods you know how to make, so delete everything you don't.  Save and close, but **don't add or commit just yet**.

#### Seeing what has changed: `git diff`

After all that effort to list all your favorite foods, you just deleted a bunch of them!  What a waste of effort... let's try to get them back.

- (optional) Try re-opening the file and undo-ing that last delete from within your text editor.  You (probably) can't.
- See what is different between the last commit and your current working state:
  ```
  $ git diff
  ```
    - Note that by default you only see the difference between the last commit (i.e. HEAD) and the current working state, so after you've added and committed, the diff will be blank.
    - There are some formatting options available with `git diff` described in the [advanced](advanced.md) notes.

#### Fixing a current mistake: `git restore`

- Let's actually undo those changes, taking your file back to what it looked like at the end of your last commit:
  ```
  $ git restore ideas.md
  ```
- You can check the contents of the file and `git status` to see that the deleted text has been restored.

Hooray, disaster has been averted!

#### Seeing what you've done in the past: `git log`

- How did you get to your current state?  You can see every commit that you've made in this branch:
  ```
  $ git log
  ```
- There are additional options to format the log detailed in the [advanced](advanced.md) notes; one generic way to condense the output and add visual branch representation:
  ```
  $ git log --graph --oneline
  ```

#### Fixing a past mistake: `git show` / `git revert`

You deleted stuff in the past too, when you deleted the entire "drinks" section.  Let's bring that back too.

- Use `git log` to identify the commit where you deleted that section (good thing you used descriptive commit messages!), and note its hash: the long sequence of hexadecimal digits after the word "commit" in the full log, or the first 7 digits of that sequence at the start of the oneline text.

- (optional) Look at that specific change to verify that it is what you want to undo:
  ```
  $ git show <hash>
  ```
    - Replace `<hash>` with either the full or the short hash (don't include the angle brackets `<>`, those are just to indicate the placeholder in the above command).

- Undo that specific change:
  ```
  $ git revert --no-edit <hash>
  ```
    - Git will create a new commit with an auto-generated message.
    - If you leave out `--no-edit`, git will prompt you to edit the commit message in a text editor.

Even though there were other changes made afterwards, that specific change nevertheless got undone.  In this case, the revert could be cleanly applied as a new commit; you can use `git log` / `git show` to see what has happened.

#### Handling a conflict

Sometimes later commits edit the content in an earlier commit, in which case it's not clear how to undo the earlier commit.  `git` doesn't try to answer that question for you, instead forcing you to figure it out.

- Decide instead to delete the title altogether.  Save, add, commit.

- Try to revert the change to the title that you made way long ago.  Find the commit hash with `git log`, verify with `git show`, then try to undo it with `git revert`.

    - You asked `git` to undo a change on text that no longer exists; `git` doesn't know what you intend, so it shows an error.
    - `git` will provide two options for what you might mean: the status of that section of text before the first commit that you're trying to revert, and the status of that section of test after the last commit that edited that section.  However, it will be up to you to identify what you actually want.

- Open the file in the text editor to handle the conflict.  Find the conflicted section and the two options:
    - between "<<<<<< HEAD" and "======" is the latest state of that text section
    - between "======" and ">>>>>> parent of &lt;hash&gt; (&lt;message&gt;)" is the state of that text section before the commit you're trying to revert

- Edit the text section to what you actually want: choose one of the two options, or replace the entire section with something else entirely.  In the end, ensure that you've deleted the "<<<<<<", "======", ">>>>>>" lines.

- Indicate that you've changed the file:
  ```
  $ git add ideas.md
  ```

- Complete the revert:
  ```
  $ git revert --continue --no-edit
  ```

#### Bulk undo: `git reset`

Things started to go wrong when you started deleting content to go from favorite foods to recipe ideas.  Let's just go back to the way things were.  Luckily, you tagged that state back then, which makes things easier now:

```
$ git reset favorites
```

This tells git that the latest commit you want to keep is the one you'd tagged with the name "favorites".  It doesn't actually change any of the file contents, so a `git status` will show that the file has changes, and `git diff` will show you what those changes are.  If you really want to undo all those changes and return to the state of the repo at the tagged commit, you already know how to get rid of the un-committed changes:

```
$ git restore ideas.md
```

Note: You can `git reset` and `git restore` in a single command: `git reset --hard`.

### A cloud interlude

#### Single-player backup: `git push`

Since you initially cloned this repository from your Github account to your local drive, it might be nice to save your new commits back on your Github account.

- Send your new commits to Github:
  ```
  $ git push
  ```

You should be able to see all your new changes on your repo page on github.com.

#### Multiple devices: `git pull`

You can use git to synchronize between multiple clones of the same repository.  If you've cloned the same repo on two different devices (or maybe two separate directories on the same device), then added and pushed commits from one copy, you can fast forward your other copy by getting and applying all the newer commits since you cloned:

```
$ git pull
```

Note: this assumes that you only add, commit, and push on one clone at a time.  Otherwise, you're entering the realm of parallel changes, which we'll look at in the next section.

### Trying things in parallel

Now that your "ideas" document contains a list of your favorite foods, let's start making a recipe.  Pick the food you want to submit the recipe for.

- Open `README.md` in a text editor and delete all the ingredients and steps for the example recipe, leaving the section headings in place.  Replace the title with the name of the food you'll be creating.  Save, add, and commit.

- Edit `README.md` to include the list of ingredients for your food.  Save, add, and commit.

#### Creating a new option: `git switch`

Invent a simple modification to the default recipe by adding a single ingredient (perhaps garlic, cinnamon, chocolate, or cheese?).

- Create a new branch to be explore that variant:
  ```
  $ git switch -c <branchname>
  ```
    - Replace `<branchname>` with a single (possibly hyphenated) word identifier for the variant, e.g. `plus-garlic` or `chocolatey`.
    - `-c` is used to simultaneously create the branch and switch to it.

- Edit `README.md` to add the extra ingredient to the ingredient list.  Save, add, commit.

#### Going between options: `git switch`

- Be sure to close the text editor to avoid confusing it.  The file itself will be directly modified by `git` behind the scenes.

- Return to the original recipe in progress:
  ```
  $ git switch main
  ```

- Reopen `README.md`, and note that the additional ingredient is no longer in the list.  Add the instructions for the original recipe to the file.  Save, add, commit.

- (optional) View your parallel realities using the git log, noting the fork in the lines between the named branches:
  ```
  $ git log --graph --abbrev-commit --branches --pretty=oneline
  ```

#### Bringing things together: `git merge`

- Return to the variant you're exploring:
  ```
  $ git switch <branchname>
  ```

- View `README.md` (but close again afterwards); note that the additional ingredient is back on the list but the newly added instructions are gone.  This was the most recent state of the repo while you were on that branch before.

- Incorporate the changes you made to the other branch in this one too:
  ```
  $ git merge main
  ```
    - In this case, the parallel changes didn't overlap / interfere.  Much like `git revert` though, you may end up with merge conflicts.  If so, you would resolve them in the same way.

- Open `README.md` and add the additional instruction(s) where you use the new ingredient in the recipe.  Save, add, commit.

- (optional) See the latest representation of your parallel variants using `git log`.

#### (Optional) Choosing one: `git branch`

- If you would like to uniquely settle on one of your branches, you can remove the other.  By convention, we will stick to `main` being the unique branch, so get back on that branch:
  ```
  $ git switch main
  ```

- If that is the recipe variant you want to stick with, you're set for now.  If you'd prefer the other variant though, incorporate all of those changes into the current branch:
  ```
  $ git merge <branchname>
  ```

- Get rid of (delete) the other branch:
  ```
  $ git branch -d <branchname>
  ```

Note 1: If you didn't merge those changes into main, `git` will refuse to delete (to protect you from yourself).  It will tell you how to override its refusal if you really mean to delete the other branch and lose its commits forever(*).

(*) Note 2: Not actually, but that's a more advanced topic.

### More cloud things

You've created your recipe, now it's time to edit our recipe book to include it.  You're going to work with us (within the Github ecosystem) to make that happen.

#### Communication: issues

Tell us that you'd like us to include your recipe in our book.

- Navigate to our recipe book's Github page at <https://github.com/robotmaker2026/recipe-book> and click the "Issues" tab (i.e. <https://github.com/robotmaker2026/recipe-book/issues>).

- Click the big green button labeled "New issue".

- In the description, explain in detail what you want us to consider (e.g. "Add a recipe for &lt;food&gt; in the category &lt;category&gt;")

- Give a short descriptive title of the request (e.g. "Feature request: &lt;food&gt;")

- Click the green "Create" button, then note the issue number of the newly created issue.

#### Contributing: merge / pull requests

(Politely) add your recipe to our book yourself.

- Edit our recipe book to include your new recipe: fork, `clone`, `edit`, `add`, `commit`, `push` the recipe book repo from <https://github.com/robotmaker2026/recipe-book> with the name of the food, the link to your recipe repository, and your name.  Feel free to add to an existing category or make a new one as you see fit.

- Navigate to your Github fork of our recipe-book repo on github.com, and click on the "Pull requests" tab.

- Click the big green "New pull request" button.

- Make sure the left-hand branch shows the original recipe-book repo (under the `RobotMaker2026` organization) and the right-hand branch shows the branch you modified in under your Github account.

- Check the tabs for "&lt;m&gt; commit(s)" and "&lt;n&gt; file(s) changed" to ensure you're only making the minimal relevant number of changes.  If it all looks good, click the big green "Create pull request" button.

- Give a brief title and a detailed descriptive comment of your proposed change.  In the description, refer to the issue number that you filed earlier requesting the change you're addressing by including the key phrase "Resolves #&lt;issue number&gt;".
    - Use the issue number from the previous section; Github might help with relevant tooltips.
    - There are other keywords that will all do the same thing; feel free to use a different one if it better describes what your change does: <https://docs.github.com/en/issues/tracking-your-work-with-issues/using-issues/linking-a-pull-request-to-an-issue>

- Click the big green "Create pull request" button.
