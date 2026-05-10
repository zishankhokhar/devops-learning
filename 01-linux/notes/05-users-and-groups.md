# 05 — Users and Groups

## Module 4.1 — /etc/passwd basics
Example entry from /etc/passwd:

root:*:0:0:System Administrator:/var/root:/bin/sh


### Breakdown of the /etc/passwd entry

- **username:** `root`  
  The account name.

- **password placeholder:** `*`  
  Real passwords are stored in `/etc/shadow`, not here.

- **UID:** `0`  
  UID 0 = the superuser (full system control).

- **GID:** `0`  
  Primary group ID, also the root group.

- **comment field:** `System Administrator`  
  A description or full name.

- **home directory:** `/var/root`  
  The root user’s home folder.

- **shell:** `/bin/sh`  
  The program that runs when this user logs in.
