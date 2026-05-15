# Lab: Users and Groups

## Objective
Understand how Linux stores and manages users and groups.

## Commands Used
cat /etc/passwd

## Output
root:*:0:0:System Administrator:/var/root:/bin/sh
### Breakdown of the entry
username: root  
password placeholder: *  
UID: 0  
GID: 0  
comment: System Administrator  
home directory: /var/root  
shell: /bin/sh

---

## Module 4.2 — /etc/group

### Output
staff:*:20:root
### Breakdown of the entry

group name: staff  
password placeholder: *  

GID: 20  
members: root

---

## Module 4.3 — Creating Users and Groups

### Commands Used
sudo dscl . -create /Groups/devops
sudo dscl . -create /Groups/devops PrimaryGroupID 501
sudo dscl . -create /Users/devuser
sudo dscl . -create /Users/devuser UserShell /bin/zsh
sudo dscl . -create /Users/devuser RealName "Dev User"
sudo dscl . -create /Users/devuser UniqueID 502
sudo dscl . -create /Users/devuser PrimaryGroupID 501
sudo dscl . -create /Users/devuser NFSHomeDirectory /Users/devuser
sudo mkdir /Users/devuser
sudo chown devuser:devops /Users/devuser
sudo passwd devuser

### Output
uid=502(devuser) gid=501(devops) groups=501(devops),12(everyone),61(localaccounts),701(com.apple.sharepoint.group.1),100(_lpoperator)

### Meaning
Created a new group (devops), created a new user (devuser), assigned UID/GID, set shell, created home directory, and set password.


### Adding user to extra groups

Command:
sudo dseditgroup -o edit -a devuser -t user staff

Output:
uid=502(devuser) gid=501(devops) groups=501(devops),12(everyone),20(staff),61(localaccounts),701(com.apple.sharepoint.group.1),100(_lpoperator)

Meaning:
Added devuser to the staff group as a secondary group.


### Removing user from group

Command:
sudo dseditgroup -o edit -d devuser -t user staff

Output:
uid=502(devuser) gid=501(devops) groups=501(devops),12(everyone),20(staff),61(localaccounts),701(com.apple.sharepoint.group.1),100(_lpoperator)

Meaning:
Removed devuser from the staff group.

---

### Deleting the user

Commands:
sudo dscl . -delete /Users/devuser
sudo rm -rf /Users/devuser

Output:
id: devuser: no such user

Meaning:
Deleted the user and removed their home directory.

---

### Deleting the group

Command:
sudo dscl . -delete /Groups/devops

Output:
(dscl error showing group not found)

Meaning:
Group successfully deleted.



## Challenges
(you will fill this in if anything goes wrong)

## What I Learned
- Created a group using: dscl . -create /Groups/devops
- Assigned a GID using: dscl . -create /Groups/devops PrimaryGroupID 501
- Created a user account using multiple dscl -create commands
- Set user shell, real name, UID, GID, and home directory with dscl attributes
- Created the user’s home directory manually with mkdir
- Set directory ownership using: chown devuser:devops /Users/devuser
- Set a user password using: passwd devuser
- Added a user to a group using: dseditgroup -o edit -a devuser -t user staff
- Removed a user from a group using: dseditgroup -o edit -d devuser -t user staff
- Deleted a user using: dscl . -delete /Users/devuser
- Deleted a group using: dscl . -delete /Groups/devops
- Verified all changes using: id devuser and dscl . -read

---

## Module 4.4 — /etc/sudoers

### Commands Used
sudo visudo
sudo -l
sudo usermod -aG sudo username
sudo deluser username sudo

### Output
(put your sudo -l output here)

### Meaning
Configured sudo permissions, understood sudoers syntax, tested sudo access, and learned safe editing using visudo.

### Sudoers Permission Rules

root ALL = (ALL) ALL
%admin ALL = (ALL) ALL

Meaning:
- root has full sudo access
- all users in the admin group have full sudo access
- admin is the macOS equivalent of the sudo group

- Opened the sudoers file safely using: sudo visudo
- Viewed and understood the Defaults section that controls environment variables
- Located the permission rules: root ALL=(ALL) ALL and %admin ALL=(ALL) ALL
- Learned that %admin is the macOS group with full sudo rights
- Understood that group rules start with % and user rules do not
- Verified sudo permissions using: sudo -l
- Learned that sudoers must never be edited with normal editors (nano/vim)
- Understood that visudo validates syntax before saving to prevent breaking sudo
- Learned how to give sudo access by adding a user to the admin/sudo group
- Learned how to remove sudo access by removing the user from the group or deleting their rule


## Challenges
(you will fill this in if anything goes wrong)

## What I Learned
(we will fill this at the end)
