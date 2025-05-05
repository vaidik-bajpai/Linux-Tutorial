# Linux User and Group Management

This guide covers essential commands for managing users and groups on a Linux system, including user creation, modification, account policies, and group operations.

----------

## User Management

### Creating a New User

```bash
sudo useradd <username>

```

-   Creates a user account.
    
-   A group with the same name is created as the primary group.
    
-   A home directory is created at `/home/<username>`.
    
-   Default shell is `/bin/bash`.
    
-   Files from `/etc/skel/` are copied to the new home directory.
    
-   The account does **not** expire by default.
    
-   No password is set initially.
    

Set a password:

```bash
sudo passwd <username>

```

----------

### Viewing User Defaults

```bash
useradd -D
cat /etc/login.defs

```

Shows system-wide default settings for new user accounts.

----------

### Removing a User

```bash
sudo userdel <username>

```

-   Deletes the user but **not** their home directory or mail spool.
    

To remove the user and their files:

```bash
sudo userdel -r <username>

```

----------

### Customizing User at Creation

```bash
sudo useradd -s /bin/othershell -d /home/otherdirectory <username>

```

Options:

-   `-s`: Set custom shell.
    
-   `-d`: Set custom home directory.
    
-   `-u`: Specify a custom user ID.
    

Example:

```bash
sudo useradd -u 1100 -s /bin/zsh -d /custom/home <username>

```

----------

### Viewing User Info

-   Account details are stored in `/etc/passwd`.
    
-   Format:
    
    ```
    <username>:x:<uid>:<gid>::<home-dir>:<shell>
    
    ```
    
-   First regular user usually has UID 1000.
    

View ownership:

```bash
ls -l /home/
ls -ln /home/

```

Identify user:

```bash
id
whoami

```

----------

### Creating System Users

```bash
sudo useradd --system <sysaccount>

```

-   No home directory is created.
    
-   Typically used for daemon processes.
    

----------

## Modifying Users

Use `usermod` to change user attributes.

### Change Home Directory

```bash
sudo usermod --home /new/home --move-home <username>

```

### Change Username

```bash
sudo usermod --login <new_username> <username>

```

### Change Shell

```bash
sudo usermod --shell /bin/othershell <username>

```

----------

## Locking and Expiring Accounts

### Lock/Unlock User

```bash
sudo usermod -L <username>     # Lock
sudo usermod -U <username>     # Unlock

```

### Set Account Expiry

```bash
sudo usermod --expiredate 2025-12-18 <username>

```

-   To immediately expire an account, set a past date.
    
-   To remove expiration:
    

```bash
sudo usermod --expiredate "" <username>

```

----------

## Password Policies

Use `chage` to manage password expiry.

### Expire Password Immediately

```bash
sudo chage -d 0 <username>

```

### Unexpire Password

```bash
sudo chage -d -1 <username>

```

### Set Max Password Age

```bash
sudo chage -M 30 <username>  # Change every 30 days
sudo chage -M -1 <username>  # Never expire

```

### View Password Expiry Info

```bash
sudo chage -l <username>

```

----------

## Group Management

### Understanding Groups

-   Users can belong to one **primary** group and multiple **secondary** groups.
    
-   The **primary group** (login group) is used for file ownership and process privileges.
    

----------

### Creating and Deleting Groups

```bash
sudo groupadd <groupname>
sudo groupdel <groupname>

```

----------

### Adding/Removing Users to/from Groups

```bash
sudo gpasswd -a <username> <groupname>     # Add user
sudo gpasswd -d <username> <groupname>     # Remove user

```

----------

### Viewing Group Membership

```bash
groups <username>

```

----------

### Changing User's Primary Group

```bash
sudo usermod -g <groupname> <username>

```

-   Do **not** confuse `-g` (primary group) with `-G` (secondary groups).
    

----------

### Renaming a Group

```bash
sudo groupmod -n <new_name> <old_name>

```
