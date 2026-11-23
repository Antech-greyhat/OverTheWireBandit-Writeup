# Level 0 — SSH setup and the first file

**Session:** `bandit0` → `bandit1` · [Official setup](https://overthewire.org/wargames/bandit/bandit0.html) · [Official challenge](https://overthewire.org/wargames/bandit/bandit1.html)

## Level goal

### SSH setup — Bandit Level 0

From the [official setup page](https://overthewire.org/wargames/bandit/bandit0.html). The initial password is omitted from this quotation; read it on the source page.

> The goal of this level is for you to log into the game using SSH. The host to which you need to connect is **bandit.labs.overthewire.org**, on port 2220. The username is **bandit0** and the password is **[omitted; see official setup]**. Once logged in, go to the [Level 1](https://overthewire.org/wargames/bandit/bandit1.html) page to find out how to beat Level 1.

### First file — Bandit Level 0 → Level 1

From the [official challenge page](https://overthewire.org/wargames/bandit/bandit1.html):

> The password for the next level is stored in a file called **readme** located in the home directory. Use this password to log into bandit1 using SSH. Whenever you find a password for a level, use SSH (on port 2220) to log into that level and continue the game.

## Connect

Run this in your local terminal with an SSH client installed:

```bash
ssh -p 2220 bandit0@bandit.labs.overthewire.org
```

`-p 2220` selects Bandit's SSH port; `bandit0` is the account. Use the initial password from the official setup page. The password prompt does not display what you type.

On a first connection, SSH asks about the server's host key. Verify that you are connecting to the intended host before accepting it.

![SSH connection command; authentication output redacted](../assets/level-0/ssh-setup.png)

## Commands I used

In the remote `bandit0` home directory:

```bash
ls
cat readme
```

| Command | Simple explanation |
| --- | --- |
| `ls` | List files in the current directory. |
| `cat readme` | Print `readme`, which contains the password for `bandit1`. |

![Listing the directory and reading readme; all file output redacted](../assets/level-0/readme.png)

## Backup

```bash
cat < readme
```

The shell opens `readme` as standard input, and `cat` prints it. This reads the same contents.

## Continue

Save the recovered password privately. Return to your local terminal with any of these options, tested in a Bandit SSH login shell:

| Option | How to use it |
| --- | --- |
| `exit` | Type the command and press Enter to end the remote shell. |
| `logout` | Type the command and press Enter in the SSH login shell. |
| `Ctrl+D` | Press at an empty shell prompt to end the remote shell. |

Then connect from your local terminal:

```bash
ssh -p 2220 bandit1@bandit.labs.overthewire.org
```

Enter the password at the prompt. [Back to the index](../README.md)
