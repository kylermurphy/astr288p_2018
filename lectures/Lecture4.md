# Lecture 4:  PYTHON

## Updating your *astr288p* repo

Remember to always update your git repo for this class. New material is added weekly.
```
cd ~/ASTR288P/astr288p      # make sure you are in one of the 'astr288p' directories
git status                  # first make  sure you don't have anything modified
git pull                    # warnings are possible here if there are conflicts
```

## References

* Unix Shell : http://swcarpentry.github.io/shell-novice/
* Python : http://swcarpentry.github.io/python-novice-inflammation/
* PSL :   https://swcarpentry.github.io/python-second-language/
* Learn Python : https://www.tutorialspoint.com/python/index.htm

## Python 

In the previous lecture we installed our own version (miniconda3) of Python. Make sure
you have the right version using the **which** command!   There are at least 4 ways you
may wind up running python:

### 1. python: the script interpreter

```
which python
python
```

Normally never used when in an interactive python session like **ipython**, but python scripts normally start with

```
#! /usr/bin/env python
```

so you can use them just like another unix command on the terminal/command line (see also the **hello world** python example from the previous lecture).

### 2. ipython: 

Interactive python, ideal for small tasks, running scripts/code, or quickly trying something out

```
ipython
```	

### 3. graphical user interface

There are a number of options, most of them have *introspection-based code completion* (quick code and tab completion) and *integrated debugger*

* PyCharm
* KDevelop
* PyDev (eclipse)
* Spyder (anaconda) 

You can install this:   **conda install spyder**

We will not be using these in this class, but it can be a great way for development.

### 4. jupyter: web interface

```
which jupyter 
jupyter notebook
```	

Now watch your default browser opening a new tab. Navigave to your **astr288p/notebooks** folder, where
you should see some *.ipynb* files.  The rest of this lecture will be taking place in the notebooks.

We will start with **Lecture04_01_intro.ipynb**

