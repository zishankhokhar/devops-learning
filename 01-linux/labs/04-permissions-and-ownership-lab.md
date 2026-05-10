## Permissions

-rw-r--r--@  1 zishan  staff  774 May  6 17:38 README.md
drwxr-xr-x@  5 zishan  staff  160 May  8 19:01 labs
drwxr-xr-x@ 10 zishan  staff  320 May  7 23:34 notes

### README.md
`-rw-r--r--@`
- Regular file  
- User: read, write  
- Group: read  
- Others: read  

### labs
`drwxr-xr-x@`
- Directory  
- User: read, write, execute  
- Group: read, execute  
- Others: read, execute  

### notes
`drwxr-xr-x@`
- Directory  
- User: read, write, execute  
- Group: read, execute  
- Others: read, execute  


## Converting symbolic to numeric permissions

- rwxr-x--- → **750**
- rw-r--r-- → **644**
- rwx------ → **700**
- rwxrwxrwx → **777**
- rw-rw---- → **660**

- 755 → rwxr-xr-x
- 644 → rw-r--r--
- 700 → rwx------
- 600 → rw-------
- 775 → rwxrwxr-x


## Output

-rw-r--r--@ 1 zishan  staff  0 May  8 20:31 testfile.txt

What this means
- -→ regular file
- rw- → user can read + write
- r-- → group can read
- r-- → others can read



### chmod Practice

#### 1. chmod 644
Command:
chmod 644 testfile.txt
Output:
User = rw, Group = r, Others = r

#### 2. chmod 600
Command:
chmod 600 testfile.txt
Output:
-rw------- 
Only you can read/write
Good for private files

#### 3. chmod 755
Command:
chmod 755 testfile.txt
Output:
-rwxr-xr-x
Meaning:
User = rwx, Group = r-x, Others = r-x

#### 4. chmod u+x
Command:
chmod u+x testfile.txt
Output:
-rwxr-xr-x
Meaning:
Adds execute permission to user

#### 5. chmod g-w
Command:
chmod g-w testfile.txt
Output:
-rwxr-xr-x
Meaning:
Removes write permission from group


### Ownership Practice

#### 4.2 Change owner of testfile.txt
Command:
sudo chown $USER testfile.txt
ls -l testfile.txt
Output:
-rwxr-xr-x@ 1 zishan  staff  0 May  8 20:31 testfile.txt
Meaning:
Changed the owner of testfile.txt to my user account (zishan). Group stayed the same. Permissions unchanged.

#### 4.3 Change group of testfile.txt
Command:
sudo chgrp staff testfile.txt
ls -l testfile.txt
Output:
-rwxr-xr-x@ 1 zishan  staff  0 May  8 20:31 testfile.txt
Meaning:
Changed the group of testfile.txt to 'staff'. Owner stayed the same. Permissions unchanged.

#### 4.4 Change owner and group of testdir
Command:
sudo chown $USER:staff testdir (did not work due to issue with zsh)
Output:
drwxr-xr-x@ 2 zishan  staff  64 May  9 17:57 testdir
Meaning:
Changed both owner and group of testdir in one command. Owner = zishan, Group = staff.


### Step 5 — Special Permissions

#### Step 5.4 — Create specialdir
Commands:
mkdir specialdir
ls -ld specialdir
Output:
drwxr-xr-x@ 2 zishan  staff  64 May  9 18:58 specialdir
Meaning:
Created a directory for testing special permissions.

#### Step 5.5 — Apply SGID to directory
Commands:
sudo chmod g+s specialdir
ls -ld specialdir
Output:
drwxr-sr-x@ 2 zishan  staff  64 May  9 18:58 specialdir
Meaning:
Notice the s in the group section.
SGID applied. New files inherit the directory's group (staff).

#### Step 5.6 — Apply Sticky Bit
Commands:
sudo chmod +t specialdir
ls -ld specialdir
Output:
drwxr-sr-t@ 2 zishan  staff  64 May  9 18:58 specialdir
Meaning:
Sticky bit applied. Users cannot delete each other's files inside this directory.

### Step 6 — Testing SGID and Sticky Bit

#### Step 6.1 — Create a file inside specialdir
Commands:
touch specialdir/file1.txt
ls -l specialdir
Output:
-rw-r--r--@ 1 zishan  staff  0 May  9 19:40 file1.txt
Meaning:
The file inherited the 'staff' group because SGID is active.

#### Step 6.2 — Verify directory permissions
Commands:
ls -ld specialdir
Output:
drwxr-sr-t@ 3 zishan  staff  96 May  9 19:40 specialdir
Meaning:
Directory shows 's' (SGID) and 't' (Sticky Bit), confirming both are active.

#### Step 6.3 — Sticky Bit behaviour
Explanation:
Sticky Bit prevents users from deleting files they do not own. Only the file owner or root can delete files inside a sticky directory.

### Step 7 — Final Summary

#### What I Learned

- I learned how to read and interpret Linux file permissions using symbolic (rwx) and numeric (755) formats.
- I practiced converting between numeric and symbolic permissions and understood how each digit maps to user, group, and others.
- I used `chmod` to modify permissions, including:
  - numeric mode (e.g., 644, 755)
  - symbolic mode (e.g., u+x, g-w)
- I learned how to change file and directory ownership using:
  - `chown` (change owner)
  - `chgrp` (change group)
  - `chown user:group` (change both at once)
- I learned what SUID, SGID, and the Sticky Bit do:
  - SUID: run as file owner
  - SGID: inherit group on new files
  - Sticky Bit: prevent users from deleting each other’s files
- I tested SGID and Sticky Bit by creating files inside a directory and observing inherited group and restricted deletion behavior.

#### Why This Matters

- These concepts are essential for DevOps, system administration, CI/CD pipelines, Docker, Kubernetes, and secure deployments.
- Understanding permissions prevents security issues, broken deployments, and access problems.
- Ownership and special permissions are used constantly in real production environments.

#### Cleanup (Optional)

Commands:
rm -rf testfile.txt testdir specialdir
