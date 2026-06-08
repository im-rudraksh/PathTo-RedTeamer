# Day 03 — Bandit Wargame Levels 4–13
**Date:** 04/04/2026
**Source:** OverTheWire — Bandit
**Status:** Completed Levels 4→13 ✅

---

## Why this matters for hacking
- `file` — identify file types on a target without relying on extensions
- `2>/dev/null` — suppress errors for clean output, used constantly in scripts
- `strings` — extract readable data from binaries and malware samples
- `xxd -r` — reverse hexdumps, core skill in CTF forensics
- `tr` — transform text, useful for simple ciphers and encoding tricks
- `sort` + `uniq -u` — find unique lines, used in log analysis and recon

---

## Daily Notes
```
level 4->5 :used the "file" cmd for the first time used "file -" to find the ASCII text file out of many directly "cat" the file

level 5->6 used "find" using -size from "."(current directory) 
        used 2>/dev/null (used to get clean answer) at the end of the cmd to redirect stderr(standard error) and discard them
		here 2> mean redirect stderr and /dev/null/ means discard those stderr 

level 6->7 used "find" in "/" root directory using option "-user" "-group" "-size" altogether 

level 7->8 used grep to find the line 

level 8->9"sort" sorted the data to use (piped "|") "uniq" with "-u"(shows only the strings that appear once to find the line)

level 9->10 used "strings" to print human readable content and piped "|" it with "grep' 

level 10->11 used "base64 -d" to decode base 64 lines

level 11->12 used to learn "tr" to change the start of the alphabet from "a-z" to "n-za-m" for both upper adn lower case
        (also learned changing upper to lower case for self use)

level 12->13 used many new cmds "mktemp -d" to make a temp directory in servers temp folder, "cp" to copy file from user directory to the created temp directory
		learnt what is hexdump(hexadecimal data representation of a file its location as well as content and content type) 
		"cat" saw the file content matched it with type of compression using manual hex inspection because content  hexdump was inside the file
		hex code for diffrent compressions (gzip: 1f 8b 08 ; bzip2 :42 5a 68(B2H) ; xz : fd 37 7a 58 5a 00 ; zip : 5a 4b 03 04(PK..))
		(important) used "cat" to pipe the file content into "xxd -r"(reverse the hexdump to binary) and saved the result in a new file using ">"
		used "file" on the new output file found compression of gzip type 
		used "mv" to rename the file with .gz(gzip) extension (repeated the last 2 steps for bzip2(.bz2) using "bunzip2")and used "tar -xf filename" (-x  for extraction ,-f for using file name )
		after repeatedly finding compression type(using "file"), renaming and decompressing file got the answer in the last fecompressed file.
        
```