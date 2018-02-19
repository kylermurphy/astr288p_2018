# astr288p_2018

Exercises from previous lecture can be found in the **exercise** directory along with solutions (where applicable).

## Some notes from last class

When logged into URSA to install Miniconda we were in a login shell as opposed to an interactive shell. A bash login shell will not run the ```.bashrc```, instead it will run ```.bash_profile```. This will be true when logged into URSA from your laptops as well. 

Miniconda added to the path directory in the ```.bashrc```, to ensure that ```.bashrc``` file is always executed we can add the following line to our ```.bash_profile```

```
. ~/.bashrc #run .bashrc after login
```

You can do this by pasting the following code into the terminal

```
echo ". ~/.bashrc #run .bashrc after login" >> .bash_profile
```

If you are still having troubles running Miniconda you can also use the public (so-called astromake) version as follows:

```
echo 'export PATH="/astromake/opt/python/miniconda3/bin/:$PATH"' >> .bashrc
```

My Miniconda should work as well:

```
echo 'export PATH="/n/ursa/A288P/krmurphy/ASTR288P/software/sublime_text_3/:$PATH"' >> .bashrc
```

*A note on remote logins:* when you are logged onto URSA you are running a terminal/shell directly on URSA and hence are using the operating system installed on URSA. For this class when remotely logged onto URSA you will be in a linux system regardless if you login from a Windows of Mac machine. 

*A note on WSL:* you may not be able to change a files permissions in WSL if you are in the Windows Files System. However if you transfer a file from the Windows Files System to a Linux File System (such as URSA) you will be able to modify a files permissions again using ```chmod```.


