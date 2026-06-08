# Day 06 — Bandit Level 19–20 & File Permissions Deep Dive
**Date:** 10/04/2026
**Source:** OverTheWire — Bandit
**Status:** Completed Levels 19→20 ✅

---

## Why this matters for hacking
- `permission bits` — reading permissions instantly tells you what you can access on a target
- `setuid bit` — core privilege escalation primitive, exploited constantly in CTFs and real engagements
- `setuid binary` — running it gives you the file owner's privileges, not yours

---

## Daily Notes
```
Learnt how to read file permission bits
10 fixed bits are used as permission bits always

FOR EXAMPLE: -rwsr-x---   1   user1   group   14888   Apr 3 15:17  file-name.txt

    - r w s r - x - - -
    ^ ^ ^ ^ ^ ^ ^ ^ ^ ^
pos:0 1 2 3 4 5 6 7 8 9

pos 0     : file type [ '-' = file | 'd' = directory | 'l' = symlink ]
pos 1,2,3 : owner permissions  [ r=read | w=write | x=execute | s=setuid ]
pos 4,5,6 : group permissions  [ r=read | w=write | x=execute | s=setgid ]
pos 7,8,9 : other permissions  [ r=read | w=write | x=execute ]

NOTE: setuid means the file runs as its OWNER regardless of who executes it
      This is a privilege escalation primitive — if a root-owned file has setuid,
      running it gives you root-level access temporarily

The '-' confusion (important):
  First '-' (pos 0) = file type, regular file
  Later '-' (in permissions) = that permission is simply not granted


Level 19->20 : executed the setuid binary, used it to cat files
              locked to root-only access
```