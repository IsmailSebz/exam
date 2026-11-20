Linux Fundamentals BSE 4105 – 2026/1 

**Dr. Alex Mwotil** 

1 

##### Unix & Linux 

### **Unix** 

**1969** 

_Bell Labs — Dennis Ritchie & Ken Thompson_ 

- “Everything is a file” 

- Multi-user, hierarchical file system 

- Small tools “glued” together 

- Documentation included 

### **Linux** 

**1992** 

_Created by Linus Torvalds — who also built Git!_ 

   - Open-source, Unix-like system 

   - Inspired by Unix's philosophy 

   - Free to use, study & modify 

   - Powers most of the cloud & DevOps world 

- macOS is Unix in disguise! 

2 

##### The Shell 

An interactive program that lets you talk directly to the operating system and its applications. 



<!-- Start of picture text -->
$  pwd<br>/home/student<br>Why use the shell over a GUI?<br>Faster for Works on<br>Programmable Customizable<br>complex tasks remote servers<br><!-- End of picture text -->

3 

**`pwd`** Print current working directory **`cd`** Change working directory Basic Shell **`ls`** List files in working directory Commands **`man`** Bring up the manual for a command **`exit`** Log out of the shell **`clear`** Clear all output from the console **`date`** Output the system date **`cal`** Output a text calendar **`uname`** Print information about the system 

4 

##### Directory Shorthand 

```
.
```

Current working directory 

```
..
```

Parent of the current directory 

```
~username
```

username's home directory 

**`~/Desktop`** Your Desktop directory 

5 

##### The Linux File System 

### **`/`** 







**`/bin /dev /etc`** Applications & Hardware Configuration binaries devices files 









**`/tmp, /home /proc /usr /var`** Universal Users' home Running Temporary files system directories processes resources 

6 

##### Directory Commands 

```
ls
```

List files 

**`pwd`** Print directory 

**`cd`** Change directory 

**`mkdir`** Make a directory 

**`rmdir`** Remove empty dir 

7 

##### Anatomy of a Command 

**`$ ls -al Dir` Command Flag Argument** _There's no single agreed convention for CLI arguments — but this is the pattern we'll use in class._ 

8 

Flags & Arguments in Practice 

List in long-list format: 

```
$ ls -l
```

Combine flags — long-list + hidden files: 

```
$ ls -la
```

Pass an argument — long-list files inside dir1: 

```
$ ls -l dir1
```

9 

## Working with Files & Editors 

Copying, moving, editing, and reading what's on disk 

10 

##### File Commands 

```
cp
```



<!-- Start of picture text -->
Copy a file<br><!-- End of picture text -->

**`mv rm`** Move / rename a Remove a file file ⚠ **No confirmation prompt — be careful! Use man pages if you're unsure.** 

#### **`touch`** 

Create empty file, or update its timestamp 

11 

##### Text Editors 

###### Everything is a file — to interact with the CLI, you'll need a text editor. 

```
nano
```

```
vim
```

## **`emacs`** 

Very simple editor 

Advanced, Advanced, powerful, powerful, modal editing highly extensible 

_Power / Learning curve_ 

_Power / Learning curve_ 

_Power / Learning curve_ 

12 

##### Vim Basics 

**`:w`** Write (save) the file **`:q!`** Quit, discard changes **`Esc`** Back to normal mode **`u`** Undo last change 

```
:wq
i
```

```
hjkl
```

```
x
```

Write & quit Enter insert mode 

Move ← ↓ ↑ → Delete character 

13 

##### Emacs Basics 

_C = Control key   ·   M = Alt/Meta key_ 

**`C-x C-f`** Read a file into emacs **`C-x C-c`** Exit emacs **`C-r`** Search backwards **`M-v`** Scroll to previous screen 

**`C-x C-s`** Save file to disk **`C-s`** Search forward **`C-v`** Scroll to next screen **`C-x u`** Undo 

14 

##### Examining Files 

```
cat
```

Print full contents 

```
head
```

Show start of file 

```
less
```

Page through output 

```
tail
```

Show end of file 

```
more
```

Page through output 

```
wc
```

Count words / lines / chars 

15 

##### Search & Sort 

**`grep`** Search for a pattern 

```
sort
```

Sort lines of input 

**`uniq`** Strip duplicate adjacent lines 

```
find
```

Search the filesystem 

```
cut
```

Remove a section from each line 

16 

Streams, Redirection & Pipes How data flows in and out of every Unix process 

17 

##### Standard Streams 

Every process reads from and writes to three abstract locations — by default, all three point at your terminal. 



<!-- Start of picture text -->
1<br>0<br>stdout<br>stdin System.out<br>Process<br>System.in<br>2<br>stderr<br>System.err<br>The System.out in System.out.println() is Java's stdout.<br><!-- End of picture text -->

18 

