# Command Line Crash Course For Beginners | Terminal Commands

> Sep 14, 2022

His [YouTube Video: Command Line Crash Course For Beginners | Terminal Commands](https://youtu.be/uwAqEzhyjtw)

## The Basics

- Terms: comman line, terminal, shell, ...

Reasons to learn the command line:

1. greater control
1. Speed and efficiency
1. To access remote servers (SSH, headless OS)
1. Command line tools (NPM, GIT, YARN, SASS, Bundlers)
1. Getting Hired

Terminal vs Command Line vs Shell

- Command Line is Windows-centric, Terminal is MAc/Lnux-centric
- **Terminal**: a tool to type and execute commands. You can install 3rd-party terminal programs
- **Command Line/Prompt**: the interface of the terminal (cmd)
- **Shell**: a programs that reads the input and displays output, the programs that the terminal runs. Different shells can have different capabilities.
- **Bash** - is the most common shell program. ZSH is another one
- Windows: CMD.EXE -> also Powershell - both have some different commands than Bash or ZSH.
- **Git Bash**: is a unix-based solution for Windows, get it at [git Downloads](https://git-scm.com/downloads)

## The Commands

I forked his gist called [Common Terminal Commands](https://gist.github.com/Kernix13/ca27967c11eb8ee21537994489b0d009).

He is not covering commands dealing with permissions, groups, users, ...

### Keyboard shortcuts

- skip `CTRL+D`
- `CTRL+R` to search which will show the last command that matches your string
- `CTRL+L` is better than typing `clear`
- `CTRL+C` to cancel
- up/down arrow keys are nice
- `TAB` to auto-complete a command - doesn't work for me in Git Cash
- `CTRL + +` or `CTRL + -` to zoom in and out of the terminal (Git Bash)

### Basic Commands

1. `man`: for manual - used to get information on other cmds - e.g. `man ls` - not working for me - instead use `[command] --help` - that worked -
1. `help` worked
1. use `q` for quit to exit out of a screen
1. `whoami` to see the user you are logged in as
1. `date` to get the date and time
1. `code .` opens your default text editor into the folder you ran that command, or into a specific folder like `code src/`

### Common Commands for navigation

1. `pwd` prints the working directory - also `~` represents your home directory as well
1. `ls` - lists the contents of a folder/directory of the curent pwd - you can check a specific folder with `ls src/` - ls options:
   1. `ls -a` will show hidden files that don't show with just `ls` |
   1. `ls -l`, the long listing, shows extra information on the files
   1. combining options like `ls -a -l` or `ls -al`
1. `cd` to go to home directory
   1. `cd [directory]` to change to a different folder
   1. `cd ..` or `cd ../` to go back a folder
   1. `cd /` to go to the root of your machine
   1. `cd -` takes you the last folder you were in
1. `start [fileName/dirname/url]` to open the file (in Windows), markdown will open in notepad, folders in Windows Explorer, URL's in your default browser

### Creating and modifying files and folders

1. `mkdir [dirname]` - make directory, creates a folder
1. `touch fileName.ext` to create a file, can add multiple filenames
   1. `touch file-{01..10}.txt` to create 10 files
1. `rm [fileName.ext]` to delete/remove a file of folder
   1. `rm -i` to prompt you to make sure you want to delete it
   1. `rm -r [dirname]` to delete a folder
   1. `em -rf [dirname]` using `f` flag to force the deletion when you have files in the folder

### Copying and moving files and folders

1. `cp [filename.ext] [dirname/fielname.ext]` to copy a file into [dirname/filename.ext]
1. `mv [filename.ext] [dirname/fielname.ext]` to move a file into the folder
1. `mv [dirname] [difffirname]` to rename a folder, e.g. `mv source src` to rename the source folder to src

### Contents of files

You can add content into a file from the terminal

1. `cat [filename]` the concatenate cmd, to **_read_** the contents of a file - good to "peek" into a file without having to open it
   1. `cat -n [filename]` to show the line numbers
1. `cat > [filename]` to **_write_** to a file and it will go onto the next line where you can type then `CTRL+D` to get out of that mode
   1. `cat >> [filename]` to append content to the file
1. `less [filename]` the less cmd, also reads/shows the contents but allows you to scroll with arrow keys or page up/down - hit `q` to exit
1. `head [filename]` to see only parts of a file from the top (1st 10 lines by default)
   1. `head -n 5 [filename]` to specify the number of lines
1. `tail [filename]` to see only parts of a file from the bottom, or `tail -n 5 [filename]`

### Terminal based text editors

VIM, nano,where nano is good to know - when dealing with servers (headless OS's) you can't open a regular text editor

1. `nano [filename]` to open a file for editing and use `CTRL+X` to exit, if you made changes you will be asked if you want to save the changes (y/n)
1. `echo [output]` to display text with output in double-quotes
   1. `echo [output] > [filename]` to echo to a file, not sure if the filename doesn't exist if it is alos created

### Searching for strings in a file

1. `grep [searchterm] [filename]` to search for a term (in double-quotes if there are spaces in your phrase) inside a file, it returns the line # where/if it is found - you can also use RegEx
1. `find . -name "*.sh"` finds the locations of files and folders based on your search conditions, where `.` means the current directory, `-name` means by name
   1. `find . -empty` to find empty files
   1. `find [dirname] [filename] -delete` to find and delete a file, e.g. `find . -name test* -delete`

### Piping or redirection

Transferring output to some other destination which we have done with some of the `cat` and `echo` cmds. You use the `>` symbol - didn't seem to understand the point of his example.

### Create a symlink

A symlink (symbolic link) is a file whose purpose is to point to a file or directory by specifying a path - basically a shortcut. Use the `ln` cmd.

1. `ln -s [filename or dirname] [symlinkname]`, where filename or dirname will be the symlink e.g. `ln -s ~/Downloads dls` - if you do a cd into that and then ls it will show you everything in it but it wasn't copied,
1. `rm dls` to remove the symlink
1. `mklink` to make a symlink in Windows if you are not using Git Bash

### File compression and creating tar balls

A **tar** is a computer file format that combines multiple files. Tarball is a jargon term for a TAR archive - a group of files collected together as one; is a computer software utility for collecting many files into one archive file, often referred to as a tarball, for distribution or backup purposes...kind of like a `zip` file.

1. `tar -czvf [tarballfilename.tar.gz] [filename or dirname]` to compress a folder where `c` is to create,
1. `tar -tzvf [filename.tar.gz]` to peek to see what is inside a tarball
1. to extract/unpack what is in a tarball, make a new directory, cd into it, then `tar -xzvf [filepath/filename.tar.gz]`

### History

1. `history` to list all your cmds
   1. `!ID#` to run that cmd again
