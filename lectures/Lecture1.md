# Lecture 1:  Introduction to UNIX

## Command Line unix (CLI) vs. desktop unix (Graphical User Interface, GUI)

  - GUI: a dime a dozen (and new ones keep coming...)
  - GUI: Mac (aqua) and Linux (X11)
  - GUI: Linux has many many window managers
         (twm, fvwm, enlightenment, gnome, kde, unity, plasma)
  - GUI: Linux is changing from using X11 to Wayland
  - CLI: one and only one (though minor differences do remain between Mac and Linux)

Shells can be **GUI** or **CLI** shells and act as an interface to the operating system's different services.

The notes below loosely follow the tutorials in
    http://www.ee.surrey.ac.uk/Teaching/Unix/
you are recommended to walk yourself through these.

## Login shell in a terminal: 
  - xterm                  (probably the oldest terminal in X11)
  - gnome-terminal         (Gnome Terminal)
  - xfce4-terminal         (XFCE4 terminal)
  - konsole                (KDE terminal)
  - emacs "M-x shell"      (yes, you can run a terminal inside of emacs, great for logging)


### What shells can we use? 

There are many CLI shells avaialble. Some exambles:

  - bash  (sh: bourne shell)
  - tcsh  (csh: C-shell)
  - ksh   (korn shell)
  - xonsh (pythonesque shell, cf. ipython)

We will be using **bash**.

   Q2-1: how do you know which shell you are running?

   A2-1: as is often in UNIX, several answers possible, that all need human parsing
   ````
   echo $SHELL 
   grep $USER  /etc/passwd
   ps
   ````
   Q2-2: What are the allowed shells on your unix system?
   
   A2-2: Use **cat** to view whats in **/etc/shells** or **chsh --lish-shells**
   ````
   cat /etc/shells
   chsh --lish-shells
   ````

   Q2-3: If a shell is not listed in **/etc/shells**, can I still use it?

   A2-3: yes, simply run it from the current shell (a shell within a shell; see A1)

### Changing your default shell

In this class, we will use **bash**, although in the future you may decide to use another default shell.
To change your default shell, type 
```
chsh -s /bin/bash
```

For this to take effect, you need to open a new terminal!

### Shell options (as defined in /etc/passwd, see /etc/shells)
/etc/passwd contains essential information relevant for user login.
An example line: 
```
tiberius:x:5091:500:Captain Kirk:/home/tiberius:/bin/tcsh
```
There's more information here than we need for the scope of this course, but the important fields are
  - tiberius : User name.
  - x is the password (it always comes up as 'x'; the actual encrypted password is stored elsewhere)
  - 5091: User ID (UID)
  - 500: Group ID (GID); we'll come back to this one later when we discuss file permissions
  - Captain Kirk: This is a comment field.
  - /home/tiberius/ : Path to a user's home directory when they log in.
  - /bin/tcsh : This means that on login shell /bin/tcsh is used. This can also be a command, as opposed to a shell.

CAVEAT: MacOS does not seem to use /etc/passwd (see http://docstore.mik.ua/orelly/unix3/mac/ch03_08.htm)


### Persistent shells with session management (cf. VNC)
If you don't need a full graphical interface, and still want to login to server (e.g. ursa) and maintain your session, use any of the following programs

  - screen        (often comes with UNIX)
  - tmux          (and there are more)

**screen** is useful if (e.g.) you have some code that takes a long time to execute and you don't want to have to keep the termainal open (say, if you're getting on an airplane).

## bash
We differentiate between an *interactive*  and *login* shell. They are controlled by one or more startup ("rc") files:
   * login:
      * /etc/profile
      * ~/.bash_profile
      * ~/.bash_login
      * ~/.profile
   * interactive
     * /etc/bash.bashrc
     * ~/.bashrc

  Some of your personal files may already be present when your account was activated. Use
  the **ls -a** command to see these hidden (files starting with a dot) files.

  Q2-4:  With the **ls -a** command you will also see **.** and **..**    what are those?

  A2-4:  The current directory **.** and the parent directory **..**

### Linux and Mac philosophy on interactive and login shells different?

This is often source of confusion and discussed online
(e.g. see http://unix.stackexchange.com/questions/119627/why-are-interactive-shells-on-osx-login-shells-by-default)

Here's a summary for Linux and Mac, and when they read the startup files (WARNING: they are not the same!)

```
  linux>  ssh localhost                                 # login
  	  bash: .bash_profile                           # Q: what about .bash_login and .profile?
	  tcsh: .cshrc .login                           # in that order
	  
  linux>  xterm (or open a gnome-terminal)              # interactive
  	  bash: .bashrc
	  tcsh: .cshrc

  mac> ssh localhost                                    # login (enable in System Preferences -> Sharing -> Remote Login)
       -> .bash_profile

  mac> Terminal  (CMD-N)                                # login
       -> .bash_profile                                 # if [ -f ~/.bashrc ]; then . ~/.bashrc; fi
       bash                                             # interactive
       -> .bashrc 
```

If you use the **csh** variety, the **.login** and **.cshrc** files control which one is read for what type of session.

## Files and Directories - Part 1:

```
  ls                  LiSt files
  pwd                 Print Working Directory
  whoami              Isn't that obvious?
```

## How to get more help for a given COMMAND:
(this obviously means you know the name of the COMMAND)

```
  COMMAND --help
  COMMAND --version
  man COMMAND
  info COMMAND

  which COMMAND
  whatis COMMAND
  apropos COMMAND
  <google>
```  

  Q2-5: man pages have sections (the -s option) to narrow down search

## Files:  the "ls" command

```
  ls -l   # l for long 
  ls -al # all long
  ls -lt # long, sort by modification time
  ls -ltr # long, sort by modification time, reverse order
  ls -lt | tac 
  ls --full-time #what does this one do? 
```
  Q2-6:  What is the '|' symbol doing? 

  Q2-7:  What is the 'tac' command?

  Q2-8:  What are '.' and '..' ?


## Directories:

```
  pwd
  mkdir ASTR288P
  cd ASTR288P            (try typing just 'A' or "AS" and then <TAB>-complete)
  pwd
```

## git: sharing your codes: a first encounter

We will come back to **git**, but the following commands will download the "astr288p" repository of codes and documentation that are helpful for this class.
```
  git clone https://github.com/SeanCGriffin/astr288p_student
  ls
  cd astr288p_student
  ls -la
```
But wait -- there's nothing but the course outline in the repository!

I need to add the correct files to the repository.

```
    git add lectures/Lecture1.md
    git commit
    git push
```

Now, if we do 
```
    git pull
```

you should be able to see this doucment!

This **Lecture1.md** file is the file you are reading now. Most humans can read it, but it does read a little nicer once it has been formatted by a web browser, instead of straight to the terminal! Or you can read it directly on github on
https://github.com/kylermurphy/astr288p_2018/blob/master/lectures/Lecture1.md

````
less lectures/Lecture1.md
````
