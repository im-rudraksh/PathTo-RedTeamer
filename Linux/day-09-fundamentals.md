# Day XX — Bandit Wargame Levels 25–27

| Field   | Details                            |
|---------|------------------------------------|
| Date    | __ / __ / ____                     |
| Source  | bandit.labs.overthewire.org        |
| Status  | Completed ✅                        |

---

## 🧠 Why These Commands Matter for Hacking

| Command / Concept | Why It Matters |
|-------------------|----------------|
| `scp` | Securely copy files to/from remote machines — used in every real engagement |
| `chmod 700` | Setting correct key permissions is mandatory for SSH auth to work |
| `ssh -i <keyfile>` | Using identity files instead of passwords — very common in real targets |
| Restricted shells (`rbash`, etc.) | Targets often drop you into restricted environments to limit attacker movement |
| `more` (pager) | Understanding how pagers work helps escape constrained environments |
| Vim shell escape | A classic privilege escalation / shell escape technique |

---

## 📓 Daily Notes

### Personal notes 
```
Level 25->26: use 'scp' or 'cat' and just copy paste the given ssh.key into a file and 'chmod 700' and use that to log in ur next level as before

Level 26->27: this is tricky! search "what are restricted environment in Linux?" then ,vim , vim shell change cmds and read about pager ('more')
in this the terminal runs a 'more' cmd and shows u the output "bandit" and logs you out instantly .
To force more into interactive mode u have to resize the terminal into a very small scale less than 100x100 and then open  vim editor by pressing button 'v' then use vim cmd to change shell to bash and get the next level pass

```

---
## AI Generated 

### Level 25 → Level 26

- **Goal:** Log into bandit26 using a provided SSH private key.
- The SSH key for bandit26 is available in the home directory of bandit25.

**Steps:**

1. While logged into bandit25, read or copy the SSH private key for bandit26.
2. Transfer it to your local machine using `scp`, **or** simply copy-paste the key content into a new local file.
3. Set strict permissions on the key file — SSH refuses to use keys that are too permissive.
4. Use the key to log into bandit26.

```bash
# On your local machine — save the key
$ nano bandit26.key          # paste the key content here, save and exit
# OR use scp to copy directly:
$ scp -P 2220 bandit25@bandit.labs.overthewire.org:~/bandit26.sshkey ./bandit26.key

# Set correct permissions (owner read/write/execute only)
$ chmod 700 bandit26.key

# Log in using the key
$ ssh -i bandit26.key -p 2220 bandit26@bandit.labs.overthewire.org
```

> **Note:** `chmod 700` sets the file to be accessible only by the owner.
> SSH will outright reject keys with looser permissions (e.g., 644 or 777).

---

### Level 26 → Level 27 ⚠️ Tricky!

**Concepts to research before attempting:**
- 🔍 *"What are restricted environments in Linux?"*
- 🔍 *"Vim shell escape techniques"*
- 🔍 *"How does the `more` pager work?"*

---

#### What's Happening Here

When you log into bandit26, instead of giving you a normal shell, the server runs a **restricted login shell**. It immediately runs the `more` command displaying the word `"bandit"` and then **logs you out instantly** — you never get a prompt.

This is because bandit26's shell (check `/etc/passwd`) is set to a custom script that invokes `more` and exits.

---

#### The Escape — Step by Step

**Step 1 — Shrink your terminal window**

`more` only enters **interactive/pager mode** when the content is too large to fit on screen.
If your terminal is full-size, `more` prints everything and exits in one shot.

> 🔑 Resize your terminal to be **very small** — fewer than ~5–6 rows tall (well under 100×100).

**Step 2 — Log in again**

```bash
$ ssh -i bandit26.key -p 2220 bandit26@bandit.labs.overthewire.org
```

Now `more` is forced into interactive mode and **pauses**, waiting for your input.
You'll see the `--More--` prompt at the bottom.

**Step 3 — Open Vim from inside `more`**

While `more` is paused, press:

```
v
```

This drops you into **Vim**, editing the file that `more` was displaying.

**Step 4 — Change the shell to bash inside Vim**

In Vim, use the `:set shell` command to override the restricted shell:

```vim
:set shell=/bin/bash
```

Then launch the shell:

```vim
:shell
```

You now have a **full bash shell** as bandit26! 🎉

**Step 5 — Get the password**

```bash
$ cat /etc/bandit_pass/bandit26     # read bandit26's password
$ ls                                # check home directory for bandit27 key/binary
```

There is typically a `bandit27-do` binary or similar — use it to read the next password:

```bash
$ ./bandit27-do cat /etc/bandit_pass/bandit27
```

```bash
$ exit    # when done
```

---

#### Why This Works — The Concept

| Concept | Explanation |
|---------|-------------|
| **Restricted shell** | A shell (like `rbash`) or custom script that limits what commands a user can run after login |
| **`more` pager** | A terminal program for reading long output one page at a time; enters interactive mode only when content exceeds screen height |
| **Vim shell escape** | Vim can spawn a shell with `:shell` or `:!cmd` — a well-known technique to break out of restricted environments |
| **`set shell=`** | Vim uses `$SHELL` to decide which shell to launch; overriding it bypasses the restriction |

> This technique is listed in **GTFOBins** (gtfobins.github.io) under `vim` — a go-to resource for shell escapes during real engagements and CTFs.

---

## 🔑 Passwords Log

> *(Keep this file private!)*

| Level    | Password |
|----------|----------|
| bandit26 | `_______` |
| bandit27 | `_______` |

---

## 📌 Commands Summary

```bash
scp -P 2220 user@host:~/remotefile ./localfile   # copy file from remote
chmod 700 keyfile                                 # set strict key permissions
ssh -i keyfile -p 2220 user@host                 # SSH login using identity file

# Inside more (pager):
v                                                 # open current file in Vim

# Inside Vim:
:set shell=/bin/bash                             # override restricted shell
:shell                                           # spawn a bash shell
:q                                               # quit Vim
```

---

## 🔗 Further Reading

- [GTFOBins — vim](https://gtfobins.github.io/gtfobins/vim/) — shell escapes via Vim
- [GTFOBins — more](https://gtfobins.github.io/gtfobins/more/) — shell escapes via more
- Linux restricted shells: `rbash`, custom `/etc/passwd` shell entries

---