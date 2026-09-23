# Linux Fundamentals — Homework

**Name:** Aditya Vikram Singh
**Roll No.:** 24bcs10429

---

## Task 1: Soft Link & Hard Link

### Difference Between Soft Link and Hard Link

| Soft Link (Symbolic Link) | Hard Link |
|---------------------------|-----------|
| Points to the original file's path | Points directly to the file's inode |
| Can link across file systems | Cannot link across file systems |
| Can link to directories | Cannot normally link to directories |
| Breaks (dangles) if the original file is deleted | Still works if the original file is deleted |
| Created using `ln -s` | Created using `ln` |

### Commands Practiced

**Create a file**
```bash
touch file1.txt
```

**Create a soft link**
```bash
ln -s file1.txt softlink.txt
```

**Create a hard link**
```bash
ln file1.txt hardlink.txt
```

**View links (and inode numbers)**
```bash
ls -li
```

**Delete the soft link**
```bash
rm softlink.txt
```

**Delete the hard link**
```bash
rm hardlink.txt
```

**Delete the original file**
```bash
rm file1.txt
```

### Interview Q&A

**Q: What is the difference between a soft link and a hard link?**

**A:** A soft link is a pointer to the original file's path — if the original file is deleted or moved, the soft link breaks. A hard link points directly to the same inode as the original file, so the data remains accessible even if the original file name is deleted, as long as at least one hard link still exists.

---

## Task 2: `adduser` vs `useradd`

### Difference

| `adduser` | `useradd` |
|-----------|-----------|
| User-friendly, interactive command | Low-level command |
| Automatically creates a home directory | Requires additional flags (e.g. `-m`) to create a home directory |
| Prompts for password and user details | Does not prompt for anything by default |
| Preferred on Debian/Ubuntu systems | Mainly used for scripting/automation |

### Recommended Command on Ubuntu

Ubuntu recommends `adduser` because it is interactive, safer for manual use, and sets up sensible defaults automatically:

```bash
sudo adduser testuser
```

### Example Workflow

Create the test user:
```bash
sudo adduser testuser
```

Switch to the new user:
```bash
su - testuser
```

Delete the user:
```bash
sudo deluser testuser
```

---

## Task 3: `journalctl`

### What is `journalctl`?

`journalctl` is the command-line utility used to query and display logs collected by `systemd`'s journal service (`systemd-journald`). It centralizes logs from the kernel, services, and applications in a single, structured location.

### Useful Commands

View all logs:
```bash
journalctl
```

View the most recent 50 lines:
```bash
journalctl -n 50
```

Follow logs in real time (like `tail -f`):
```bash
journalctl -f
```

View logs from the current boot only:
```bash
journalctl -b
```

View logs for a specific service (e.g. SSH):
```bash
journalctl -u ssh
```

View logs for Docker:
```bash
journalctl -u docker
```

View logs since today:
```bash
journalctl --since today
```

View logs from the last hour:
```bash
journalctl --since "1 hour ago"
```

---

## Task 4: Linux Command Cheat Sheet

### File & Directory Commands
```bash
pwd
ls
ls -l
ls -a
cd
mkdir
rmdir
rm
cp
mv
touch
cat
```

### File Viewing Commands
```bash
less
more
head
tail
tail -f
```

### Search Commands
```bash
find
grep
which
```

### User Management Commands
```bash
whoami
who
id
adduser
useradd
passwd
```

### Process Commands
```bash
ps
top
htop
kill
killall
```

### Disk Commands
```bash
df -h
du -sh
```

### Permission Commands
```bash
chmod
chown
chgrp
```

### Networking Commands
```bash
ping
ip a
ss
curl
wget
```

### System Information Commands
```bash
uname -a
hostname
uptime
free -h
```

---

## Images

### Task 1: Soft Link & Hard Link
![Soft link and hard link](<images/Screenshot 2026-09-01 221513.png>)

### Task 2: `adduser` vs `useradd`
![adduser vs useradd](<images/Screenshot 2026-09-01 221647.png>)

### Task 3: `journalctl`
![journalctl output](<images/Screenshot 2026-09-01 221836.png>)

### Task 4: Linux Command Cheat Sheet
![Linux commands overview 1](<images/Screenshot 2026-09-01 221859.png>)

![Linux commands overview 2](<images/Screenshot 2026-09-01 222021.png>)

![Linux commands overview 3](<images/Screenshot 2026-09-01 222103.png>)

---



