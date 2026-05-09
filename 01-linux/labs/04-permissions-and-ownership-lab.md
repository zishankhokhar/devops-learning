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
