# Writeup rules

Follow the [OverTheWire rules](https://overthewire.org/rules/). Credit the [OverTheWire community](https://overthewire.org/), use original explanations, and never publish game passwords.

## Keep each walkthrough simple

1. Name the starting account and next account, and link the official challenge.
2. Add a `## Level goal` section before the connection instructions or solution, quoting the complete official question as described below.
3. Show the commands used in the actual session.
4. Explain the commands in a short table. Break a long command into its useful parts.
5. Add one working backup and a cropped screenshot with opaque password redaction.
6. Show how to connect to the next account from the local terminal.

## Include the precise official question

- Fetch the current **Level Goal** from the matching [Bandit challenge page](https://overthewire.org/wargames/bandit/). Quote the complete goal in a Markdown blockquote and credit OverTheWire with a source link immediately above it.
- Match the source to the account transition: `levels/level-N.md` covers `banditN` → `banditN+1`, whose official goal is at `https://overthewire.org/wargames/bandit/bandit{N+1}.html`. Level 0 also includes the SSH setup goal from `bandit0.html`, separately labelled.
- Preserve the exact wording, filenames (including spaces, dots, dashes, and case), paths, users, groups, byte counts, constraints, and tips. Keep lists as lists; formatting and whitespace may change, but the question's meaning must not. Do not paraphrase the goal, invent requirements, or substitute an older version.
- Omit any password in the source and mark its place with `[omitted; see official setup]` or an equally explicit source link. Explain the omission next to the quotation; all other goal text must remain complete.
- Keep the quoted question separate from your own explanation and commands. If the current goal differs from the recorded session, state the difference outside the quotation and preserve the actual session commands.

For example, the `bandit5` → `bandit6` question belongs before the Level 5 solution:

```markdown
## Level goal

From the [official challenge page](https://overthewire.org/wargames/bandit/bandit6.html):

> The password for the next level is stored in a file somewhere under the **inhere** directory and has all of the following properties:
>
> - human-readable
> - 1033 bytes in size
> - not executable
```

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
- Compare the quoted question against the current official Level Goal. Check the account transition, exact filenames, all conditions and tips, source attribution, and any explicitly marked password omission.
- Review every exported screenshot. Replace password pixels with solid blocks, export a fresh image, and remove embedded text metadata.
- Put each newly solved level or update to an existing level in its own branch, commit, and PR, based on the repository's default branch. Stage only that level's files. Group repository-wide style or rule updates in a separate branch and PR. Include this trailer on each commit:

```text
Co-authored-by: technorant <223033055+technorant@users.noreply.github.com>
```

## Pull requests

Describe why the change is needed, what changed, and what was checked. State whether command checks used harmless local examples or a live Bandit session. Keep passwords and original screenshots out of the PR and its commit history.
