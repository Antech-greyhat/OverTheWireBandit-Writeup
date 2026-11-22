# Level 1 — Reading a file named `-`

**Session:** `bandit1` → `bandit2` · [Official challenge](https://overthewire.org/wargames/bandit/bandit2.html)

Start in the remote `bandit1` home directory, using the password you recovered in Level 0.

## Commands I used

```bash
ls
cat ./-
```

`ls` shows a file named `-`. A bare `cat -` reads standard input, so it waits for keyboard input instead of opening that file.

`./-` is a path: `./` means the current directory. Giving `cat` that path makes it open the actual file and print the password for `bandit2`.

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
