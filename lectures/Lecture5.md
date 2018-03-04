Lecture 5:  PYTHON
==================


## Updating your *astr288p* repo (with a twist)

As always, update your git repo. After last weeks' work, you might see a problem now!
```
   cd ~/ASTR288P/astr288p      # make sure you are in one of the 'astr288p' directories
   git status                  # notice something was modified?
   git pull                    # warnings are possible here if there are conflicts
   
   git stash                   # those modified files are "stashed"
   git pull                    # now get the updates
```
For the purpose of our class, it probably was overkill  to *"stash"* these files,
and removing them would have been more efficient, perhaps. So, instead if we do
```
   git status
   rm notebooks/*.*
   git pull
```
But oops, now there is more trouble!  The ones that were not modified, and we removed, are now gone,
and git claims we're up to date. Surely this must be a git bug? It's actually a feature, perhaps
somewhat unexpected.

```
   git checkout origin/master 03-arrays.ipynb
```
The better (and dangerously quiet) way in git to get back to the original version if
```
   git checkout 03-arrays.ipynb
```
## Python

### Official references

* Python Language Reference: https://docs.python.org/3/reference/
* Python Standard Library: https://docs.python.org/3/library/
* Python Tutorial: https://docs.python.org/3/tutorial/

### miniconda3 on the student cluster

If you have trouble installing miniconda3 (see Lecture3) on the student cluster, you can also use
the public (so-called astromake) version as follows:
```
   export PATH=/astromake/opt/python/miniconda3/bin/:$PATH
```
and there should also be my own personal one:
```
   export PATH=/n/ursa/A288P/teuben288/miniconda3/bin/:$PATH
```



### 

We continue with the ipython notebooks from last week, using the command

```
	jupyter notebook
```	

we finished **01-intro** last week, but before we continue with **02-flow**, let us examine **01-run**.
We will then need to finish **03-arrays** and **04-plotting** in order to do **Homework-01** due next week!
