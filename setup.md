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


--- 
### GitHub SSH Setup

To use GitHub from the command line, configure an **SSH key**. This lets GitHub authenticate you when you clone, pull, or push using SSH without needing to type your password every time.

#### 1. Check for existing SSH keys
Open your terminal and check if you already have an SSH key:

- **Windows (PowerShell)**, **macOS**, or **Linux**:
  ```bash
  ls ~/.ssh
  ```

If you see files like `id_ed25519.pub` or `id_rsa.pub`, you already have a key.

#### 2. Generate a new SSH key
If you don't have one, run this command (replace `<your email>` with your actual GitHub email):

```bash
ssh-keygen -t ed25519 -C "<your email>"
```

- Press **Enter** to accept the default file location.
- (Optional) Enter a passphrase for extra security, or press **Enter** twice to leave it blank.

#### 3. Copy the SSH public key
You need to copy the contents of your **public** key file (`id_ed25519.pub`) to your clipboard.

- **Windows (PowerShell)**:
  ```powershell
  Get-Content ~/.ssh/id_ed25519.pub | Set-Clipboard
  ```
- **macOS**:
  ```bash
  pbcopy < ~/.ssh/id_ed25519.pub
  ```
- **Linux**:
  ```bash
  cat ~/.ssh/id_ed25519.pub
  ```
  *(Then manually select and copy the output)*

#### 4. Add the key to your GitHub account
1. Go to [GitHub Settings](https://github.com/settings/keys).
2. Click **New SSH key**.
3. Give it a title (e.g., "My Laptop").
4. Paste your key into the **Key** field.
5. Click **Add SSH key**.

#### 5. Test the connection
Verify that everything is set up correctly:

```bash
ssh -T git@github.com
```

If successful, you'll see: `Hi <username>! You've successfully authenticated, but GitHub does not provide shell access.
.`
