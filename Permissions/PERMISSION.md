
# Understanding Linux File Permissions.

This guide breaks down Linux file permissions, ownership, special permission bits, and how to manage them using commands like `chmod`, `chown`, and `umask`.

```bash
ls -l Desktop
drwxr-xr-x. 1 goganoth goganoth 86 May 5 19:36 Linux-Tutorial

```
```
d | rwx | r-x | r-x
↑   ↑     ↑     ↑
│   │     │     └── Others' permissions
│   │     └──────── Group permissions
│   └────────────── User permissions
└────────────────── File type

```

### 🔤 File Types

-   `d` → directory
    
-   `-` → regular file
    

### 🔐 Permissions

-   `r` → read
    
-   `w` → write
    
-   `x` → execute
    
-   `-` → no permission
    

### 👤 Example Interpretation

From `drwxr-xr-x`:

-   **User (goganoth):** read, write, execute
    
-   **Group (goganoth):** read, execute
    
-   **Others:** read, execute
    

----------

## 🛠️ Modifying Permissions

### 🔡 Symbolic Method

```bash
chmod u+x myfile          # Add execute for user
chmod g-w file            # Remove write from group
chmod ug-r file           # Remove read from user and group

```

### 🔢 Numeric (Octal) Method

```markdown
 ____________________
| Permission | Value |
|------------|-------|
| Read       | 4     |
| Write      | 2     |
| Execute    | 1     |
 --------------------
```

```bash
chmod 755 file

```

-   **7 (user)** → 4+2+1 → read, write, execute
    
-   **5 (group)** → 4+1 → read, execute
    
-   **5 (others)** → 4+1 → read, execute
    

----------

## 👥 Ownership Permissions

### Change Owner

```bash
sudo chown <username> myfile

```

### Change Group

```bash
sudo chgrp <groupname> myfile

```

### Change Both

```bash
sudo chown <username>:<groupname> myfile

```

----------

## 🔧 Setting Default Permissions (umask)

```bash
umask 021

```


## 🧾 `umask` Position Meaning

| Position | Affects | Meaning                              |
|----------|---------|--------------------------------------|
| 0        | User    | Full permissions                     |
| 2        | Group   | No write permission (`2` = write)    |
| 1        | Others  | No execute permission (`1` = execute) |


> Default `umask` is usually `022`.

### 📌 Make it Persistent

Add to `~/.profile` or `~/.bashrc`:

```bash
umask 021

```

----------

## 📛 Special Permission Bits

### 📌 SetUID (`s` or `S` for **user**)

-   Lets users run a file as the file's owner.
    
-   Useful for programs needing root access (e.g. `passwd`).
    

#### Example

```bash
ls -l /usr/bin/passwd
-rwsr-xr-x. 1 root root 91760 Mar 20 05:30 /usr/bin/passwd

```

-   `s` replaces `x` when execute is **enabled**
    
-   `S` replaces `x` when execute is **disabled**
    

#### Set SetUID

```bash
chmod u+s file
chmod 4755 file

```

----------

### 📌 SetGID (`s` or `S` for **group**)

-   Files run with the group’s permissions.
    
-   On directories: new files inherit the directory's group.
    

#### Set SetGID

```bash
chmod g+s file
chmod 2755 file

```

----------

### 📌 Sticky Bit (`t` or `T` for **others**)

-   Only root or file owner can delete/rename inside a directory.
    
-   Commonly used in `/tmp`.
    

#### Set Sticky Bit

```bash
chmod +t directory
chmod 1755 directory

```

#### Example Output

```bash
drwxr-xr-t. 1 goganoth goganoth 0 May 6 14:30 check

```

----------

## 🔁 Process Permissions (UIDs)

Every process has:

-   **Real UID**: the user who launched the process
    
-   **Effective UID**: user whose permissions the process uses (via SUID)
    
-   **Saved UID**: allows switching between real and effective UID
    

### Example: `passwd`

-   Owned by root, has SetUID
    
-   When executed by user (UID 500), effective UID becomes 0 (root)
    
-   But it can only modify **that user's password**, not others', due to real UID checks
    

----------


## 🧠 Summary of Special Permission Bits

| Bit     | Numeric | Applies To | Meaning                              |
|---------|---------|-------------|--------------------------------------|
| SetUID  | 4       | User        | Run the file with the owner's privileges |
| SetGID  | 2       | Group       | Run the file with the group’s privileges or inherit group ID |
| Sticky  | 1       | Others      | Only the file's owner or root can delete/modify the file |


Combined with standard permissions:

```bash
chmod 4755 file   # SetUID + rwxr-xr-x
chmod 2755 file   # SetGID + rwxr-xr-x
chmod 1755 dir    # Sticky Bit + rwxr-xr-x

```