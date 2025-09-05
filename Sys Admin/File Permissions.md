## Understanding `ls -l` Output
```
$ ls -l /etc/passwd
-rw-r--r-- 1 root root 2384 Dec 15 10:30 /etc/passwd
# ↑         ↑  ↑   ↑    ↑         ↑
# |         |  |   |    |        Timestamp
# |         |  |   |    File Size
# |         |  |   Group
# |         |  Owner
# |         Link Count
# Permission String
```

### Decoding the Permission String: `-rwxr-xr--`

The 10-character string breaks down as:
```
- r w x r - x r - -
│ │ │ │ │ │ │ │ │ │
│ │ │ │ │ │ │ │ │ └─ Others: Read
│ │ │ │ │ │ │ │ └── Others: Write
│ │ │ │ │ │ │ └──── Others: Execute
│ │ │ │ │ │ └───── Group: Execute
│ │ │ │ │ └────── Group: Write
│ │ │ │ └─────── Group: Read
│ │ │ └───────── Owner: Execute
│ │ └─────────── Owner: Write
│ └───────────── Owner: Read
└─────────────── File Type (- = file, d = directory, l = symlink)
```


## File Permission Commands

### 1. `chmod` - Change File Mode

**Syntax:** `chmod [options] mode file`

#### Symbolic Method (Easy to Read)

```
bash

# Add execute permission for owner
chmod u+x script.sh

# Remove write permission for group and others
chmod go-w sensitive-file.txt

# Set read/write for owner, read for group, none for others
chmod u=rw,g=r,o= file.txt

# Recursively add execute for directories only
find /path/to/dir -type d -exec chmod +x {} \;
```
#### Octal/Numeric Method (Preferred for Scripts)

```
bash

# Common permission sets:
chmod 644 file.txt    # rw-r--r-- (regular files)
chmod 755 script.sh   # rwxr-xr-x (executables)
chmod 600 key.pem     # rw------- (private keys)
chmod 750 directory/  # rwxr-x--- (group accessible dir)
chmod 777 avoid_this  # ❌ DANGEROUS - avoid in production!

# Recursive changes
chmod -R 755 /webroot/      # Apply to files AND directories (careful!)
find /webroot/ -type f -exec chmod 644 {} \;  # Files only
find /webroot/ -type d -exec chmod 755 {} \;  # Directories only
```
### 2. `chown` - Change Owner

**Syntax:** `chown [options] owner[:group] file`

```
bash

# Change owner only
chown username file.txt

# Change owner and group
chown username:groupname file.txt

# Change group only
chown :groupname file.txt

# Recursive ownership change
chown -R www-data:www-data /var/www/html/

# Reference another file's ownership
chown --reference=source.txt target.txt
```

### 3. `chgrp` - Change Group

**Syntax:** `chgrp [options] group file`

```
bash

# Change file group
chgrp developers script.sh

# Recursive group change
chgrp -R www-data /var/www/

# Reference another file's group
chgrp --reference=source.txt target.txt
```
## Special Permissions

### SetUID (Set User ID)
```
bash

# Sets the executable to run as file owner regardless of who executes it
chmod u+s /usr/bin/passwd
# Shows as: -rwsr-xr-x instead of -rwxr-xr-x

# Numeric: Add 4000 to permissions
chmod 4755 /usr/bin/special-program
```
### SetGID (Set Group ID)

```
bash

# For files: run with file's group privileges
# For directories: new files inherit directory's group
chmod g+s /shared-directory/
# Shows as: drwxr-sr-x instead of drwxr-xr-x

# Numeric: Add 2000 to permissions
chmod 2775 /shared-directory/
```

### Sticky Bit

```
bash

# On directories: prevents users from deleting others' files
chmod +t /tmp/
# Shows as: drwxrwxrwt instead of drwxrwxrwx

# Numeric: Add 1000 to permissions
chmod 1777 /tmp/
```
## Quick Identification Cheat Sheet

### Common Permission Patterns to Recognize Instantly

```
bash

# SECURE PATTERNS:
-rw------- (600)  # Private user files (ssh keys, configs)
-rw-r----- (640)  # Group-readable config files  
-rwx------ (700)  # Private executables
-rwxr-x--- (750)  # Group-accessible executables
-rwxr-xr-x (755)  # Public executables
drwxr-x--- (750)  # Secure directories
drwx------ (700)  # Private directories
```

# WARNING PATTERNS:
```
-rw-rw-rw- (666)  # World-writable file - SECURITY RISK!
drwxrwxrwx (777)  # World-writable directory - DANGEROUS!
-rwxrwxrwx (777)  # World-executable file - DANGER!
-rwsr-xr-x (4755) # SetUID executable - validate necessity!
-rwxr-sr-x (2755) # SetGID executable - validate necessity!
```

### Quick Audit Commands

```
bash

# Find world-writable files (SECURITY RISK!)
find / -xdev -type f -perm -0002 -ls

# Find SetUID files (should be minimal)
find / -xdev -type f -perm -4000 -ls

# Find SetGID files
find / -xdev -type f -perm -2000 -ls

# Find files owned by specific user
find / -xdev -user username -ls

# Find files with no owner (orphaned files)
find / -xdev -nouser -ls

# Find executable files in home directories (potential malware)
find /home -xdev -type f -perm -100 -ls
```
## Advanced Permission Management

