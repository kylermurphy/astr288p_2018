# Windows Subsystem for Linux (WSL)


- Run a Linux environment, including, command line tools and utilites (Bash and scripting), and applications (git) directly from Windows. 
- Doesn't have the overhead of a virtual machine
- Requires **Windows 10 Anniversary** update or later (build number 1607) 

The notes below follow the Windows 10 WSL Installation Guide: 
https://docs.microsoft.com/en-us/windows/wsl/install-win10

Additional WSL resources can be found at:
- Windows developer blog, https://blogs.msdn.microsoft.com/wsl/
- Fun with WSL, https://blogs.windows.com/buildingapps/2016/07/22/fun-with-the-windows-subsystem-for-linux/#B5qbkdEfrHJIipXc.97
- Anaconda and Python on WSL (WSL and Python setup, *we will cover this in future lectures*), https://www.scivision.co/anaconda-python-with-windows-subsystem-for-linux/, and more at https://www.scivision.co/blog
- Windows for Data Science (similar to the above): https://blogs.windows.com/buildingapps/2016/07/22/fun-with-the-windows-subsystem-for-linux/#B5qbkdEfrHJIipXc.97


## 1. Enable WSL

Open PowerShell (Windows version of a Shell/Terminal) as an Administrator (this may take a few minutes). 

**-> Start -> "Windows Power Shell" -> <Right Click> ->Run as Adminstrator**

```
Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux
```
Restart when prompted.

## 2. Find Your Windows Build

**-> Start -> Settings -> System -> About ->** *OS Build*

If your build is 16215 or later, follow the instructions in sections 3. 

If your build is earlier then 16215, follow the instruction in section 4.  


## 3. Fall Creators Update and Later 

### Windows build 16215 and later
- Open Microsoft Store 
**-> Start -> "Microsoft Store"**
- Search *Linux* and choose a distribution (OpenSUSE, SLES, Ubuntu)
- I recommend Ubuntu as it is popular and has significant resources for help. 
- Select **Get** or **Install** and choose where you want the app to be saved (likely your main disk, C).
- Select **Launch** to install the distribution after downloading.
- Create a UNIX username and password. **Be sure to remember you password as you will need this to update and install new features/programs.**


## 4. Earlier Windows 10 builds 

### Pre 16215 build

- Turn on *Developer Mode* for windows. This will give you access to the linux subsytem.
**-> Settings -> Update and Security -> For Developers ->** *Developer Mode*
- Open a command propmpt and run **bash**. This will download and install Ubuntu onto your system. A "Bash on Ubuntu on Windows" shortcut will be added to the start menu. 
**-> Start -> "CMD"**
```
bash
```
- Launch Ubuntu either through the command prompt with **bash** or through the start menu shortcut. 
- When you first launch Ubuntu you will need to set up a UNIX username and password. **Be sure to remember you password as you will need this to update and install new features/programs.**
- Following the setup you can update Ubuntu to the latest distribution using:
```
apt-get update  # you may need to prepend the command with sudo
apt-get upgrade # which runs the command as 'root' or with 'adminstrative privileges' 
```

# THE LINUX FILE SYSTEM

**Never edit, create, or modify files within the linux file system in WSL with a windows app!**

This can lead to a corruption of data and may require you to uninstall and reinstall the linux environment. This is because Linux and Windows handle file permissions differently (https://blogs.msdn.microsoft.com/commandline/2016/11/17/do-not-change-linux-files-using-windows-apps-and-tools/).

If you want to work on files within both the Windows and Linux environments, store those files in the **Windows** file system. 

In your terminal the windows file system can be accessed via
```
cd /mnt/c/           # This will take you to your C drive on windows
cd /mnt/c/Users/Kyle # My home directory on windows. 
```  

For instance, for this class if you want to write a shell script for Homework 1 using an editor you've installed on Windows be sure to save the script somewhere in your Windows file system (ASTR288 in your home dirctory located on the **C:/** drive). You can then navigate to that directory in the terminal and run the script there. Similarly if you're using **git** to download lectures saving them to the Windows files system will allow you to access them with both Window and Linux applications.

Alternatively you can write the script using Vi in the terminal, save it to the linux file system and run the script from there.

**Remember**

1. DO  store files in the Windows filesystem if you want to be able to access and modify them with both Windows and Linux tools. 
2. DO NOT access, create, or modify Linux files from Windowss, apps, tools, scripts or consoles (File Explorer)

