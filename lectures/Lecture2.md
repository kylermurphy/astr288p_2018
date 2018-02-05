  Lecture 2:  More on UNIX
================


## Updating your *astr288p* repo
Any time you need to update your **astr288p** git repo, the **git pull** command will do this:
```
   cd ~/ASTR288P/astr288p_2018      # make sure you are in one of the 'astr288p' directories
   git status                 		   # first make  sure you don't have anything modified
   git pull                            # warnings are possible here if there are conflicts
```
It would actually warn you if you had modified files that are also modified on the server. It will attempt a merge and warn you.  Files that you modified and are not modified on the server.

## 1. The Shell and Terminal
More on the shell and terminal:
* The shell is a program that *executes* commands. 
* The terminal is a program that allows us to *interact* with the shell and parse commands.
* Tab completion - **Tab** will complete some tasks from the command line including, commands and file listing (**ls**, **cd**).
* History - commands within the terminal are typically stored and can be accesed using the up and down arrows.
* Comments - within a terminal anything following **#** is what is referred to as a comment which will be ignored. The comment is typically descriptive text which we use to explain what what a particlar line is doing (generally moreimportant when scripting and programming).  

## 2. Creating Files:

Although it does not matter where you do this, for the sake of organization, lets keep class files in **~/ASTR288P**:
```
  cd ~/ASTR288P
  mkdir lecture2
  cd lecture2
```
  1) **touch**   (Zero Length file)
```
     touch Data0.txt
     mkdir data0.txt          # testing case sensitivity 
```

  **Q2-1**: On a Mac this last **mkdir** may have failed. Can you see why?
  
  2) **echo** - display a line of text
```
     echo Hello1   >  Data1.txt
```

  3) **cat**
```
     cat Data1.txt
```

  **Q2-2**: What does **cat** do? Or, what command can you use to find out what **cat** does? 

```     
     echo Hello2   >  Data1.txt
     echo Hello3  >>  Data1.txt
```

  **Q2-3**: What are the **>** and **>>** symbols doing?
  
```
     cat > Data2.txt
     1 2 3
     2 3 5
     3 4 7
     ^D                       # Ctrl-D a.k.a. end-of file (EOF), ^C (Ctrl-C) also works
     cat >> Data2.txt
     4 5 9
     5 6 12
     6 7 14
     ^D
```

  **Q2-4**: How do you display what is in the file **Data2.txt**
  
  4) your favorite **$EDITOR**

Editors that can be accessed within the Terminal:
```
     emacs     (C-x C-c)  or:   ^x^c  to exit
     vi        ( ':q!"  or "ZZ" to exit, the latter one also saves the file!!!)
     pico      (^X to exit)
```
Editors with GUI's:
```
     gedit     (^Q or ^W) to exit, or click on File->Quit
     Notepad++
     Atom
     Sublime
     Visiual Studio
```
     Many editors keep a backup copy, often with a tilde (~) appended to the filename.


##  3. Viewing Files:

Many ways to view a file on the terminal:

     cat       the whole thing to the terminal
     more      paging section by section ('q' to get out, '?' to get help)
     less      "less is a better more" (/FOO   to search for the word FOO)
     tac       (reverses the lines)

     head      the first portion
     tail      the last portion

## 4. Extracting/Reducing files:


     wc        WordCount (and line and character) count
     sum       check sum (see also md5sum)
     grep      show lines that match some pattern (cf. google and googling)

## 5. Other File Operations:

     cp        CoPy files
     mv        MoVe files (also renaming if it's not going to another directory)
     rm        ReMove files (directories would need the -r flag, but see also mkdir)
     ln        LiNk between files (symbolic/soft vs. hard link)


## 6. UNIX PATH

Any command typed in the terminal will find the command from an executable file located in a directory listed in the $PATH environment variable:

```
   echo $PATH
   
   which ls
   which man
   which ds9
```


## 7. Scripting:

Scripting in UNIX is nothing more than a few shell commands in a text file, which you can execute directly using the shell (the interpreter):

A simple script:

```
     echo "echo hello world" > hello.sh
     bash hello.sh
     ls -l hello.sh

     chmod +x hello.sh
     ls -l hello.sh  
     hello.sh
     echo $PATH
     ./hello.sh
```

Scripting allows more complex tasks to be completed: 
- Downloading data from the web. 
- Compiling programs.
- Scheduling tasks to be run periodically at fixt times, dates, or intervals.

## 8. Permissions:

In the last section, we did something that made the script **executable**:

```
    chmod +x hello.sh
```

This means that we added the permission to execute the code from a shell. Other permissions are read and write, which are permissions allowing users to to view a file and write or modify files. 

You can see what permissions a file has by doing
```
    ls -l
```
and looking at some example output:
```
    drwxr-xr-x  4 griffins veritas   39 Jan 30  2015 1ES1727+502
    -rw-r--r--  1 griffins veritas  66K Nov  7  2015 77470_t0.voltages
    -rw-rw-r--  1 griffins veritas  56K Nov  7  2015 77500_t0.voltages
    -rw-r-----  1 griffins veritas  12M Dec  2  2015 79564.cvbf
```
The columns are:
  - Permissions
  - Number of links to the file / directory
  - Name of owner (**user**)
  - The **group** the files belong to. Yours will be "student" or something similar. There are multiple groups that correspond to different types of user. 
   - File size.
   - Date the file was last modified. 
   - The filename

Permissions can be broken down into three sections: user, group, other. 
The first character indicates if it's a directory (**d**), the next three characters correspond to the read, write, and execute perimissions for the user, and similarly for the group, and then other. 

**Q2-4**: Describe the details of the above files. Which files are excetuables? Which files are directories?

### Changing permissions
```
    chmod a+x : add execute access for all users
    chmod g-x : remove write access for group memebers
    chmod o-wx : remove write and execute access for non-user, non-group memebers
```

## 9. Finding files:

1) **locate** - find files by name
```
    locate -i poster
```
      
2)  **find** - search for files in a directory hierarchy (arguably one of the more complex UNIX commands)
```  
    find $HOME/Talks -name "*oster*"
```
## 10. Tarballs

A **tarball** is a type of file archive. It is a convenient method of transporting multiple files and folders around. 

### Extracting an archive
For this example, we'll download a popular text editor called sublime_text (note that we may need to update the link if a new release is provided): 
```
    cd ~/ASTR288P       # Navigate to our working directory.
    mkdir software      # Make a new directory
    cd software         # Move to it
    wget https://download.sublimetext.com/sublime_text_3_build_3143_x64.tar.bz2 #Download the file
```
You can see that the file extansion here is .tar.bz2. The .bz2 means that the file is also **compressed**.

We can decompress the file:
```
    bunzip2 sublime_text_3<Tab-complete> 
```
and then un-tar (un-archive) the tarball:
```
    tar -xvvf sublime_text_3<Tab-complete>
```
The flags in being used: 
```
    x : eXtract
    v : Verbose
    v : even more Verbose
    f : Filename specifier
```
**Q2-5**:  What changes if you remove a single $$v$$ flag? 

NOTE: In practice, it is not necessary to bunzip the tarball before calling **tar -xf**; the program is smart enough to know what's going on.

### Creating an archive

To create an archive:
```
    cd ~ #go home 
    mkdir software/some_working_directory
    touch software/some_working_directory/example.log
    echo "Test pattern" > software/some_working_directory/test.log
    tar -cvvf my_tarball.tar software/
```
**Q2-6**: What is the **-c** doing?

**Q2-7**: What are the contents of *my_tarball.tar* (someone come draw it on the board)?