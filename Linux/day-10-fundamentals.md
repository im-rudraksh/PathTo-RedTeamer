# Day XX — Bandit Wargame Levels 27–33

| Field   | Details                            |
|---------|------------------------------------|
| Date    | 20 / 04 / 2026                     |
| Source  | bandit.labs.overthewire.org        |
| Status  | Completed ✅                       |


---

## 🧠 Why These Commands Matter for Hacking

| Command / Concept | Why It Matters |
|-------------------|----------------|
| `git clone` | Pull down source code repositories from targets — common in real engagements |
| `git log` | Commit history often leaks credentials, API keys, secrets left in old commits |
| `git show` | Inspect exactly what changed in a commit — where leaked data hides |
| `git tag` | Tags can reference old states of code that still contain sensitive data |
| `git branch` | Sensitive data is often hidden in non-default branches devs forget about |
| `git checkout` | Switch between branches/commits to explore a repo's full history |
| `add → commit → push` | Understanding the full Git workflow helps you abuse misconfigured repos |
| `$0` positional parameter | Shell escape technique — works in restricted shells to spawn a real shell |

---

## 📓 Daily Notes

> From Level 27 onward, the focus shifts to **Git** — learning how to find and exploit data left behind in repositories. A massive portion of real-world credential leaks happen through careless Git usage.

---
### Personal notes 
```
Level 27->28: From here on you will learn how to use git features and cmds to find and exploit vulnerabilities using linux(get passwords)
	  	First see if you have git installed (else install it)
		if u like to read first execute later search git basics on google [https://git-scm.com/book/en/v2] and start from initial but if you want to learn while executing 
		learn cmds like 'git clone' and read the "2.5 Working with remotes" a little to use the git clone to download the git repo from the given server
		use 'git clone' with given [port] number as well don't forget
		find the password inside the downloaded repo 

Level 28->29: again download the git file (to rename the repo as u wish before downloading just add the './anyRepoName' after the git 'clone .../repo' cmd)
		Now read about cmd 'git log' and 'git show' to find the password in the repo 
		$ git log ( shows commit history with their hash-codes )
		$ git show (show the diff of the commit against the current document)

Level 29->30: Read about 'git tag' 
		[use all cmds u have learnt of git in every level]
Level 30->31:  READ about branches in git and their basic commands like ' git branch ', 'git checkout'and 'git show'		
		download the repo and try all the commands learnt until now you will find where the password is located 	

Level 31->32: Read about how to push into a git repo [add.commit.push] and 'git config user.email'and 'git config user.name' (with '--local' and '--global' options)
		download the repo and read the readme.md file 
		'touch' and 'nano' cmds of Linux can also be used 
Level 32->33: Learn about Positional Parameters in Shell Script and how they are used in ecxcaping restricted envs 
		log in to bandit labs using password and use what you have learnt.
		try $0 and search what it did and how.
		  $0: Represents the name of the script or the shell itself. While not technically a positional argument (it is the command being executed), it is often categorized with them.
		you escaped successfully now find the find containing the password inside the shell use 'cd','ls',or 'find'
		try finding what kind of shell you have landed in first  use 'echo $0'

		
```
## AI Explanation

### Level 27 → Level 28

**Topic:** `git clone` with a custom port