##### Stdin vs. Parameters 

##### **Parameter** 

- **`$`** `ls dir1` 

dir1 is a parameter — passed directly on the command line, not from standard input. 

##### **Standard Input** 

```
$ grep "a"
```

Once you run this, it waits and reads from your keyboard until you close the stream with Ctrl+D. 

19 

##### Output Redirection 



<!-- Start of picture text -->
$  command > filename<br>New file →  creates it.<br>command Existing file →  overwrites<br>it! Use  >>  to append<br>filename<br>instead.<br>Examples<br>$  ls -l > files.txt<br>→ output of current directory saved to<br>files.txt<br>$  wc -l veggies.txt >> files.txt<br>→ appends the line count to files.txt<br><!-- End of picture text -->

20 

##### Input Redirection 



<!-- Start of picture text -->
$  command < filename<br>command<br>filename<br><!-- End of picture text -->

The command reads its standard input from the file's contents instead of from the console — like redirecting a Java Scanner to read from a file instead of the keyboard. 

_Note: this affects standard input, not command-line parameters._ 

21 

##### Stderr Redirection 

```
$ command 2> filename
```

```
$ command 2>&1
```

```
$ command > filename
2>&1
```

Redirect standard error to filename 

Redirect standard error to standard output 

stdout → filename, and stderr → stdout 

22 

##### Pipes 

```
$ command1 | command2
```

> **`command1 | command2`** 

command1's standard output becomes command2's standard input. 

```
Shorthand for:  command1 > filename  →  command2 < filename
→  rm filename
```

**One of the most powerful ideas in Unix: chain simple commands together to do complex things.** 

23 

##### Combining Commands 



<!-- Start of picture text -->
$  command1 ; command2<br><!-- End of picture text -->

Run command1, then run command2 — regardless of the outcome. ✓ **`$`** `command1 && command2` 

Run command1, and only run command2 if it succeeds. 

24 

## Power Tools & Real-World Use 

Chaining commands together to get real work done 

25 

##### xargs 

Converts standard input into command-line arguments (parameters). 

```
ls *.javaxargsjavac
```

_list of files  →  turns list into arguments  →  compiles each one_ Example — compile every Java file in the current directory: 

```
$ ls *.java | xargs javac
```

26 

##### find 

Searches the filesystem for files matching a pattern. List all .java files, recursively, from the current directory: 

**`$`** `find -name "*.java"` Commonly combined with xargs — compile every Java file found: 

**`$`** `find -name "*.java" | xargs javac` **find has many flags — we'll mostly use -name and -type in class.** 

27 

###### Command Substitution 

```
$(command)
```

Runs the command first, then drops its output directly into the surrounding command as text. 

Example — compile every Java file, recursively: 

```
$ javac $(find -name "*.java")
→  find runs first, its output becomes
javac's arguments
```

28 

##### tee 

Sends output to both a file AND the console at the same time. 



<!-- Start of picture text -->
command tee file.txt<br>console<br>Examples<br>$  command | tee file.txt<br>$  command 2>&1 | tee file.txt   (stdout +<br>stderr → file & console)<br><!-- End of picture text -->

29 

cut 

```
$ cut -d<DELIMITER> -f<FIELD>
```

Splits each line on a delimiter and returns the field you asked for. 

**`a b c d e`** `, , , ,` **field 2 (-f2)** 

Example — split on commas, take the 2nd field: 

```
$ echo "a,b,c,d,e" | cut -d, -f2
```

30 

##### Logs in DevOps 

A status report of a running process — and one of the most common things you'll work with. 

**Dev** 

Include useful, meaningful logging information in the program. 

**Ops** Read the logs — often filtering through large files to find what matters. 

Example — watch logs live, filtered to a keyword: 

```
$ tail -f log_file | grep "text"
```

31 

##### SSH (Secure Shell) 

Log into a remote machine, transfer files, and run commands — all securely. 



<!-- Start of picture text -->
Local Remote<br>Machine Machine<br>TCP/IP port 22<br>$  ssh username@ldapgit.cranecloud.io<br>$  ssh username@ldapgit.cranecloud.io ls /tmp<br>You'll need an SSH client on the local machine — check the man pages for more options.<br><!-- End of picture text -->

32 

##### Recap & Exercises 

**Introduction to Linux** ✓ What Linux is & why DevOps runs on it ✓ Kernel, shell, and the filesystem ✓ Navigating directories & permissions 

##### **Shell Commands** 

✓ 

Files: ls, cd, cp, mv, rm, mkdir ✓ Streams, redirection (>, >>, <) & pipes (|) ✓ xargs, find, cut, tee, SSH & logs 

**3 exercises to be uploaded to MUELE** 

33 

C O M I N G U P N E X T 

# **Git Fundamentals** 

_Version control, branching, and collaborative workflows_ 

**34** 

