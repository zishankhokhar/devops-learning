## Permissions & Ownership (Phase 3)

### Understanding Linux Permissions

Linux uses permissions to control who can read, write, or execute a file or directory.  
Each file has three types of permissions:

- read (r) — allows viewing the contents
- write (w) — allows modifying the contents
- execute (x) — allows running the file as a program or script

These permissions apply to three groups:

- user — the owner of the file
- group — users who belong to the file’s group
- others — everyone else on the system

Together, they form the standard permission structure used throughout Linux.

### Reading Permissions with `ls -l`

You can view permissions using:
ls -l


This shows a permission string like:
-rwxr-xr--


This string is split into four parts:

1. **File type**  
   - `-` = regular file  
   - `d` = directory  

2. **User permissions** (owner)  
3. **Group permissions**  
4. **Others permissions**

Example breakdown:

-rwxr-xr--
^   ^  ^
|   |  |
|   |  └── others (r--)
|   └──── group (r-x)
└──────── user (rwx)

Each group has its own r, w, x permissions, forming the full permission structure.


### Permission Numbers (Octal Representation)

Linux permissions can also be represented using numbers.  
Each permission type has a numeric value:

- **read (r) = 4**
- **write (w) = 2**
- **execute (x) = 1**

To calculate permissions for each group (user, group, others), you add the values together.

Examples:

- **7 = 4 + 2 + 1 = rwx**
- **6 = 4 + 2 = rw-**
- **5 = 4 + 1 = r-x**
- **4 = r--**
- **0 = ---**

This creates the common permission sets you see in Linux:

- **755 = rwx r-x r-x**
- **644 = rw- r-- r--**
- **700 = rwx --- ---**

These numbers are used with the `chmod` command to set permissions quickly.

### Changing Permissions with `chmod`

The `chmod` command is used to change file and directory permissions.  
You can use it in two ways:

---

#### 1. Numeric Mode (Octal)

This uses permission numbers like **755**, **644**, **700**, etc.

Examples:

- `chmod 755 file.txt` → rwx r-x r-x  
- `chmod 644 file.txt` → rw- r-- r--  
- `chmod 700 script.sh` → rwx --- ---

Numeric mode is fast and commonly used in DevOps.

---

#### 2. Symbolic Mode (Letters)

Symbolic mode uses letters to add or remove permissions:

- **u** = user  
- **g** = group  
- **o** = others  
- **a** = all  

Operators:

- **+** add permission  
- **-** remove permission  
- **=** set exact permission  

Examples:

- `chmod u+x script.sh` → add execute for user  
- `chmod g-w file.txt` → remove write for group  
- `chmod o=r file.txt` → set others to read only  
- `chmod a+rx folder` → give everyone read + execute

Symbolic mode is more descriptive and easier to understand.

---

#### Checking Your Changes

After modifying permissions, verify them with:

ls -l

This confirms whether your changes applied correctly.

### Ownership: User & Group

Every file and directory in Linux has two types of ownership:

- **User (owner)** — the person who created the file
- **Group** — a group of users who can share access

You can view ownership using:

ls -l

Example:
-rw-r--r-- 1 zishan staff 1200 May 7  report.txt


Breakdown:

- **zishan** → user (owner)
- **staff** → group

Ownership determines who gets the **user** and **group** permissions.

---

### Changing Ownership with `chown`

The `chown` command changes the **user** and/or **group** owner of a file.


#### Change the user owner:

sudo chown newuser file.txt


#### Change the group owner:

sudo chown :newgroup file.txt


#### Change both user and group:

sudo chown newuser:newgroup file.txt

Example:
sudo chown zishan:devops script.sh

This sets:

- user → zishan  
- group → devops  

---

### Changing Group Ownership with `chgrp`

`chgrp` is used when you only want to change the **group**:
sudo chgrp developers project.log


This is useful when multiple users belong to the same group and need shared access.

---

### Checking Ownership After Changes

Always verify your changes with:

ls -l
This confirms the new user and group ownership.