**Concepts to read:**
- 🔍 Git Basics: [https://git-scm.com/book/en/v2](https://git-scm.com/book/en/v2) *(start from Chapter 1 if new to Git)*
- 🔍 *"2.5 Git Basics — Working with Remotes"* — focus on `git clone`

**Steps:**

1. Check if Git is installed:

```bash
$ git --version          # check if installed
$ sudo apt install git   # install if missing
```

2. Clone the repo from the Bandit server — include the port using the SSH URL format:

```bash
$ git clone ssh://bandit27-git@bandit.labs.overthewire.org:2220/home/bandit27-git/repo
```

3. Navigate into the downloaded repo and find the password:

```bash
$ cd repo
$ ls
$ cat README        # or whatever file is present
```

> **Key concept:** `git clone` pulls the entire repository — all files, history, and branches — to your local machine. On a real target, this means you get everything, including things the developer thought were deleted.

---

### Level 28 → Level 29

**Topic:** `git log` and `git show` — reading commit history

**New trick:** Rename the repo folder while cloning by appending `./yourName` at the end:

```bash
$ git clone ssh://bandit28-git@bandit.labs.overthewire.org:2220/home/bandit28-git/repo ./myrepo
$ cd myrepo
```

**Concepts to read:**
- 🔍 `git log` — shows the full commit history with hash codes and messages
- 🔍 `git show` — shows the diff (what changed) for a specific commit

**Commands:**

```bash
$ git log                        # list all commits with hashes + messages
$ git log --oneline              # compact view — one line per commit
$ git show <commit-hash>         # see exactly what changed in that commit
$ git show HEAD~1                # show the commit before the latest one
```

**How to find the password:**

Look through `git log` for suspicious commit messages like *"removed password"*, *"fix credentials"*, *"oops"*. Then use `git show <hash>` to see what was in the file **before** it was removed.

```bash
$ git log --oneline
  a1b2c3d  fix info leak         <-- suspicious!
  e4f5g6h  add missing data

$ git show a1b2c3d               # see what was changed/removed here
```

> **Why this matters:** Developers often commit passwords by mistake and then make a follow-up commit to remove them — but Git **never forgets**. This is one of the most common real-world credential leak vectors.

---

### Level 29 → Level 30

**Topic:** `git tag` — finding data in tagged versions

**Concepts to read:**
- 🔍 *"Git tagging"* — tags mark specific points in repo history (usually releases)

**Commands:**

```bash
$ git clone ssh://bandit29-git@bandit.labs.overthewire.org:2220/home/bandit29-git/repo ./repo29
$ cd repo29

$ git log --oneline              # check commit history
$ git tag                        # list all tags in the repo
$ git show <tagname>             # inspect a tag — may point to an old commit with secrets
```

> **Why this matters:** A tag like `v1.0-beta` or `release-old` might point to a version of the repo where credentials were still present before they were cleaned up in later commits.

**Tip — combine everything you've learned:**

```bash
$ git log --all --oneline        # show commits across ALL branches and tags
$ git show <hash>
$ git tag
$ git show <tagname>
```

---

### Level 30 → Level 31

**Topic:** Git branches — secrets hidden in non-default branches

**Concepts to read:**
- 🔍 *"Git branches"* — a branch is an independent line of development
- 🔍 `git branch`, `git checkout`, `git show`

**Commands:**

```bash
$ git clone ssh://bandit30-git@bandit.labs.overthewire.org:2220/home/bandit30-git/repo ./repo30
$ cd repo30

$ git branch -a                  # list ALL branches (local + remote)
$ git checkout <branch-name>     # switch to a different branch
$ ls && cat README               # explore the branch contents

$ git log --all --oneline        # see history across all branches
$ git show <hash>                # inspect any interesting commit
$ git tag                        # don't forget tags too
```

> **Why this matters:** Developers often create feature or dev branches and forget about them. These branches can contain test credentials, debug configs, or old versions of files with sensitive data — and they're rarely cleaned up.

**Typical workflow for this level:**

```
git branch -a   →   spot a non-main branch   →   git checkout <branch>   →   find password
```

---

### Level 31 → Level 32

**Topic:** Pushing to a Git repo — `add → commit → push`

**Concepts to read:**
- 🔍 *"How to push to a git repository"*
- 🔍 `git config user.email` and `git config user.name` with `--local` and `--global`

**Steps:**

```bash
$ git clone ssh://bandit31-git@bandit.labs.overthewire.org:2220/home/bandit31-git/repo ./repo31
$ cd repo31
$ cat README.md                  # read the instructions — they tell you what to push
```

The README will ask you to create a specific file with specific content and push it. Follow these steps:

```bash
# Set your Git identity (required before committing)
$ git config --local user.email "you@example.com"
$ git config --local user.name "yourname"

# Create the required file
$ touch key.txt                  # or use nano to create with content
$ nano key.txt                   # write the required content, save with Ctrl+O, exit Ctrl+X

# Stage, commit, and push
$ git add key.txt                # stage the file
$ git add -f key.txt             # use -f if the file is in .gitignore
$ git commit -m "add key file"   # commit with a message
$ git push origin master         # push to the remote repo
```

The server will respond with the password for bandit32 after a successful push.

> **`--local` vs `--global`:**
> - `--local` → sets config only for the current repo (stored in `.git/config`)
> - `--global` → sets config for all repos on your user account (stored in `~/.gitconfig`)

> **Why this matters:** Misconfigured Git repos on real targets sometimes allow **unauthenticated pushes**. Knowing how to push means you can potentially inject malicious files into a target's codebase or CI/CD pipeline.

---

### Level 32 → Level 33

**Topic:** Positional parameters in shell scripting — escaping a restricted environment

**Concepts to read:**
- 🔍 *"Positional parameters in shell scripting"*
- 🔍 *"Shell special variables: `$0`, `$1`, `$2`..."*

**What are Positional Parameters?**

| Variable | Meaning |
|----------|---------|
| `$0` | The name of the script or the **shell itself** |
| `$1` | First argument passed to the script |
| `$2` | Second argument, and so on |
| `$@` | All arguments |
| `$#` | Number of arguments |

**The Escape:**

When you log in to bandit32, you are dropped into an **UPPERCASE SHELL** — a restricted shell that converts everything you type to uppercase before executing it, breaking all normal commands.

```bash
# Everything gets uppercased:
$ ls   →   LS   →   command not found
$ cat  →   CAT  →   command not found
```

**The trick — use `$0`:**

```bash
$ $0
```

`$0` represents the name of the current shell. Since `$0` is not a word but a **special variable**, the uppercase shell doesn't break it. It expands to `/bin/sh` (or similar), spawning a real shell.

```bash
# You now have a proper shell — proceed normally:
$ whoami
$ cat /etc/bandit_pass/bandit33
```

> **Why this works:** `$0` is evaluated by the shell *before* the uppercase transformation is applied. It's not a command name — it's a variable expansion. The restricted shell has no protection against this.

> **Why this matters:** Positional parameters and special shell variables are a go-to technique for escaping restricted shells (`rbash`, custom scripts, etc.) in CTFs and real privilege escalation scenarios.

---

## 🔑 Passwords Log

> *(Keep this file private!)*

| Level    | Password |
|----------|----------|
| bandit28 | `_______` |
| bandit29 | `_______` |
| bandit30 | `_______` |
| bandit31 | `_______` |
| bandit32 | `_______` |
| bandit33 | `_______` |

---

## 📌 Full Commands Reference

```bash
# Git setup
git --version
sudo apt install git
git config --local user.name "name"
git config --local user.email "email"

# Cloning
git clone ssh://user-git@host:port/path/repo          # clone a repo
git clone ssh://user-git@host:port/path/repo ./name   # clone with custom folder name

# Exploring history
git log                     # full commit history
git log --oneline           # compact history
git log --all --oneline     # history across ALL branches and tags
git show <hash>             # diff for a specific commit
git show HEAD~1             # diff of previous commit

# Tags
git tag                     # list all tags
git show <tagname>          # inspect a tag

# Branches
git branch -a               # list all branches (local + remote)
git checkout <branch>       # switch to a branch

# Pushing
git add <file>              # stage a file
git add -f <file>           # force-stage (bypasses .gitignore)
git commit -m "message"     # commit staged changes
git push origin master      # push to remote

# Shell escape
$0                          # spawn the current shell — escapes restricted environments
```

---

## 🔗 Further Reading

- [Git Book (official)](https://git-scm.com/book/en/v2) — Chapters 1 & 2 are essential
- [GTFOBins — git](https://gtfobins.github.io/gtfobins/git/) — git shell escapes
- [TruffleHog](https://github.com/trufflesecurity/trufflehog) — real tool that scans git history for leaked secrets
- [GitLeaks](https://github.com/gitleaks/gitleaks) — another industry-standard secret scanner for git repos

---
# At this moment, level 34 does not exist yet.
*Part of an ongoing Red Teaming learning journey — Beginner → Professional.*