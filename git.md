## Do it

Learn `git` by using many of its tools in an example project: submitting a recipe to our recipe book.

We will be using the terminal / command prompt for all of our `git` actions (as described in [setup](setup.md)).  Commands that you should enter into the terminal will be represented in code blocks like so:

```
$ pwd
```

You won't type the `$` character---it is usually provided to you by the terminal, but even if not we'll still use it as a placeholder to generically indicate the command prompt.  In this case, you would type the three letter command `pwd` and press `<enter>`, and your terminal should respond with the full path to the folder you're in.

With that, let's get started.

However you usually do it on your computer, create a folder to hold all the different repos you'll create in this course (perhaps named `RobotMaker2026`).

### Main workflow

#### Getting started from scratch: `git init`

- Under the `RobotMaker2026` folder, create a new folder named `recipe-ideas`.  This new folder will be the root of your first repo.

- Navigate to `RobotMaker2026/recipe-ideas` in a command prompt.

- **Initialize** a new, blank repo in that directory:
  ```
  $ git init
  ```

Congratulations, you have now created a new (blank) repo!  This repo will exist only on your computer, and give you access to all of the benefits of `git` (see the [overview](overview.md) if you need a refresher) in a fully offline way.

We'll start adding content in the next section.

#### Your first content: `git add` / `git commit`

- Use whatever text editing software you like to create a new plain text file in the `recipe-ideas` folder named `ideas.md`.
    - **Do not** create a Word document, rich text format, pdf, or any other kind of file---ensure you save the file as "plain text".
    - The `.md` extension denotes a markdown file, which gives you intuitive formatting while still staying readable in plain text.

- For now, the text content of the file can be just a simple heading (including the pound sign `#` at the start of the line to indicate the top-level heading):
  ```
  # Ideas for the recipe book
  ```

- Save the file and exit your text editor.

- Tell git about the file:
  ```
  $ git add ideas.md
  ```

- Create a commit with a helpful message indicating what has changed:
  ```
  $ git commit -m "Created initial blank document"
  ```

Your repo is now doing something for you!  It is tracking a file, which so far has a history of one commit.  Let's do more with that file in the next section.

#### Making progress according to plan: `git status`

- Open your `ideas.md` file in your text editor

- Add several ideas for recipes, by listing out all the foods you like---one per line, each preceeded by a dash `-`, e.g.:
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

- Create a commit with a helpful message indicating what has changed:
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

- Create a new commit by adding the file then committing with a helpful message.

- Feel free to make additional changes to content, formatting, or anything else for this list, adding and committing anytime you have completed a meaningful change to the content.

You now have a branch with multiple commits in your repo!  In case you missed it earlier, you can see the branch name from:
```
$ git status
```

Once you're happy with a list of your favorite foods, move on to the next step.

#### Helping future you: `git tag`

Commit messages tell us what has changed since the last commit.  Sometimes it may be helpful to know the overall, cumulative state of the repo.

- Let's leave a note to capture where we are so far:
  ```
  git tag -a favorites -m "The full list of my favorite foods, classified by type"
  ```
    - `-a` is telling git to **add** a tag
    - The single word after `-a` is the tag **name**: a short identifier for us to refer to later
    - The **message** after `-m` is the note we're leaving to ourselves

### Fancy undo

To show off the value of `git` when it comes to undoing mistakes, let's create some more edits.

- Decide that "drinks" (or some other category that you have) shouldn't count as a favorite food:  Open `ideas.md` in a text editor, delete that entire section, save and close, add, commit.
- Decide that you don't have enough options, so open `ideas.md` and add some more items / categories to your list.  Save and close, add, commit.
- Decide that you should only list the foods you know how to make, so delete everything you don't.  Save and close, but don't add or commit just yet.

#### Seeing what has changed: `git diff`

After all that effort to list all your favorite foods, you just deleted a bunch of them!  What a waste of effort, let's try to get them back.

- (optional) Try re-opening the file and undo-ing that last delete.  You (probably) can't.
- See what is different between the last commit and your current working state:
  ```
  $ git diff
  ```
    - Note that by default you only see the difference between the last commit (i.e. HEAD) and the current working state, so if you've added and committed, the diff will be blank.
    - There are many more things you can do with `git diff` which we will save for advanced `git`.

#### Fixing a current mistake: `git restore`

- Let's actually undo those changes, taking our file back to what it looked like at the end of our last commit:
  ```
  $ git restore ideas.md
  ```

Hooray, disaster has been averted!

#### Seeing what you've done in the past: `git log` / `git show`

- How did we get to our current state?  We can see every commit that we've made in this branch:
  ```
  $ git log
  ```
- There are many options to format the log; one quick way to condense the output a bit:
  ```
  $ git log --graph --abbrev-commit --branches --pretty=oneline
  ```

#### Fixing a past mistake: `git revert`

We deleted stuff in the past too, when we deleted the entire "drinks" section.  Let's bring that back too.

- Use `git log` to identify the commit where we deleted that section, and note its hash: the long sequence of hexadecimal digits after the word "commit" in the full log, or the first 7 digits of that sequence at the start of the oneline text.
- Undo that specific change:
  ```
  $ git revert <hash>
  ```
    - Replace `<hash>` with either the full or the short hash (don't include the angle brackets `<>`, those are just to indicate the placeholder in the above command).

#### Fixing lots of mistakes: `git reset`

### Using the cloud part 1:

#### Building off something existing: `git clone`

Sometimes you don't want to start from a new blank repo, but make changes on an existing repo.  In this case we'll build on the repo that lives at <>.

- In the terminal, navigate to the **parent directory** where you want this repo, i.e. `RobotMaker2026`
- **Clone** an existing repo to make a brand new one with the exact same history:
  ```
  $ git clone
  ```

Hooray, you now have your own repo pre-populated with some files (and their history of commits).  Don't worry about the original owner anymore, it's all yours now.

Note 1: the root of the new repo is now in the `` subfolder of `RobotMaker2026`.

Note 2: we could also have chosen any existing git repo to clone, even the one we created in the previous step.  Typically we will clone repos from online links though.

### Trying things in parallel

#### Creating a new option: `git branch`

#### Going between options: `git switch`

#### Bringing things together: `git merge`

### Using the cloud

#### Single-player backup: `git push`

#### Multiple devices: `git pull`

#### If things went parallel: `git fetch`

#### Clone in the cloud: fork

#### Being polite: merge / pull requests

#### Communication: issues
