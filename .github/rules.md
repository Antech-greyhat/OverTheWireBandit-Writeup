# Writeup rules

Follow the [OverTheWire rules](https://overthewire.org/rules/). Credit the [OverTheWire community](https://overthewire.org/), use original explanations, and never publish game passwords.

## Keep each walkthrough simple

1. Name the starting account and next account, and link the official challenge.
2. Show the commands used in the actual session.
3. Explain the commands in a short table. Break a long command into its useful parts.
4. Add one working backup and a cropped screenshot with opaque password redaction.
5. Show how to connect to the next account from the local terminal.

## Explain commands with a table

For example:

```bash
find . -type f -size 1033c ! -executable -exec file {} + | grep "ASCII text"
```

| Part | Simple explanation |
| --- | --- |
| `find .` | Search the current directory and its subdirectories. |
| `-type f` | Select regular files. |
| `-size 1033c` | Select files that are exactly 1033 bytes; `c` means bytes. |
| `! -executable` | Exclude files the current user can execute. |
| `-exec file {} +` | Run `file` on the matches in batches; `{}` holds the matched paths and `+` ends the action. |
| `\|` | Send the file descriptions to the next command. |
| `grep "ASCII text"` | Keep lines whose description contains `ASCII text`. |

## Explain result paths

Use the same format when a command returns a path, such as `/var/lib/dpkg/info/bandit7.password`:

| Part | Simple explanation |
| --- | --- |
| `/` | Start at the filesystem root. |
| `var/lib/` | Application state data. |
| `dpkg/info/` | Debian package metadata; this is where the example file was found. |
| `bandit7.password` | The filename. |
| A trailing `:` in `file` output | Separate the filename from its file-type description; leave it out when opening the file. |
| `cat /var/lib/dpkg/info/bandit7.password` | Print the file's contents; redact the password output before publishing. |

## Before committing

- Check `git status --short` and review the exact files being staged.
- Keep `.gitignore` limited to local files or directories that actually exist. Keep raw screenshots and private notes outside the repository.
- Check relative links and explain only commands that were used or verified.
- Review every exported screenshot. Replace password pixels with solid blocks, export a fresh image, and remove embedded text metadata.
- Put each newly solved level in its own commit and PR. Group repository-wide style or rule updates in a separate PR. Include this trailer on each commit:

```text
Co-authored-by: technorant <223033055+technorant@users.noreply.github.com>
```

## Pull requests

Describe why the change is needed, what changed, and what was checked. State whether command checks used harmless local examples or a live Bandit session. Keep passwords and original screenshots out of the PR and its commit history.
