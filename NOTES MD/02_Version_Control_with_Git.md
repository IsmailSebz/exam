Version Control with Git BSE 4105 – 2026/1 

Alex Mwotil 

1 

#### What We'll Cover 

## **01** 

###### **Why Version Control** 

The problems it solves 

## **02** 

**Git Fundamentals** 

Repos, staging, commits 

**03** 

###### **Branching** 

Diverge, work, merge back 

**04** 

###### **Working with Remotes** 

Push, pull & pull requests 

_Everything here runs on the Linux shell skills from the last session/exercises._ 

2 

### Why Version Control 

The problems that make version control necessary 

3 

##### The Problem — Working Solo 

_"My software code is working great!"  …and then:_ 

**?** 

**?** 

**?** 

I edited and saved over I deleted a file — or an My laptop was stolen, or the working version. important section. the disk failed. **How do I get back to the Where is my file now? Where are all my files? code that worked?** And the classic filename problem: 

```
Solution_edited.ppSolution_dont_deleSolution_FINAL_v2.
Solution_1.ppt
tte.pptppt
```

**_How do I manage all of these?_** 

4 

##### The Problem — Working as a Team 

Final Year Project — four team members, one report document. 

- **?**<sup>Where do we store the document?</sup> 



**Member 1** 





<!-- Start of picture text -->
Member 2<br><!-- End of picture text -->

- **?**<sup>Who will have the latest version?</sup> How do we share each other's 

- **?** changes — over a phone call? 



**Member 3** 

```
report
```



**Member 4** 

- **?**<sup>How do I compare version 1 against</sup> version 5? 

- **?**<sup>Whose laptop do we back up to? Is</sup> that even safe? 

5 

#### What is Version Control? 

**The process of tracking and managing changes to digital assets over time.** 



<!-- Start of picture text -->
Also known as source code management (SCM)<br>revert to any earlier version<br>ee eee 4<br>v1 v2 v3 v4<br>earlier earlier earlier now<br><!-- End of picture text -->

_You already use version control every day — Undo in an editor, and revision history in Google Docs._ 

6 

##### Version Control Systems (VCS) 

Software that automates the version control process — no manual copies, no adhoc scripts. 

###### **Tracks changes** 

###### **Keeps full history** 

Every edit to a file or set of files, over time. 

A complete record of code and other files — revert to any version. 

###### **Follows the SDLC** 

###### **Enables collaboration** 

Tracks code across development and iterations, managing change. 

The single most important tool for working as a team. 

7 

#### The VCS Landscape 

Many systems and hosting platforms exist — we'll use Git. 

**GitHub GitLab Bitbucket Beanstalk Perforce Apache Subversion AWS CodeCommit Mercurial Git is the version control system. GitHub and GitLab are platforms that host Git repositories.** 

8 

Git Fundamentals 

Repositories, the staging area, and commits 

9 

#### What is Git? 

###### **A free, open-source, distributed version control system.** 

**1** 

**A DevOps tool** Used for source code management across the delivery pipeline. 

**2** 

**Scales** Handles small projects and very large ones efficiently. 

**3 Tracks changes** Records every change made to the source code over time. 

**4** 

**Non-linear work** Many developers working in parallel, then merging together. 

_Created by Linus Torvalds in 2005 — the same person who created Linux._ 

10 

#### What is a Repository? 

A repository ("repo") is a location that stores a copy of your project's files — and their full history. 



<!-- Start of picture text -->
different from<br>Working Directory Repository<br>The files you actually see and edit — also The stored copy plus the complete history of<br>called the working tree. every change.<br>Every collaborator has a complete copy of the repository — history and all.<br><!-- End of picture text -->

##### What Belongs in a Repository? 

> ✓ **Commit these** 

> ✕ **Keep these out** 

Source code files  (.c, .java, .py …) 

Build files  (Makefile, build.xml) Images and general resource files Documentation and README files 

Object files  (.class, .o) Executables and build output Anything you can regenerate Passwords, keys, secrets 

**Never commit secrets. Use environment variables — a pushed password lives in the history forever.** 

12 

##### Distributed: Local & Remote 



<!-- Start of picture text -->
A remote (central) repository is hosted on a platform like GitHub or GitLab. Everyone keeps a full<br>local copy.<br>Remote repository<br>GitHub / GitLab<br>push pull<br>Local repo Local repo Local repo<br>Developer 1 Developer 2 Developer 3<br><!-- End of picture text -->

13 

#### The Four Areas of Git 

###### A simplified model of the Git phases — remember this! 

**Working Directory** Your changes, as you edit 

