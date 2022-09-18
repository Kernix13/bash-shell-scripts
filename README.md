# Intro Shell Script Tutorial by Brad Traversy

The following is simple and basic shell scripts. Just getting introduced to the subject.

> ./myscript.sh

```sh
# lists files and directories within a directory
ls
# create file
touch filename.ext
# open code editor
code .
# make file executable, prevent "Permissions Denied" error
chmod +x filename.ext
# Run your file
./myscript.sh
```

- `chmod` = change mode
- `+x` = add executable permission
- in the file add a declaration of the dialect we are using (Bash)

```sh
# find where bash is
which bash
# /usr/bin/bash
```

- go to the top of your file and add a sh-bang (`#!`) and the location of bash

**Variables**:

- Variables should be UPPERCASE - you can use letters, numbers and underscores
- user input: `read -p "Enter your name: ` where `read` is user input, `-p` is to prompt the user

**Conditionals**:

- Conditionals - you need a space before and after the brackets and end with if backwards `fi`

```sh
# IF statement
if [ "VAR" == "something" ]
then
  echo "Something"
fi
```

```sh
# IF ELSE statement
if [ "VAR" == "something" ]
then
  echo "Something"
else
  echo "Something else"
fi
```

```sh
# ELSE IF statement (elif)
# Else-If Statement
if [ "$NAME" == "Jim" ]
then
  echo "Your name is Jim"
elif [ "$NAME" == "Kernix" ]
then
  echo "Your name is Kernix"
else
  echo "Your name is NOT Jim or Kernix"
fi
```

**Comparisons**:

| code  | meaning                     |
| :---- | :-------------------------- |
| `-eq` | is equal to                 |
| `-ne` | is NOT equal to             |
| `-gt` | is greater than             |
| `-ge` | is greater than or equal to |
| `-lt` | is less th                  |
| `-le` | is less than or equal to    |

```sh
# Comparisons
NUM1=3
NUM2=5
if [ "NUM1" -gt "$NUM2" ]
then
  echo "$NUM1 is greater than $NUM2"
else
  echo "$NUM2 is greater than $NUM1"
fi
```

**File Conditions**:

| code      | meaning                                 |
| :-------- | :-------------------------------------- |
| `-d file` | true if file is a directory             |
| `-e file` | true if file exists                     |
| `-f file` | true if provided string is a file       |
| `-g file` | true if the group[ id is set on a file] |
| `-r file` | true if the file is readable            |
| `-u`      | true if the user if is set on a file    |
| `-u`      | true if the user if is set on a file    |
| `-w`      | true if the file is writable            |
| `-x`      | true if the file is an executable       |

- File Conditions: `-f file` true if provided string is a file (better than `-e`),

```sh
FILE="test.txt"
if [ -f "$FILE" ]
then
  echo "$FILE is a file"
else
  echo "$FILE is NOT a file"
fi
# delete a file
rm test.txt
# create a directory
mkdir test.txt
```

> To clear the console you can use `clear` but I believe that is a Node.js command. Otherwise you can use `CTRL + L` or lowercase l.

**Case Statements**:

- Case Statements: see example but `;;` is to end a case check, end with `)` and `*)` is wierd - end case with case backwards - only y, Y, n or N works for me???

**Loops**:

- for loop: `for` `do` `done` | `$(ls *.txt)` where `ls` is to list and here is to list all files ending with `.txt`
- `mv` moves and renames a file(s)
- you can remove a file with `rm`: `rm new-2.txt`
- He created 3 files from the command line with `touch 1.txt 2.txt 3.txt`
- While loop: new keywords: `WHILE`, `read`, `-r`, `CURRENT_LINE`, `((VSRIABLE++))`, and `< "filename.ext"` - what is CURRENT_LINE?
- this is great to get code from a file but how can you input the lines you want? Then how can I get it programatically for a JS function?

**Functions**:

- identical to a JS Function except no `()` to call the function
- Parameters: you don't pass the params in the parentheses, you use positional parameters such as `$1`, `$2`, etc (similar to RegEx)

**Basic commands**:

- create a folder, put a file in it, write to it - you could do this in the cmd line or write a script to do it - use `>>` to write to a file - this is good for repetitive tasks

Cheat Sheets:

- [Bash Scripting Cheat Sheets](https://linuxconfig.org/bash-scripting-cheat-sheet)
- [Bash scripting cheatsheet](https://devhints.io/bash)
- [BASH Cheat Sheet](https://www.pcwdld.com/bash-cheat-sheet#wbounce-modal)
- [Linux Bash Commands Cheat Sheet](https://algodaily.com/lessons/bash-commands-cheat-sheet1)
- [Basic Bash Commands for Linux Newbies](https://www.maketecheasier.com/basic-bash-command-for-new-linux-users/)
