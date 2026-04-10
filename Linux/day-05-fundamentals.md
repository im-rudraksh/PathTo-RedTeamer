# Day 05 — Bandit Levels 16–19
**Date:** 09/04/2026
**Source:** OverTheWire — Bandit
**Status:** Completed Levels 16→19 ✅

---

## Why this matters for hacking
- `nmap -sT -sV` — port scanning and service detection, first step of every real engagement
- `2>&1` — redirecting stderr to stdout, essential for piping and scripting
- `diff -u` — comparing files, used in log analysis and spotting config changes
- `ssh <command>` — executing commands on remote hosts without an interactive shell
- `ssh -t /bin/bash --norc` — bypassing shell config files, useful for restricted shell escapes
- `scp` — pulling files off targets silently over SSH

---

## Daily Notes
```
Level 16->17 learnt about nmap ; logged in using simple password 
	     used "$ man nmap" to read and find the option to scan ports
	     used "nc -zv" to see the connectable ports on the host piped the output to grep but as it is it won't work as "nc" give stderr not stdin/stdout 
	     hence, used 2>&1 ["2"(stderr) ">" (redirect) "&"(file descriptor: defines the types of file by OS "0" means input, 1 and 2) "1"(stdout)]
	 	$ nc -zv host ports 2>&1 | grep "succeeded"
	     used "nmap -sV" (for verbose settings shows services, version, name )
	     (BETTER) use nmap for scanning ports as well as knowing the services using "-sT" and "-sV" together (no need of using "nc")
	     use "--open" to see only the open ports 
	     use either nc or openssl to connect to the resultant port and feed the password, got a key, save it, use it as .pem file as password for the next level

Level 17->18 learnt about "diff" used to compare two files and find what is same or different in those 2 files
		but actually it tells u how to make one file exactly like the other
		output is like "2a3" meaning that after 2nd line of file 1 add line 3rd of second file
		similarly in place of "a" there can be "d" (delete) and "c" (change)
		">" in output means line from file 2 and "<" means line from file 1
		best use "-u" this gives unified answer i.e. with "+" meaning add line, "-" subtracting line
	     logged in using .pem file, used diff file1 file2
	     got the password 

Level 18->19 learnt to bypass .bashrc config files using three different methods:
             cat readme file using ssh commands, ssh "-t" pseudo terminal with bash, and download directly using scp
	     1) ssh commands: SSH can execute commands directly on the remote host by sending them
	        as part of the connection request (inside quotes), without starting an interactive shell.
		$ ssh username@host -p portnumber "cat readme"
	     2) ssh "-t" opens pseudo terminal and ssh executes "/bin/bash" shell from the server
	        "--norc" without using the configuration files of .bashrc
		$ ssh username@host -p portnumber -t /bin/bash --norc
	     3) scp (secure copy) can copy/download files without opening an interactive terminal
	        and save the file in your desired location.
		scp transfers files between systems over SSH without opening an interactive shell,
		allowing you to upload or download files to a specified location.
		$ scp -P port username@host:path/of/file destination/path
```