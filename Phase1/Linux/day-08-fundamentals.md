# Day 08 — Bandit Levels 23–25
**Date:** 15/04/2026
**Source:** OverTheWire — Bandit
**Status:** Completed Levels 23→25 ✅

---

## Why this matters for hacking
- `stat` — checking file ownership, used to identify privilege escalation targets
- `timeout` — limiting execution time, seen in sandboxed environments
- Writing exploit scripts — abusing privileged cron jobs by dropping your own code
- `chmod +x` — making scripts executable for privileged processes
- `chmod 777` — making directories writable by all users including privileged ones
- `printf "%04d"` — zero padded formatting, essential for brute force scripts
- `nc` — raw TCP brute forcing, sending generated payloads to a service

---

## Daily Notes
```
Level 23->24
  Learnt intro to 'stat', 'timeout', read a script, and wrote a script of my own
  First saw the cron file and its script, saw the script and understood its working components
  It was executing files of current user(bandit23) as a higher user(bandit24)
  Made a file using 'nano', typed a script that uses shebang(tells what interpreter 
  to use) '/bin/bash' (bash interpreter) and cat the password of next user into a 
  temp file location using '>' redirect operator
  Created a tmp folder using 'mktemp -d', saved the above file there and made it 
  executable 'chmod +x' [so that it can be executed when copied in cron's process]
  Made the tmp folder writeable by all [so that when our script runs as higher user 
  it can write into temp] '$ chmod 777 tmp/path'
  Copied the script file into the folder from where the scripts are being executed
  Waited 60 sec to let cron complete the process
  Got the password

Level 24->25
  Learnt to write a script and brute force a 4 digit pin on a raw TCP connection
  Wrote a script using nano, used shebang bash interpreter then wrote a for loop
  Used 'echo' with 'printf "%04d"' to generate attempts from 0000 to 9999
  Sent it using pipe and nc to the port and got the password

  Script used:
  #!/bin/bash
  for i in {0..9999}; do
      pin=$(printf "%04d" $i)
      echo <password> ${pin}
  done
  ./script.sh | nc localhost 30002
```
Level 23->24 Learnt intro to 'stat', 'timeout', read a script, and wrote a script of my own
		first saw the cron file and its script ,saw the script and understood its working components 
		it was executing files of current user(bandit23) as a higher user(bandit24) 
		made a file  using 'nano', typed a script that uses shebang(tells what interpreter to use) '/bin/bash' (bash interpreter) and cat the password of next user into a temp file location using '>' redirect operator
		created a tmp folder using 'mktemp -d' saved the above file there and made it executable 'chmod +x' [so that it can be executed when copied in cron's process]
		made the tmp folder to be writeable by all [so that when our script runs as higher user it can write into temp] '$ chmod 777 tmp/path'
		copied the script file into the folder from where the scripts are being executed 
		waited 60 sec to let cron complete the process.
	     	Got the password

Level 24->25 Learnt to write script and bute force a 4 digit pin on a raw tcp connection on a specific port 
		wrote a script using nano ,used shebang bash interpreter then wrote a for loop used 'echo' with 'printf "%04d" '  to give answer with 0000 to 9999
		sent it using 'pipe' and 'nc' to the port and got the password

```