# Day 04 — Bandit Levels 13–15
**Date:** 07/04/2026
**Source:** OverTheWire — Bandit
**Status:** Completed Levels 13→15 ✅

---

## Why this matters for hacking
- `ssh -i` — private key auth is standard in real server access, not just passwords
- `scp` — securely copy files off a target machine during an engagement
- `nc` — netcat is every hacker's go-to for raw TCP connections
- `openssl s_client` — manually testing SSL/TLS services on a target
- `chmod 600` — locking down key files so SSH actually accepts them

---

## Daily Notes
```
//-------------READ FILE commands-deep-dive-------------//

Level 13->14 learned more about ssh keys; used "find" to find the folder by "-name" and "cd"(ed) to it 
		found a  secret key and used scp to download the file(you can cat  and paste it in a file then "chmod 600 file" to upgrade its security as well)
		used "$ scp -p 2220 -i "password of level 13" username@targethost:filename ./destination/path/" (read about ssh keys if u don't understand this)
Level 14->15 learned about netcat(nc) ; used ssh secretkey created in last level to log in the level
	      $ ssh -i secretkey.private usernaem@hostname/ip -p port (-i uses the secretkey.private to log in instead of a password)
	     use find to find the secretkey file like before or go to the same directory for password as in level13-14 ,now u can see the password file as well copy that.
	     used "nc" to connect a raw TCP connection on localhost (i.e. inside the bandit server)
	      "$ nc localhost 30000"
	     once connected use password u just got and u will get a new password for next level
Level 15->16 learnt about openssl ; logged in using simple password 
	     used "$ man openssl" to read and find the option to connect to local host
		$ echo "password of level 15" | openssl s_client -connect hostip:port -quiet" 
		(s_client: This  implements  a  generic SSL/TLS client) (-connect h:p to tell host and port to connect to) 
		(-quiet: to remove (right now) unnecessary certificate and handshake info coming from server )
	     TIP: use without -quiet to understand things better
```