### Access Control Lists (ACLs)

```
bash

# View ACLs
getfacl file.txt

# Set ACL for specific user
setfacl -m u:username:rwx file.txt

# Set ACL for specific group  
setfacl -m g:groupname:rx file.txt

# Set default ACL for directory (inherited by new files)
setfacl -d -m u:username:rwx directory/

# Remove specific ACL
setfacl -x u:username file.txt

# Remove all ACLs
setfacl -b file.txt
```

### umask - Default Permission Mask

```
bash

# Show current umask
umask  # Typical output: 0022

# Set umask (prevents permissions rather than granting)
umask 0027  # Results: files 640, directories 750
umask 0077  # Results: files 600, directories 700
```
```
# Calculate final permissions: 
# File: 666 - umask, Directory: 777 - umask
# umask 022 → files: 644 (666-022), directories: 755 (777-022)
```

## Best Practices for SysAdmins

1. **Principle of Least Privilege**: Grant minimum necessary permissions
    
2. **Regular Audits**: Schedule permission audits with find commands above
    
3. **Document Changes**: Log permission modifications for troubleshooting
    
4. **Use Groups Wisely**: Manage access through groups rather than individual users
    
5. **Avoid 777**: Never use chmod 777 - fix the underlying issue instead
    
6. **SetUID/SetGID Minimization**: These are security risks - use sparingly
    
7. **ACLs over Complex Groups**: Use ACLs for complex permission scenarios
    

## Gotchas and Common Mistakes

1. **`chmod -R` applies to both files and directories** - often you want different permissions for each
    
2. **SetUID scripts are a security risk** and often disabled on modern systems
    
3. **Permissions on symlinks** - you change permissions on the target, not the link
    
4. **NFS and ACLs** - some network filesystems have limited ACL support
    
5. **Default umask varies** by distribution and user configuration



## Quick Reference Table

|Permission|Octal|Symbolic|Typical Use|
|---|---|---|---|
|Read only|4|r--|Config files|
|Write only|2|-w-|Log directories|
|Execute only|1|--x|Scripts, programs|
|Read+Write|6|rw-|Data files|
|Read+Execute|5|r-x|Programs, scripts|
|Write+Execute|3|-wx|Avoid this combination|
|Read+Write+Execute|7|rwx|Programs, directories|

# Linux File Permission Flags: Complete Reference Guide

## Understanding the Permission Syntax

Linux file permissions use a specific set of letters that each have precise meanings. Here's the complete breakdown:

## The Basic Permission Letters

### 1. **User Classes** (Who the permission applies to)

- `u` = **User** (owner of the file)
    
