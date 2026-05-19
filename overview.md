## Overview

### What is `git`

`git` is a tool that runs on your computer that lets you do two things very well:

- undo anything
- try different things in parallel

These two are basically what people mean when they call `git` a "distributed version control system (DVCS)".  But if that's too verbose, you can just stick to "`git` is a fancy undo."

* Note 1: `git` only works on text files (which nonetheless does allow for a lot of non-text media such as SVG images, markdown based presentations, and more.)
* Note 2: `git` is typeset in a fixed point font to indicate that it's a tool that you'll run locally on your own computer (as opposed to on someone else's server i.e. "in the cloud").

#### What is Github

**Github** is an online multiplayer ecosystem ("cloud service") that helps with communication, coordination, sharing, and other features relevant for `git` users working together.  It also provides a few other tools to augment the core `git` functionality.

Github is not `git`, and `git` is not Github.  You may find occasions to use either indepently, or both in conjunction.

Most of this tutorial will focus on using `git` as a standalone tool, but there will be some sections on using the relevant collaborative elements of Github.

### Why to `git`

At some point, you will make a mistake.  `git` will help you recover.

And when it's easier to recover from a mistake, you'll probably be less hesitant to try things that might be mistakes.  You might end up more creative, more efficient, or more relaxed.

### Glossary

- **Repository (repo)**: A collection of files that you have told `git` about.  These files may be organized in nested / hierarchical folders, but they will all be under a single top-level folder.

- **Root**: That top-level folder.

- **Project**: A collection of files all logically related to a single purpose (however you define it).  You might have one project in one repository, multiple projects in one repo, or one project spread across several repos.

- **Commit**: A timestamped snapshot of all the files your repo.  More precisely, it's actually a snapshot of the changes to your files since the previous commit.

- **Branch**: A connected sequence of commits tracing back to the initial commit in a repo.

- **HEAD**: The most recent commit that you've been working from.

- **Hash**: A long random hexadecimal string that identifies a commit.
