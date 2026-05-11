````md
# whoamilab - Start Walkthrough

Beginner SSH enumeration challenge.

Difficulty: ★☆☆☆☆  
Category: SSH / Linux Enumeration

---

# Objective

Connect to the remote Linux server and locate the hidden flag file.

---

# Connect to the Server

```bash
ssh student@[TARGET-IP] -p 30003
````

---

# SSH Warning Fix

While connecting, the following error appeared:

```text
WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED!
Host key verification failed.
```

This happens when an old SSH fingerprint is saved locally.

Remove the outdated key:

```bash
ssh-keygen -f "/home/YOUR-USERNAME/.ssh/known_hosts" -R "[TARGET-IP]:30003"
```

Reconnect again:

```bash
ssh student@[TARGET-IP] -p 30003
```

When prompted:

```text
Are you sure you want to continue connecting (yes/no/[fingerprint])?
```

Type:

```text
yes
```

Enter the password:

```text
password123
```

---

# Initial Enumeration

After logging in:

```bash
whoami
pwd
ls -la
```

Example output:

```text
student
/home/student
```

---

# Find the Flag

Search the filesystem for files containing "flag":

```bash
find / -iname "*flag*" 2>/dev/null
```

Discovered file:

```text
/opt/it-staff/.confidential/.flag.txt
```

---

# Common Mistake

Trying to execute the file directly:

```bash
/opt/it-staff/.confidential/.flag.txt
```

Result:

```text
Permission denied
```

The file must be read using `cat`.

---

# Enumerate Permissions

Check directory permissions:

```bash
ls -la /opt
ls -la /opt/it-staff
ls -la /opt/it-staff/.confidential
```

---

# Read the Flag

```bash
cat /opt/it-staff/.confidential/.flag.txt
```

Flag successfully retrieved.

---

# Optional Enumeration

Check sudo privileges:

```bash
sudo -l
```

Check SUID binaries:

```bash
find / -perm -4000 2>/dev/null
```

---

# Final Notes

* Always use `cat` to read text files.
* Hidden directories often contain sensitive information.
* Basic Linux enumeration is important in CTF challenges.

Happy Hacking :)

```
```
