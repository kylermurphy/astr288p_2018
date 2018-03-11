# Lecture 5:  PYTHON

## Recap

Things we should feel familiar with:

       * local (unix) terminal to type commands:   ls, pwd, cd, mkdir, cat, more, rm, mv
       * ssh into ursa
       * installing your own python (miniconda or anaconda)
       * understanding how to modify your environment ($PATH, etc.)
       * basic usage of python in "notebook" - printing variables, lists etc., if/then/else/for/while
          list:        a =  [1,2,3.0,'4']
          tuple:       b = (1,2,3.0,'4')
          dictionary:  c = {'1':1,  '2':2, '3': 3.0, 'four':'4'}
          set:         d = {1,2,3.0,'4',2,1,3}
	  
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


### 

We continue with the ipython notebooks from last week, using the command

```
	jupyter notebook
```	

we finished **01-intro** and **02-flow** last week. This week we will continue with ipython notebooks
and learn about one of most important data structures in scientific programming: arrays and plotting.
