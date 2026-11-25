# OverTheWire Bandit Writeups

Concise notes from my [Bandit](https://overthewire.org/wargames/bandit/) sessions: the commands I used, why they work, and one working backup for each challenge.

> **Spoilers:** These walkthroughs explain solutions. All passwords are hidden.

## Walkthroughs

The level number follows the account I start from. Level 0 includes the SSH setup and the `bandit0` → `bandit1` challenge.

| Writeup | Session | Focus |
| --- | --- | --- |
| [Level 0][level-0] | `bandit0` → `bandit1` | SSH setup and reading `readme` |
| [Level 1][level-1] | `bandit1` → `bandit2` | A file named `-` |
| [Level 2][level-2] | `bandit2` → `bandit3` | Spaces and leading dashes in a filename |
| [Level 3][level-3] | `bandit3` → `bandit4` | Hidden files |
| [Level 4][level-4] | `bandit4` → `bandit5` | Finding the readable file |
| [Level 5][level-5] | `bandit5` → `bandit6` | File size and executable permissions |
| [Level 6][level-6] | `bandit6` → `bandit7` | File owner, group, and size |
| [Level 7][level-7] | `bandit7` → `bandit8` | Finding the millionth entry |
| [Level 8][level-8] | `bandit8` → `bandit9` | Sorting and unique lines |
| [Level 9][level-9] | `bandit9` → `bandit10` | Readable strings in binary data |
| [Level 10][level-10] | `bandit10` → `bandit11` | Base64 decoding |
| [Level 11][level-11] | `bandit11` → `bandit12` | ROT13 character translation |
| [Level 12][level-12] | `bandit12` → `bandit13` | Hexdumps and compression layers |
| [Level 13][level-13] | `bandit13` → `bandit14` | Network work begins: SSH key authentication |
| [Level 14][level-14] | `bandit14` → `bandit15` | Sending a password over TCP |
| [Level 15][level-15] | `bandit15` → `bandit16` | Sending a password over TLS |
| [Level 16][level-16] | `bandit16` → `bandit17` | Port discovery, TLS, and an SSH key |
| [Level 17][level-17] | `bandit17` → `bandit18` | Comparing changed file lines |
| [Level 18][level-18] | `bandit18` → `bandit19` | Running a command over SSH |
| [Level 19][level-19] | `bandit19` → `bandit20` | A setuid command helper |
| [Level 20][level-20] | `bandit20` → `bandit21` | A TCP listener and setuid client |
| [Level 21][level-21] | `bandit21` → `bandit22` | Following a cron job's output |
| [Level 22][level-22] | `bandit22` → `bandit23` | Calculating a cron script's hashed filename |
| [Level 23][level-23] | `bandit23` → `bandit24` | Submitting a shell script to cron |
| [Level 24][level-24] | `bandit24` → `bandit25` | Streaming four-digit PINs over one TCP connection |

Try the official challenge first, then open the relevant walkthrough when you need it. Further levels will be added after I solve them.

I solved each level using my own understanding and knowledge. These writeups record the commands and approaches that made sense to me; other commands and methods can solve the same challenges. I include one working alternative for each level.

## Network work from Level 13

From [Level 13][level-13], the walkthroughs introduce network authentication and services: SSH keys, plain TCP connections, TLS, port and service discovery, remote commands, and a listener/client exchange.

SSH has carried the login sessions since Level 0. Level 13 starts the focused network work with key authentication; Levels 14–16 introduce the challenge services.

Levels 21–23 follow scheduled cron jobs and their scripts on the Bandit server. [Level 24][level-24] returns to TCP services by sending all four-digit PINs over one connection.

The [SSH, Netcat, OpenSSL, and Nmap guide](guides/ssh-nc-openssl-nmap.md) collects the commands used here, explains their options, and gives practical use cases.

Run the challenge's `localhost` connections and scans inside the relevant Bandit shell, where `localhost` is the Bandit server. Run account logins and key-file preparation in your local terminal.

## Passwords and screenshots

Follow the [OverTheWire rules](https://overthewire.org/rules/). Keep recovered passwords in private notes outside this repository. Get the initial login password from the [official setup page](https://overthewire.org/wargames/bandit/bandit0.html).

Only cropped, permanently redacted screenshots are included. Solid blocks hide passwords, SSH private-key bodies, and TLS session secrets while preserving commands, paths, prompts, and useful results. Multi-step captures appear in the order used; original screenshots stay outside this repository.

See the [writeup rules](.github/rules.md) for the format, command tables, and checks to complete before committing.

## Credit

Bandit is created and hosted by the [OverTheWire community](https://overthewire.org/). Each walkthrough quotes the official Level Goal with a link to its source; passwords are omitted. The explanations and solutions are original notes from my own sessions.

[level-0]: levels/level-0.md

[level-1]: levels/level-1.md

[level-2]: levels/level-2.md

[level-3]: levels/level-3.md

[level-4]: levels/level-4.md

[level-5]: levels/level-5.md

[level-6]: levels/level-6.md

[level-7]: levels/level-7.md

[level-8]: levels/level-8.md

[level-9]: levels/level-9.md

[level-10]: levels/level-10.md

[level-11]: levels/level-11.md

[level-12]: levels/level-12.md

[level-13]: levels/level-13.md

[level-14]: levels/level-14.md

[level-15]: levels/level-15.md

[level-16]: levels/level-16.md

[level-17]: levels/level-17.md

[level-18]: levels/level-18.md

[level-19]: levels/level-19.md

[level-20]: levels/level-20.md

[level-21]: levels/level-21.md

[level-22]: levels/level-22.md

[level-23]: levels/level-23.md

[level-24]: levels/level-24.md