**`git add`** [d 

**`git` Staging** **`commit`** as **Area** — Changes prepped for commit 

**Local Repository** Local copy with your commits 

**`git push` Remote** [_d — **Repository** Shared repo, e.g. GitHub 



**git pull  — bring remote changes back down into your working directory** 

14 

#### Inspecting State 

Two commands you will run constantly — before and after almost everything else. 

```
$git status
```

```
$git log
```

**What's changed right now?** Shows the state of files in your working directory and staging area — what's modified, what's staged, and what Git isn't tracking yet. 

###### **What happened before?** 

Shows the commit history — every snapshot taken, who took it, when, and the message they left explaining why. 

15 

#### Essential Git Commands | Cheat Sheet 

```
git clone url [dir]
```

Copy a Git repository 

**`git add files`** Add file contents to the staging area **`git stage files`** Same as git add **`git commit`** Snapshot the staging area and create a commit **`git status`** View status of the working directory and staging area **`git diff`** Show differences between staging and working directory **`git log`** Show commit history **`git pull`** Fetch from the remote and try to merge **`git push`** Push the local repository to the remote 

View status of the working directory and staging area Show differences between staging and working directory Show commit history 

Fetch from the remote and try to merge Push the local repository to the remote 

_Run any of these with --help to see the full set of options._ 

16 

#### Adding & Committing 

###### **1.  Stage the files you want in the next snapshot** 

```
$git add file1.txt file2.txt
```

A snapshot of both files is added to staging. You can keep editing them — but you'll need to add them again for those newer changes to be staged. 

**2.  Move staged changes into the local repository, with a message** **`$`** `git commit -m "Updated filename"` 

**All of these act on your LOCAL repository. Nothing reaches your teammates until you run git push.** 

17 

##### Undoing: Unstage a Change 

Added something to staging by mistake? Take it back out. 



<!-- Start of picture text -->
git reset<br>Working Staging<br>Directory Area<br>$ git reset HEAD filename<br><!-- End of picture text -->

The file goes back to being an unstaged change. Your edits are NOT lost — only the staging is undone. 

18 

###### Writing Good Commit Messages 

###### **Longer message** 

###### **Quick message** 

- **`$`** `git commit` 

Opens your default editor. Write a subject line under 50 characters, leave a blank line, then add as many paragraphs of detail as the change deserves. 

**`$`** `git commit -m "My message"` Types the subject line directly on the command line. Useful for simple, selfexplanatory commits — most of what you'll do day to day. 

**Write the message for the person reading it in six months. That person is usually you.** 

19 

#### Configuring Git 

Set your identity once — Git stamps it on every commit you make. 

```
$git config --global user.name "My Username"
$git config --global user.email username@email.com
```

```
$git config --list                        verify what is set
```

```
$git config --global push.default simple  silence the push warning
```

```
$git config --global core.editor vim      editor for commit messages
```

**--global applies to every project. Drop it to set a value for one repository only.** 

20 

### Branching 

Diverge from the main line, work safely, then merge back 

21 

#### Why Branch? 

Everything so far has happened on one branch — master (also called main). 

**master is the single point of truth** 

**So work on a branch instead** 

> ✓ Code on master should be stable 

> ✓ It should always compile 

> ✓ Branch off master for each feature 

> ✓ Break things freely — master is safe 

> ✓ It is what everyone else builds on 

> ✓ Merge back once it actually works 

**Working directly and collaboratively on master is how you break everyone's build at once.** 

22 

#### Commit History 

Every commit references its parent — the commit that came before it. 



<!-- Start of picture text -->
points to its parent<br>is<br>X Y Z<br>first commit most recent<br>A branch is not a copy of your files — it is just a moving pointer to one commit in this chain.<br><!-- End of picture text -->

23 

##### HEAD & the Main Branch 



<!-- Start of picture text -->
HEAD<br><!-- End of picture text -->

```
master
```

```
X
```

**`HEAD`** A reference to the branch you are currently on. Move branches and HEAD follows you. 

```
Y
```

```
Z
```

```
master / main
```

The main branch of the repository, created by default when you initialise it. 

24 

Creating & Switching Branches **`$`** `git branch feature` **`$`** `git checkout feature` ee oo 8” Both branches point at the same commit. HEAD has moved to feature — you are now working there. _git checkout -b feature  creates the branch and switches to it in one step._ 

25 

Committing on a Branch **`$`** `echo "update" > file.txt` **`$`**<sup>`git add file.txt`</sup> **`$`**<sup>`git commit -m "W"`</sup> ee Q©o = **The new commit W lands on feature. master has not moved.** 

26 

# Diverging Histories **`$`** `git checkout master` **`$`** `echo "V" >> file.txt` **`$`** `git add file.txt  &&  git commit -m "V"` ee **`W`** G © on **`HEAD` Two branches, two different commits, one shared ancestor. The histories have diverged.** 

27 

#### Merging Branches 

```
$git merge feature
```

Run from master — integrates the changes on feature into the branch you are currently on. 



<!-- Start of picture text -->
ae<br><!-- End of picture text -->

**M is a merge commit — it has two parents, one from each branch.** 

28 

Working with Remotes Sharing your commits with everyone else 

29 

#### Local vs. Remote 

Your local repository and the remote each keep their own copy of the history. 



<!-- Start of picture text -->
Local Remote<br><!-- End of picture text -->

```
origin/master
```

A commit reference marking the last commit you fetched from the remote named origin. 

30 

#### git push 

You commit locally — the remote knows nothing about it until you push. 



<!-- Start of picture text -->
Local Remote<br><!-- End of picture text -->

```
$git push
```

**W is copied up to the remote, and both master pointers now agree.** 

31 

#### git fetch & git pull 

Someone else pushed. How do their commits reach you? 

- **`$`** `git fetch` 



<!-- Start of picture text -->
$ git merge<br><!-- End of picture text -->

Downloads new commits from the remote and updates origin/master — but does NOT touch your working files. 

Integrates those fetched commits into the branch you are currently working on. 

> **`git pull` =** **`git fetch` +** 

```
git merge
```

_git pull does both steps in one command — which is why it sometimes surprises you._ 

32 

##### The Pull Request Workflow 

In practice you rarely merge locally and push. You let GitHub or GitLab run the merge. 



<!-- Start of picture text -->
1 2 3 4 5<br>Branch Push Open PR Review Merge<br>Create a local  Open a pull /  Collaborate, leave  Merge into master<br>Push that branch<br>branch and make  merge request on  comments, fix  once it is<br>up to the remote<br>your commits GitHub or GitLab conflicts approved<br><!-- End of picture text -->

**Be deliberate about what lands on master. Know when to branch, and when to merge.** 

33 

### Getting Set Up on GitLab 

Crane Cloud GitLab — access, SSH keys, and your first push 

34 

#### Crane Cloud GitLab 

Our GitLab instance for this course unit — this is where your work will live. 

```
https://gitlab.cranecloud.io/
```

**Your credentials** The same username and password you use for SSH on the lab machines. 

**Self-managed** Our own GitLab instance, separate from gitlab.com. A gitlab.com account will not work here. 

###### **Start early** 

Get working before this week’s exercise is due. Don't leave it to the deadline. 

35 

> **1** Generate an SSH Key 

**Generate the key on the ldapgit machine, logged in under your own user account.** First — check whether you already have one: 

```
$ ls ~/.ssh/
```

_Look for id_ed25519 / id_ed25519.pub (or id_rsa / id_rsa.pub). If they exist, skip to step 2._ Otherwise, create a new key pair: 

```
$ssh-keygen -t ed25519 -C "your.name@students.mak.ac.ug"
Press Enter to accept the default path [do not enter a
passphrase]
```

_ED25519 is the preferred key type. Use  ssh-keygen -t rsa -b 4096  only if ED25519 is unavailable._ 

36 

**2** Add the Key to GitLab Copy your PUBLIC key — the .pub file: **`$`** `cat ~/.ssh/id_ed25519.pub` 

**`id_ed25519.pub id_ed25519`** ✓ ✕ **public — safe to share** private — never share Then, in GitLab: **Select your Access  ›  SSH Add new key, avatar Edit profile keys paste, save (upper-right)** _Give the key a Title you'll recognise. You may also set an expiry date._ **Full instructions:  docs.gitlab.com/user/ssh/** 

37 

###### **3** Verify & Set Your Identity 

Test the connection: 

```
$ssh -T git@gitlab.cranecloud.io
Welcome to GitLab, @username!
```

_On the first connection you'll be asked to confirm the host's authenticity — type yes._ Then tell Git who you are — it stamps this on every commit: 

```
$ git config --global user.name "My Username"
$ git config --global user.email username@email.com
$ git config --list
```

**Use the same email as your GitLab account so your commits are linked to your profile.** 

38 

###### **4** Your First Repository 

###### Everything from this deck, end to end — clone, change, stage, commit, push. 

- **`$`** `git clone git@gitlab.cranecloud.io:group/project.git` **`$`** `cd project` 

- **`$`** `echo "my notes" > notes.txt` 

- **`$`** `git status` 

- **`$`** `git add notes.txt` 

- **`$`** `git commit -m "Add notes file"` 

- **`$`** `git push` 

```
clone
```



<!-- Start of picture text -->
edit add commit push<br><!-- End of picture text -->

_Use the SSH clone URL (git@…), not the HTTPS one — that's what your key authenticates._ 

39 

#### Recap & Exercise 

#### **What we covered** 

#### **Before the next session** 

> ✓ Why version control exists 

> ✓ Repos, staging & commits 

> ✓ Branching, HEAD & merging 

> ✓ Sign in to gitlab.cranecloud.io 

> ✓ Generate your SSH key on ldapgit 

> ✓ Add the public key to GitLab 

> ✓ Push, pull & pull requests 

> ✓ Verify with ssh -T and clone a repo 

**Full SSH key instructions: docs.gitlab.com/user/ssh/     •     Exercises on MUELE** 

40 



<!-- Start of picture text -->
AM<br><!-- End of picture text -->

#### **Thank You** 

Alex Mwotil alex.mwotil@mak.ac.ug 

41 

