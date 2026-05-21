## Setup

### The command line

There are certainly many graphical frontends (GUIs) to the `git` tool, and some are even useful.  Nonetheless, `git` was primarily developed to be used at the command line (equivalently: terminal prompt); I find that hiding those command details behind an interface is responsible for much of the confusion and complaints about `git` being black magic.  As such, in this tutorial we will **exclusively focus on command line** interactions with `git`.  Hopefully this will help you make better sense of how `git` can make your life better.  Once you understand the core concepts, and workflow, feel free to migrate to other interfaces as you see fit.

#### Accessing the command line

- For MacOS, use the Terminal app that comes installed by default
- For Windows, I recommend PowerShell: <https://learn.microsoft.com/en-us/powershell/scripting/install/install-powershell-on-windows?view=powershell-7.6>
- For linux, you have your option of many terminal emulators; use whichever one you like or comes default on your install.

### Installing `git`

A comprehensive guide to your options to install `git` can be found at <https://git-scm.com/book/en/v2/Getting-Started-Installing-Git>.  I have nothing further to add---follow those instructions.

### Configuring `git`

#### Commands

Open up a terminal and run these five commands, making the appropriate substitutions for the text inside the angle brackets &lt;&gt;.

```
$ git config --global user.name "<your name>"
$ git config --global user.email "<your email>"
$ git config --global init.defaultBranch main
$ git config --global core.fileMode false
$ git config --global core.autocrlf <mode>
```

- Replace the strings inside the angle brackets &lt;&gt; with your choice of identification, leaving the quotes "" around them.  Note that if you (intend to) use Github or any other public facing cloud service, this information will be publicly visible forever, so choose accordingly between contactability and privacy.  There is no validation of either of these strings, so what you choose can be entirely arbitrary.

- If you are on MacOS or linux the autocrlf mode should be `input`; Windows users set the autocrlf mode to `true`, i.e.:
  ```
  $ git config --global core.autocrlf input
  ```
  --- or ---
  ```
  $ git config --global core.autocrlf true
  ```

#### Explanations

- Lines 1 and 2: User details
    - Every commit includes author details, so you need to tell `git` what to put there.

- Line 3: Updated convention
    - The convention currently is to have the single / initial / most relevant branch named `main`

- Lines 4-5: Handling Windows/Mac/Linux quirks
    - The different operating systems deal with files differently; these defaults make your `git` life less cluttered should you use different computers with the same repository.
    - Line 4 ignores differing file system modes (that describe file access permissions in different ways) across the different operating systems.
    - Line 5 deals with the different newline / line ending chacracters across the different operating systems

Any of these settings can be overridden within a specific repository by running the command in that repo with a new value and without the `--global` flag, i.e.:
```
$ git config user.email "myemail+thisproject@example.com"
```
