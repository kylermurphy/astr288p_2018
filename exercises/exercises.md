# astr288p_2018 Exercises

## Exercise 2-1

If you were following along in the notes you should have created 2 files in your *~/ASTR288P/Lecture2/* directory,  *Data1.txt* and *Data2.txt*. Using the **mv** command; move these files to a new directory *~/ASTR288P/Practice/* and rename *Data2.txt -> Data3.txt*.

An excellent resource for the **mv** command can be found here, https://www.howtoforge.com/linux-mv-command/.

## Solution 2-1 
Assuming you are in the directory where *Data1.txt* and *Data2.txt* where created then the following will complete the above. 

```
mkdir ~/ASTR288P/Practice                  # create the Practice directory
mv Data1.txt ~/ASTR288P/Practice/          # move Data1.txt
mV Data2.txt ~/ASTR288P/Practice/Data3.txt # move and rename Data2.txt

```


## Excercise 2-2

Write a bash script that when run in the current directory will generate two files, *AlphaList.log* and *RevAlphaList.log*. The file *AlphaList.log* should contain the path of the current dirctory on the first line followed by a list of the files in the current directory in alphabetical order. The file *RevAlphaList.log* should contain the path of the current directory followed by a list of files in the directory in reverse alphabetical order. Both log files should also contain the permissions for each file in the directory. **NOTE**, you can name the script what ever you want but in general the names of scripts should (at least vaguely) reflect their utility. Test the script on your home directory.

The page https://www.howtoforge.com/linux-ls-command/ contains examples for the **ls** command. 

## Soultion 2-1

Pasting the code below into a text editor and savin as ex2-1.sh will complete this exercise.

```
emacs ex2-1.sh #open the file ex2-1.sh in emacs
```

Shell script code
```
#! /bin/bash

#print to screen the files being created
echo Creating AlphaList.log and RevAlphaList.log 

# pipe the outputs of pwd and ls -l to the first file
pwd > AlphaList.log
ls -l >> AlphaList.log


# pipe the ouputs of pwd and ls -l -r to the second file
pwd > RevAlphaList.log
ls -l -r >> RevAlphaList.log
```

Save the script ex2-1.sh and change the permisions so that it is exucatable.

```
chmod +x ex2-1.sh #change the shell scripts permision
./ex2-1.sh        # run the shell script, so long as it is the current directory you are in
```


## Exercise 3-1

Today we discussed *variables, aliasing, and links*. These often come in handy as quick shortcuts for more complex commands, long directories, or when you want to always have a particular option when executing a command. You can create permanent *variables, alias', and links* by adding them to your startup file/script, **.bashrc** for the **bash** shell (note these start up files/script vary for different shells).

Using an editor of your choice create a **.bashrc** startup file (note the *required* **.** in the file name). Add the following to your **.bashrc**

1. The remove command **rm** does not prompt when removing files. Add an alias to the **.bashrc** such that **rm** will always prompt whether or not you want to delete the file. *Hint* check the **rm** manual for list of options for the command.
1. We installed the Sublime Text editor in class today. Add the location of the executable to path environment in the **.bashrc** file. What will this allow you to do? 
1. The file _'bashrc_example.sh'_ is located in the top directory of the Astr288p_2018 git hub repository. Copy and paste the contents of this file into your **.bashrc**. Save the file and close and reopen your terminal. What has changed? Review the new code in your **.bashrc** file, can you figure out what each line does?  

```
# Opening an editor with an untitled file name
./Astr288p/software/sublime/sublime_text_3/sublime_text

# Opening an editor with a new file
./Astr288p/software/sublime/sublime_text_3/sublime_text new.txt

# Or since your .bashrc does not exist yet
./Astr288p/software/sublime/sublime_text_3/sublime_text .bashrc

# Opening an existing file when in the directory of the file

./Astr288p/software/sublime/sublime_text_3/sublime_text bashrc_example.sh

# to keep your shell active after opening a file
./Astr288p/software/sublime/sublime_text_3/sublime_text .bashrc &

# if you forget the '&' at the end of the command you can use
ctrl-z #suspends current process
bg     #runs the last process in the background

# when complete run enabling your .bashrc file to run from 
#  a login terminal
echo . ~/.bashrc >> .bash_profile
```

**NOTE** the *case* and *if* statements in the **.bashrc** file. These are control flow statements which we will discuss in the next lecture. Can you figure out what they do? 

The **PS1** variable is your command propmpt variable in the terminal (set now as **-bash-4.1$**). The code in the **.bashrc** file modifies the command prompt so that you can make it more *user friendly*. To get color uncomment the variable *force_color_propmpt*.  

The following websites give detailed overviews of how to modify the PS1 variable so that you can desing your own prompt.

- https://www.howtogeek.com/307701/how-to-customize-and-colorize-your-bash-prompt/ 
- http://ezprompt.net/
- https://wiki.archlinux.org/index.php/Bash/Prompt_customization#See_also
- https://misc.flogisoft.com/bash/tip_colors_and_formatting


## Solution 3-1
The **-i** command will prompt to remove all files and similarly the **-I** command will prompt when removing more then three files or when removing recursively (e.g., all files within a directory). The two alias' below would work. This helpful so that you don't accidently delete something. Note the **-i** and **-I** can be negated with **-f** when you are absoulutely certain you want something removed. 

```
alias "rm=rm -i"
alisa "rm=rm -I"
```

You can add the location of **sublime_text** to your path in the **.bashrc** file multiple ways. From the command the code below will add the required text to the end of **.bashrc**

```
echo "export PATH=~/ASTR288P/software/sublime_text_3/:$PATH" >> ~/.bashrc
```

Alternatively you could open an editor and add the following command to the **.bashrc** file

```
export PATH="~/ASTR288P/software/sublime_text_3/:$PATH"
```

## Exercise 3-2
Copying files is an important task for moving files between directories but also for moving files between remote systems. For instance, **scp** can be used to move files from your machine to a directory on **URSA**. This is ideal for submitting homework if you don't have access to the computer lab.

Review the article on [**scp**](http://www.binarytides.com/linux-scp-command/) as it will be usefull throughout the course. 

