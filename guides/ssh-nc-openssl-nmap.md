# SSH, Netcat, OpenSSL, and Nmap in Bandit

These tools support the focused network work starting at Level 13. SSH also carries the account logins from Level 0. Each example names the account or service from its challenge.

| Tool | Use case here | Levels |
| --- | --- | --- |
| `ssh` | Log in with a key or run a single remote command. | 13, 16, 18; account logins throughout |
| `nc` | Send lines to a TCP service, check a connection, or run a listener. | 14, 16 backup, 20, 24 |
| `openssl` | Decode Base64 or inspect and communicate with a TLS service. | 10 backup, 15, 16 |
| `nmap` | Discover open ports and identify their services. | 16 |

## SSH: login and remote execution

Use SSH from your local terminal to reach a remote account securely.

```bash
ssh -p 2220 bandit14@bandit.labs.overthewire.org
ssh -i bandit13.key -p 2220 bandit14@bandit.labs.overthewire.org
ssh -p 2220 bandit18@bandit.labs.overthewire.org "cat readme"
```

| Part | Meaning |
| --- | --- |
| `user@host` | Select the remote account and server. |
| `-p 2220` | Use Bandit's SSH port instead of the usual port 22. |
| `-i keyfile` | Use a private key to authenticate. |
| `"cat readme"` | Run this remote command and return when it finishes. |
| `-T` | Disable pseudo-terminal allocation for a remote command. |

Before a key login, run `chmod 600 keyfile` locally so only your user can read or write that key. Verify the intended host before accepting a new SSH host key.

Practical uses include key-based server access and running a single remote task. In Level 18, requesting the command directly avoids the interactive shell's automatic logout.

## Netcat: TCP clients and listeners

Run the challenge service commands inside the relevant Bandit shell. Here, `localhost` means the Bandit server.

```bash
nc localhost 30000
nc localhost 30000 < /etc/bandit_pass/bandit14
nc -l -p 4444
nc -zv -w 1 localhost 31000-32000 2>&1 | grep -E 'open|succeeded'
```

| Part | Meaning |
| --- | --- |
| `host port` | Connect to a TCP service as a client. |
| `< file` | Supply the file's contents as the client's input. |
| `-l` | Listen for an incoming connection. |
| `-p 4444` | Select the listener's local port in the version used here. |
| `-z` / `-v` | Check connections without application data / report results. |
| `-w 1` | Limit connection and I/O waits. |
| `2>&1` | Include diagnostic output in the pipeline. |
| `&` after a command | Run it in the shell's background. |

The screenshots use `nc -l -p 4444`. Netcat variants have different flags; OpenBSD Netcat also supports `nc -l 4444`. Check `nc -h` on the machine where you run it.

Practical uses include testing a line-based TCP service and observing a client's exchange with a listener. Level 20 needs both programs on the same Bandit server: the listener sends the current password and prints the client's returned password. Choose the same port for both.

In the remote `bandit24` shell, stream all four-digit PINs through one connection:

```bash
for i in {0000..9999}; do echo "[current bandit24 password] $i"; done | nc localhost 30002 | grep -v "Wrong!"
```

Replace the placeholder privately with the current password. Bash preserves the four-digit padding. Placing `nc` after the completed loop sends every newline-terminated password/PIN pair through the same client; `grep -v` hides unsuccessful replies. The [Level 24 walkthrough](../levels/level-24.md) includes the recorded result and a backup using `seq` and `printf`.

## OpenSSL: Base64 and TLS

Base64 decoding, used as a Level 10 backup:

```bash
openssl base64 -d -in data.txt
```

`-d` decodes and `-in` names the input. Base64 encoding is useful for representing binary data as text; it does not encrypt it.

TLS connections, run inside the relevant Bandit shell:

```bash
openssl s_client -connect localhost:30001
openssl s_client -connect localhost:30001 -quiet < /etc/bandit_pass/bandit15
openssl s_client -connect localhost:31790 -quiet
```

| Part | Meaning |
| --- | --- |
| `s_client` | Start a TLS client and inspect the handshake. |
| `-connect host:port` | Choose the TCP destination for the TLS connection. |
| `-quiet` | Suppress session output and disable interactive command-letter handling. |
| `< file` | Send a newline-terminated password from its file. |

Use the verbose connection to inspect certificates and the negotiated TLS version. Use `-quiet` for a clean data exchange; certificate diagnostics can remain. This also avoids the connected-command interpretation behind messages such as `KEYUPDATE` noted by the official challenges.

The lab's self-signed certificate warning does not establish a trusted identity. A successful handshake establishes the encrypted channel; the application's `Correct!` reply confirms the password submission.

Practical uses include troubleshooting TLS services, checking certificate details, and sending data over an encrypted connection. Port 31790 was the matching Level 16 service in this session; discover the current ports before using it.

## Nmap: ports and services

In the remote `bandit16` shell:

```bash
nmap -sV -p 31000-32000 localhost
```

| Part | Meaning |
| --- | --- |
| `-p 31000-32000` | Limit the scan to the challenge's port range. |
| `-sV` | Probe open ports for service identification. |
| `-sT` | Use TCP connection checks when specifying a connect scan. |
| `--open` | Show open or possibly open ports. |

An alternative first pass is `nmap -sT --open -p 31000-32000 localhost`; follow up with service detection or a TLS client on the open ports.

`echo` returns the data it receives. `ssl/echo` does that over TLS. `ssl/unknown` identifies TLS wrapping without naming the application. Connect to the candidates and inspect their replies to find the one returning the next credential.

Practical use: build a list of listening services before troubleshooting them with the right client.

## References

- [SSH manual](https://man.openbsd.org/ssh)
- [Traditional Netcat manual](https://manpages.debian.org/trixie/netcat-traditional/nc.1.en.html)
- [OpenSSL s_client manual](https://docs.openssl.org/3.6/man1/openssl-s_client/)
- [Nmap service detection](https://nmap.org/book/man-version-detection.html)
- [Back to the walkthrough index](../README.md)