- `g` = **Group** (members of the file's group)
    
- `o` = **Others** (everyone else)
    
- `a` = **All** (equivalent to ugo - user, group, and others)
    

### 2. **Permission Types** (What can be done)

- `r` = **Read** - view/file contents/list directory
    
- `w` = **Write** - modify file/delete or create files in directory
    
- `x` = **Execute** - run program/enter directory
    
- `s` = **SetID** - special execution permissions
    
- `t` = **Sticky** - restricted deletion flag
    

### 3. **Operators** (What to do with the permission)

- `+` = **Add** the permission
    
- `-` = **Remove** the permission
    
- `=` = **Set** exactly these permissions (overwrite existing)
    

## Complete Symbolic Notation Examples

### Basic Permission Management

```
bash

# Add single permission
chmod u+x script.sh      # Add execute permission for owner
chmod g-w file.txt       # Remove write permission for group
chmod o+r document.pdf   # Add read permission for others

# Multiple permissions for single class
chmod u+rw file.txt      # Add read and write for owner
chmod g-rwx directory/   # Remove all permissions from group

# Multiple classes, single permission
chmod ug+x program       # Add execute for both user and group
chmod go-w sensitive.txt # Remove write for group and others

# Using 'all' selector
chmod a+r file.txt       # Add read permission for everyone
chmod a-x program        # Remove execute permission from everyone
```
### Setting Exact Permissions

```
bash

# Set specific permissions (overwrites existing)
chmod u=rwx script.sh    # Set user to read, write, execute
chmod g=rx document      # Set group to read and execute only
chmod o= file.txt        # Set others to no permissions

# Multiple classes with exact permissions
chmod ug=rw,o= data.txt  # User and group: read/write, others: none

### Special Permission Flags

bash

# SetUID (runs as file owner)
chmod u+s /usr/bin/passwd    # Set SetUID bit
chmod u-s /usr/bin/program   # Remove SetUID bit

# SetGID (runs with file's group privileges)
chmod g+s /usr/local/bin/app # Set SetGID bit
chmod g-s /usr/bin/tool      # Remove SetGID bit

# Sticky bit (restrict file deletion in directories)
chmod +t /shared/tmp         # Set sticky bit
chmod -t /shared/tmp         # Remove sticky bit

# Combination with regular permissions
chmod u=rwxs,g=rx,o= program # SetUID with specific permissions
chmod g=rwxs,o=rx directory/ # SetGID with specific permissions
```

## Octal vs Symbolic Notation Comparison

### Symbolic Notation (Letters)

```
bash

# These all do the same thing:
chmod u=rwx,g=rx,o= file.txt
chmod 750 file.txt

# Complex changes are easier with symbolic:
chmod go-wx file.txt         # Remove write/execute from group/others
chmod a+r file.txt           # Add read for everyone
chmod u+x,g-x script.sh      # Add execute for user, remove for group
```

### Octal Notation (Numbers)

```
bash

# Common permission sets:
chmod 644 file.txt    # rw-r--r-- (u=rw,g=r,o=r)
chmod 755 script.sh   # rwxr-xr-x (u=rwx,g=rx,o=rx)
chmod 600 key.pem     # rw------- (u=rw,g=,o=)
chmod 750 directory/  # rwxr-x--- (u=rwx,g=rx,o=)

# With special permissions:
chmod 4755 program    # rwsr-xr-x (SetUID + 755)
chmod 2755 sharedir/  # rwxr-sr-x (SetGID + 755)
chmod 1777 tmp/       # rwxrwxrwt (Sticky + 777)
```
## Advanced Symbolic Notation

### Reference-Based Permissions

```
bash

# Copy permissions from one file to another
chmod --reference=source.txt target.txt

# Set permissions based on mask
chmod =rwx file.txt          # Set all classes to rwx (777)
chmod = file.txt             # Remove all permissions (000)
```
### Recursive Permission Changes

```
bash

# Recursive with symbolic notation
chmod -R u+rwX /data/        # Capital X: execute only if directory or already executable
chmod -R go-w /webroot/      # Remove write permission from group/others recursively
```
# Selective recursive changes (safer)
```
find /path/ -type f -exec chmod 644 {} \;    # Files only
find /path/ -type d -exec chmod 755 {} \;    # Directories only
```

## Permission Interpretation Table

|Symbol|Meaning|On Files|On Directories|
|---|---|---|---|
|`r`|Read|View content|List contents|
|`w`|Write|Modify content|Create/delete files|
|`x`|Execute|Run as program|Enter (cd into) directory|
|`s`|SetID|Run as owner/group|Files inherit directory's group|
|`t`|Sticky|(Rarely used)|Restrict file deletion to owner|
|`-`|No permission|No access|No access|

## Common Permission Scenarios

### Web Server Permissions

```
bash

# Secure web directory (user: developer, group: www-data)
chown -R developer:www-data /var/www/html/
find /var/www/html/ -type f -exec chmod 640 {} \;    # Files: rw-r-----
find /var/www/html/ -type d -exec chmod 2750 {} \;   # Directories: rwxr-s--- (SetGID)
chmod g+x /var/www/html/                             # Ensure group can enter directory
```
### Shared Group Directory

```
bash

# Collaborative directory for 'developers' group
chown :developers /shared/project/
chmod 2775 /shared/project/          # SetGID: new files inherit group
find /shared/project/ -type f -exec chmod 664 {} \;   # Files: rw-rw-r--
find /shared/project/ -type d -exec chmod 2775 {} \;  # Directories: rwxrwsr-x
```

### Private User Files

```
bash

# Secure home directory
chmod 700 ~/                          # Private home
chmod 600 ~/.ssh/id_rsa               # Private SSH key
chmod 644 ~/.ssh/id_rsa.pub           # Public SSH key (readable)
chmod 755 ~/public_html/              # Web directory (if needed)
```

## Quick Reference Cheat Sheet

### Symbolic Notation Patterns

```
bash

# Basic syntax:
chmod [who][operator][permissions] file

# Examples:
chmod u+rx file      # User +read +execute
chmod go-w file      # Group & others -write  
chmod a=r file       # All =read only
chmod u=rwx,g=rx,o= file # Specific permissions per class
```
### Common Combinations

```
bash

# Make executable:
chmod +x script.sh           # Add execute for all (if umask allows)
chmod u+x script.sh          # Add execute for owner only

# Make private:
chmod go= file.txt           # Remove all group/other permissions
chmod go-rwx sensitive.data  # Same as above

# Make group-readable:
chmod g+r file.txt           # Add group read
chmod g+rw shared.txt        # Add group read+write

# Make world-readable (use cautiously):
chmod o+r public.txt         # Add others read
chmod a+r published.pdf      # Add read for everyone
```

### Special Flag Usage

```
bash

# SetUID/SetGID best practices:
chmod u+s,go= /usr/bin/su    # Secure SetUID binary
chmod g+s,o= /shared/team/   # SetGID for collaborative directory

# Sticky bit for shared temp:
chmod a+rwx,+t /shared/tmp/  # Full access but can't delete others' files
```
## Key Takeaways

1. **Symbolic notation** is more flexible for making incremental changes
    
2. **Octal notation** is better for setting exact permission states
    
3. **Understand the difference** between `x` and `X` (capital X only adds execute if it makes sense)
    
4. **Special permissions** (s, t) have security implications - use carefully
    
5. **Test permission changes** in a safe environment before applying to production
