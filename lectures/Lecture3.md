Lecture 3:  Remote sessions, manipulating your $PATH, login scripts
================

## 1. Remote Access 

### Remote login

Remote access or remot login allows you to remotely connect to another machine via a terminal. We use **ssh**:

```
	ssh user@remote
```

If properly configured, ssh can also be used to forward graphical information. This can be tested using (e.g.) **xeyes** or **xclock**. 
```
	ssh -Y user@remote
	xeyes
	xclock
```

Running an ssh remote session is like having a terminal directly on that machine. Your $HOME directory is actually a network drive mounted on another machine (URSA), when logging into URSA you will have access to all the files in your home directory.

```
  ssh -Y user@ursa.astro.umd.edu
```

Remote logins can *speed* some processes up, like installing software in a directory which is actually a network drive mounted on another machine (URSA), but  can also *slow* some processes down, like running graphacal processors such as editors.

**NOTE:** If you log into URSA you will likely be running the default **tsch**, use **bash** command to change shells on URSA. You can also use the **chsh** command to change your login shell (will require you to log back into URSA). 

### Remote file transfer

If you want to move files from one computer to another, there are several tools avaialbe. Arguably the simplest is **scp** (**s**ecure **c**o**p**y).

To copy a file to a remote machine:
```
	scp file user@remote:/path/to/remote/destination
```
We can also do this to entire directories using the **-r** flag (**r**ecursive).

You can also use scp to copy files from a remote machine to a local machine:
```
	scp user@remote:/path/to/target /path/to/local/destination
```

There are other commands, like **rsync** which offer effectively the same product, but have more features (e.g. resuming transfers, progress bars, etc.)

**Q3-1**: What might you use the first example for? And the second? 

## 2. Adding to your own $PATH:

We went through the effort of downloading sublime_text, but now we need to be able to run it. As we saw last week, it can be run from the directory where it was installed: 

```
    cd ~/ASTR288P/software/sublime_text_3
    ./sublime_text
```

but what if we want to open it from somewhere else? In Unix, executtables must be located in your $PATH in order to be seen by the command line.

```
    echo $PATH
```

We can add directories to the path 

```
    export PATH=~/software/sublime_text_3/:${PATH}
```

**Q3-2**: How do you permanently add something to the $PATH?

## 3. Variables

In many shells, there are a number of variables designed to make life easier

  - $HOME -- The path to your home directory
  - ~ (tilde) -- This is an alias to $HOME
  - $PWD -- **P**ath **W**ith **D**irectory
  - $PATH -- The list of locations of all the different executables on your system
  - ...
 
### Creating new variables  

In bash (different in other shells), 
```
    export WORKDIR=${HOME}/some/long/path/to/avoid/typing
```
allows you to quickly access the directory in question via (e.g.)
```
    cd $WORKDIR
```
### Aliasing

You can also **alias** commands for shortcuts. For example:
```
alias grep="grep -n --color=auto"
```
Now, when **grep** is called, it calls it with the **-n** and **--color** flags. 

**Q3-3**: What does the **-n** command do?

If you want to permanetly add *variables* or *aliases* they can be added to your **.bashrc** file in your home directory. 
Recall from lecture 1, the **.bashrc** file is a file which the terminal executes at startup. Adding *variables* or *aliases* to the startup file will provide you with permanent access to those features.    

## 4. Links

Linking files is like have a convenient shortcut available (similar to creating the WORKDIR path variable above), e.g.

```
  ln -s /etc/passwd               # soft link (can go across devices)
  ls -l passwd
  head passwd

  rm passwd
  ln /etc/passwd                  # hard link (must be on same device)
```

Did you get an error in the last attempt?  If yes, you are likely trying this across to another device. The **df** command will list the current devices/mounted file systems (e.g, harddrives or USB keys) or on what device a file lives.

```
  df .
  df /etc/passwd
  df
```

Lets try this again

```
  ls -l ~/.bashrc 
  ln ~/.bashrc dot-bashrc
  ls -l ~/.bashrc 
```
   

## 5. PYTHON

The python language often comes natively on your UNIX system. Try the following commands in **ipython** (or **python** if you don't have **ipython** yet):
```
   LAPTOP> which python
   LAPTOP> which ipython
   LAPTOP> ipython
   In [1]:  import numpy
   In [2]:  import scipy
   In [3]:  import astropy
   In [4]:  import astroML
   In [5]:  import admit
   In [6]:  quit
```
At some point you might see the message **no module named '...'**, this is because the module has yet to be installed.

## 6. Anaconda and Miniconda

**Miniconda** is a very barebones version of python which you can tailor to your own needs. See also http://conda.pydata.org/miniconda.html.

If you need more, download the full **Anaconda** version. With this you get a nice graphical install and by default more functionality such as additional modules including jupyter and spyder. See https://www.continuum.io. 

### On Linux:
```
  df .
  wget https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh 
  bash Miniconda3-latest-Linux-x86_64.sh
```

Make sure you do these commands on a locally mounted disk, not NFS (network) mounted!

### On Mac:
```
  curl https://repo.continuum.io/miniconda/Miniconda3-latest-MacOSX-x86_64.sh > Miniconda3-latest-MacOSX-x86_64.sh 
  bash Miniconda3-latest-MacOSX-x86_64.sh
```

And now, in common to both Linux and Mac, you will answer some questions and at the end a modification to your **~/.bashrc** file (linux) or **~/.bash_profile** (mac) will be made.

```
  export PATH="$HOME/miniconda3/bin:$PATH" #bash 
  setenv PATH "$HOME/miniconda3/bin:$PATH" #tsch
```

And now make sure your shell is looking at this new python (e.g. **source ~/.bashrc** for your current shell, or open a new shell):

```
  which python
```

Now continue installing some modules that we will need for future lectures

```
  conda install ipython numpy scipy matplotlib notebook ipywidgets networkx
  conda install astropy
  conda install jupyter

```

See what modules you have installed:

```
  conda list
```


### "Hello World!" in python

```
	echo 'print("Hello World!")' > hello.py
	python hello.py
```	

In our scripts we can avoid having to type the name **python**, using the **!#**:

```python
	#! /usr/bin/python
	#
	print("Hello World!")
```
or more generally
```python
	#! /usr/bin/env python
	#
	print("Hello World!")
```

**Q3-4**: What is **!#** doing in the above? What is the difference between the two scripts above that *appear* to do the same thing.


### The C compiler and hello world

```
	emacs -nw hello.c
```

```C
	#include <stdio.h>

	void main() 
	{
	  printf("Hello World from C!\n");

	}
```

```
	gcc -o helloc hello.c
	ls -l hello.c
	ls -l helloc
	helloc
	more helloc
	cat helloc
```

## 7. GRIP

GitHub Readme Instant Preview, **GRIP**: a command that allows you to preview [*MarkDown*](https://en.wikipedia.org/wiki/Markdown) files in a web browser. Allows you to view *MarkDown* while offline. 

These lecture notes are in md(*MarkDown*) format, they are simple text files that are a lightweight markup language, and they format nicely in a web browsers.

Install and use it as follows
```
   pip install grip
   grip Lecture2.md
   grip Lecture3.md localhost:6420
```
pip is just another package manager, like when we did **conda install** previously.
Some packages need to be installed via **pip**, but always try **conda install** first. 

Because python also has a built-in http (web) server, you can now open a URL on
[http://localhost:6419](http://localhost:6419), or
[http://localhost:6420](http://localhost:6420) in the second case. Just make sure
to use unique port numbers.
