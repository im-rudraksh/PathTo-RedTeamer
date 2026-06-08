# Day 02 — Bandit Wargame Levels 0–4
**Date:** 31/03/2026  
**Source:** bandit.labs.overthewire.org  
**Status:** Completed ✅

---
## Why these commands matter for hacking
- `ssh` — how you access every remote machine in a real engagement
- `cat ./-` — handling special filenames comes up constantly in CTFs
- `ls -a` — hidden files on a target often contain passwords or keys
- `-- ` after a command — bypasses flag interpretation, useful to know
---

## Daily Notes 
```
Today I used wargames to learn Linux used to and completed till level3-level4
	|-->Level0 && Level0-Level1
	|--> first i searched a little about ssh connections to connect to Host: bandit.labs.overthewire.org Port 2220(login username and password were available on website for level0)
	|  "ssh" to describe connection type "-p" to tell port number(2220) then used syntax :username@host_ip/address for establishing connection
	|  Used cd, ls and cat commands to  find the file and the password for the next levels
	|    |->$ ssh -p 2220 bandit0@bandit.labs.overthewire.org   //-- to connect 
	|    |->$ exit                                             //-- to disconnect to the level0 
	|    |->$ ssh -p 2220 bandit1@bandit.labs.overthewire.org   //-- to connect
	|    |->$ exit                                             //-- to disconnect to the connection (levels here)
	|
	|--> Level1-Level2
	|  Used cmds ls, cd ,cat and find
	|    |->$ ssh -p 2220 bandit2@bandit.labs.overthewire.org   //-- to connect 
	|    |-> Learnt that to read or find files with names starting with "-" (quotes not included) u need to specify the whole path or "." which represents  current directory 
	|    |  also u can use "--" after a cmd like cat (represents that all parameters like -p or -a will not be used after this
	|    |  hench found the password to next level
	|    |->$ exit                                             //-- to exit
	|
	|--> Level2-Level3
	|  Used cmds ls, cat
	|    |->$ ssh -p 2220 bandit3@bandit.labs.overthewire.org   //-- to connect 
	|    |-> Learnt how to handle files with spaces in there name as well as "-"
	|    |-> used quotes and ./ together
	|    |->got the password
	|    |->$ exit
	|    
	|-->Level3-Level4
	|  Used cmds ls,cat
	|    |->$ ssh -p 2220 bandit4@bandit.labs.overthewire.org   //-- to connect 
	|    |  Learnt to see hidden files using ls cmds options (-a, --all)
	|    |  got the password
	|    |->$ exit						  //to disconnect

```
