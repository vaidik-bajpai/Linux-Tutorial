# Linux Basic Commands Cheat Sheet

A collection of essential Linux commands with descriptions and examples to help you understand and use them efficiently.

----------

## 1. User & System Info

### `whoami`

Prints the current logged-in user.

```bash
whoami

```

### `date`

Displays the current date and time.

```bash
date

```

----------

## 2. Output & Printing

### `echo`

Prints text or variables to the terminal.

```bash
echo "Hello, World!"

```

----------

## 3. Navigation

### `pwd`

Print Working Directory.

```bash
pwd

```

### `cd`

Change directory.

```bash
cd /home/user/Documents

```

-   `cd .` – Stay in the current directory.
    
-   `cd ..` – Go one level up.
    
-   `cd ~` – Go to the home directory.
    
-   `cd -` – Go to the previous directory.
    

----------

## 4. Listing Files

### `ls`

List files and directories.

```bash
ls

```

-   `ls -a` – Include hidden files.
    
-   `ls -la` or `ls -al` – Long listing format including hidden files.
    
-   `ls -R` – Recursive listing.
    
-   `ls -r` – Reverse order.
    
-   `ls -t` – Sort by modification time.
    

----------

## 5. File Operations

### `touch`

Creates an empty file.

```bash
touch newfile.txt

```

### `file`

Displays file type.

```bash
file newfile.txt

```

### `cat`

Concatenates and displays file content.

```bash
cat file.txt

```

### `less`

View file content one screen at a time, with scrolling and search support.

```bash
less file.txt

```

-   Use `Space` to go down a page.
    
-   Use `b` to go back a page.
    
-   Use `/search_term` to search inside the file.
    
-   Press `q` to quit viewing.
    

----------

## 6. History & Shortcuts

### `!!`

Repeats the last command.

```bash
!!

```

### `Ctrl + R`

Search command history.

### `Tab Completion`

Auto-completes commands and file names.

----------

## 7. Screen Management

### `clear`

Clears the terminal screen.

```bash
clear

```

----------

## 8. Copying Files

### `cp`

Copies files or directories.

```bash
cp source.txt destination.txt

```

-   `cp -i` – Prompt before overwrite.
    
-   `cp -r` – Copy directories recursively.
    

----------

## 9. Moving & Renaming

### `mv`

Moves or renames files and directories.

```bash
mv old.txt new.txt        # Renames a file
mv old_folder new_folder  # Renames a folder

```

-   `mv -i` – Prompt before overwrite.
    
-   `mv -b` – Backup files before overwriting.
    

----------

## 10. Creating Directories

### `mkdir`

Creates a directory.

```bash
mkdir new_folder

```

-   `mkdir -p` – Creates nested directories.
    

```bash
mkdir -p parent/child/grandchild

```

----------

## 11. Removing Files/Dirs

### `rm`

Removes files.

```bash
rm file.txt

```

-   `rm -f` – Force remove.
    
-   `rm -i` – Prompt before removal.
    
-   `rm -r` – Recursive remove (directories).
    

### `rmdir`

Removes empty directories.

```bash
rmdir empty_folder

```

----------

## 12. Searching

### `find`

Search for files.

```bash
find /path -name "file.txt"

```

-   `find -type f` – Find files only.
    
-   `find -name` – Find by name.
    

----------

## 13. Help & Docs

### `help`

Displays help for shell built-ins.

```bash
help cd

```

### `man`

Displays manual pages.

```bash
man ls

```

### `whatis`

Gives a one-line description.

```bash
whatis ls

```

----------

## 14. Aliases

### `alias`

Create shortcuts for commands.

```bash
alias ll='ls -la'

```

### `unalias`

Remove aliases.

```bash
unalias ll

```

----------

## 15. Exit

### `exit`

Closes the terminal or logs out.

```bash
exit

```

----------