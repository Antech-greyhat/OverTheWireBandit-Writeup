# Level 1 — Reading a file named `-`

**Session:** `bandit1` → `bandit2` · [Official challenge](https://overthewire.org/wargames/bandit/bandit2.html)

Start in the remote `bandit1` home directory, using the password you recovered in Level 0.

## Commands I used

```bash
ls
cat ./-
```

| Command | Simple explanation |
| --- | --- |
| `ls` | List the files, including the one named `-`. |
| `cat ./-` | Open the file named `-` in the current directory and print its contents. |

`./` means the current directory. A bare `cat -` reads standard input, so it waits for keyboard input instead of opening the file.

![Reading the dash-named file with cat ./-; password output redacted](../assets/level-1/dashed-filename.png)

## Backup

```bash
cat < -
```

The shell opens the file named `-` and sends its contents to `cat` through standard input. Quoting `"-"` or using `cat -- -` still leaves `cat` with its special standard-input operand.

## Continue

Save the password privately, run `exit`, and connect from your local terminal:

```bash
ssh -p 2220 bandit2@bandit.labs.overthewire.org
```

Enter the recovered password at the prompt. [Back to the index](../README.md)
