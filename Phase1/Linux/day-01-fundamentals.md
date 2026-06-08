# Day 01 — Linux Fundamentals Part 1
**Date:** 30/03/2026  
**Source:** TryHackMe — Linux Fundamentals Part 1  
**Status:** Completed ✅

---

## Why these commands matter for hacking
- `grep -r` — search entire target filesystem for passwords, keys, secrets
- `find / -name *.txt` — locate sensitive files on a compromised machine
- `&&` operator — chain commands into one-liner payloads
- `>` redirector — overwrite files, useful for dropping payloads

---

## Commands learned
```
Today marks the beginning of the becoming a red teamer from a beginner (30/03/2026)
DAY -->1 (LINUX FUNDAMENTALS)
	|--> I am currently using TRYHACKME.COM's Linux fundamental path
	  |--> 1) I have learnt to use commands like "cd" for changing directory 
	  |   cmd $ cd path/of/file  //----(we can use one single name of the folder in that directory or use multiple with path of sub directory)----//
	  |   cmd $ cd /             //--to go back to root directory--//
	  |   cmd $ cd ..            //--to go back up the file directory hierarchy--//
	  |   cmd $ cd -             //--to go back to the previous directory  that u were using not acc to file hierarchy--//
	  |
	  |
	  |--> 2) "ls" listing is used to list the content of the folder onto the terminal ,
	  |   |--> $ ls -l    //for long list (file permission ,owner , group ,size and modification date
	  |   |--> $ ls -a    //shows hidden files as well
	  |
	  |--> 3) "pwd" print working directory --prints the path of current working directory
	  |      $ pwd 
 	  |
	  |--> 4) "find" used to find a file(s)/folder(s) i.e. there path starting search from root directory
 	  |       $ find -name "file_name.txt"          //-- here -name is a sub cmd of find that specifies to find file using name ,the name of file is in brackets
	  |       $ find -iname "example.txt"           //-- helps find file name case insensitive i.e. example.txt ,Example.txt, EXAMPLE.txt can be find with this
	  |       $ find -name *.txt                    //--(don't use quotes) * is a wildcard here its used to find any file with .txt extension in the directory and sub directories
	  |	  $ find /path/to/find -name "example.txt" //---to find along a specified path
	  |	  $ find . -type f                         //-- "." helps find inside current directory only and "-type" helps find by its type "f" for files and "d" for directories
	  |       $ find ~ -type d                    //-- "~" helps find within scope of current user
	  |       $ find . -name example.txt -delete  //-- finds and deletes the file
	  |
	  |--> 5) "cat" concatenate --used for showing content of file in terminal without opening the file
	  |       $ cat
	  |
      |--> 6) "grep" global search for a regular expression (regex) for searching and matching patterns inside a file without opening the file
  	  |       $ grep "pattern" filename.txt               //--- pattern always in quotes 
      |       $ grep "^pattern" filename.txt              //-- searches lines staring with the pattern
      |	  $ grep "pattern$" filename.txt                  //-- searches lines tha end with the pattern
	  |       $ grep /path/to/find/ "paatt' filename.txt  //--searching in a specified path
	  |       $ grep -i "pattern" filename.txt            //-- searches pattern with case insensitive 
	  |       $ grep -r "pattern" filename.txt            //-- searches pattern in the files of current directory as well as sub directories
      |       $ grep -v "pattern" filename.txt            //-- (invert match) send lines that do not match with pattern 
      |	  $ grep -n "pattern" filename.txt                //-- searches lines that match the pattern and prefixes the number of line 
	  |       $ grep -o "pattern" filename.txt            //-- return only the word/part that matches the searches pattern
	  |       $ grep -w "pattern" filename.txt            //-- searches exact words avoids long words
	  |       $ grep -l "pattern" filename.txt            //-- searches pattern and return only the file name that contains that pattern
	  |
	  |--> 7) "wc" word count --returns (number of lines , number of words ,number of bytes , filename) in a file in this respective order
	  |       $ wc filename 
	  |       $ wc -l filename              //-- "-l"for only number of lines ,"-w" for only number of words ,"-c" only number of bytes ,"-m" for number of charcters--//
 	  |--> 8) "echo" types anything after it ,will be printed exactly in the terminal
	  |       $ echo hello i am funny
	  |
	  |--> 9) OPERATORS (quotes not included)
	  |      |-> "&" use it at the end of any cmd it will run in background (gives u an id and process number)
	  |      |    $ grep -i "hello" welcome.txt &
	  |      |-> "&&" use it to run multiple cmds one after another BUT 2nd cmd runs only if 1st is successful
	  |      |    $ cd home/Desktop && grep -i "hello" welcome.txt 
	  |      |-> ">"  redirector takes the output before it and runs it as input for other and replaces in case of file writting
	  |      |    $ echo hello > welcome.txt        //--(creates a file named welcome.txt and if exist then replaces the content from start of the docx)
	  |      |-> ">>" same as redirector but it appends the data instead of replacing 
	  |      |    $ echo hello again >> elcome.txt
```
