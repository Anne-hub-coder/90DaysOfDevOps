# Day 09 – Linux User & Group Management Challenge

## Objective

Today I practiced Linux user and group management on my Ubuntu AWS EC2 instance.

I learned how to:

- Create users with home directories
- Set passwords
- Create Linux groups
- Assign users to multiple groups
- Create shared directories
- Verify permissions using different users

---

## Task 1 – Create Users

### Commands

```bash
sudo useradd -m tokyo
sudo passwd tokyo

sudo useradd -m berlin
sudo passwd berlin

sudo useradd -m professor
sudo passwd professor
```

### Verification

```bash
grep "tokyo\|berlin\|professor" /etc/passwd
```

```bash
ls -l /home
```

### What I learned

- `useradd -m` creates both the user and home directory.
- Passwords are assigned separately using `passwd`.

---

## Task 2 – Create Groups

### Commands

```bash
sudo groupadd developers
sudo groupadd admins
```

### Verification

```bash
grep "developers\|admins" /etc/group
```

### What I learned

- Groups help organize users with shared permissions.
- `/etc/group` stores Linux group information.

---

## Task 3 – Assign Users to Groups

### Commands

```bash
sudo usermod -aG developers tokyo
sudo usermod -aG developers,admins berlin
sudo usermod -aG admins professor
```

### Verification

```bash
groups tokyo
groups berlin
groups professor
```

### Final Group Membership

| User | Groups |
|------|--------|
| tokyo | developers |
| berlin | developers, admins |
| professor | admins |

### What I learned

- `-aG` safely adds users to groups.
- A user can belong to multiple groups.

---

## Task 4 – Shared Directory

### Commands

```bash
sudo mkdir -p /opt/dev-project
sudo chgrp developers /opt/dev-project
sudo chmod 775 /opt/dev-project
```

### Verify Permissions

```bash
ls -ld /opt/dev-project
```

Expected:

```text
drwxrwxr-x
```

### Test Access

```bash
sudo -u tokyo touch /opt/dev-project/tokyo.txt
sudo -u berlin touch /opt/dev-project/berlin.txt
```

Verify:

```bash
ls -l /opt/dev-project
```

### What I learned

- `chgrp` changes group ownership.
- `chmod 775` gives owner and group members full access.

---

## Task 5 – Team Workspace

### Commands

```bash
sudo useradd -m nairobi
sudo passwd nairobi

sudo groupadd project-team

sudo usermod -aG project-team nairobi
sudo usermod -aG project-team tokyo

sudo mkdir -p /opt/team-workspace
sudo chgrp project-team /opt/team-workspace
sudo chmod 775 /opt/team-workspace
```

### Test

```bash
sudo -u nairobi touch /opt/team-workspace/nairobi.txt
```

Verify:

```bash
ls -ld /opt/team-workspace
ls -l /opt/team-workspace
```

### What I learned

- Shared workspaces make team collaboration easier.
- Group ownership simplifies access management.

---

## What I Learned

- Created Linux users with home directories.
- Managed passwords and user accounts.
- Created groups and assigned users.
- Used `usermod -aG` safely.
- Configured shared directories with `chgrp` and `chmod`.
- Tested permissions as different users.

---

## DevOps Takeaway

Linux user and group management is essential in DevOps because teams need secure shared access without giving unnecessary root permissions. Groups make collaboration safer and easier.

---

## Evidence

Screenshots collected during this exercise:

- users-created.png
- groups-created.png
- group-membership.png
- shared-directory.png
- team-workspace.png

---

## Day 09 Summary

Today I practiced Linux user and group management by creating users, assigning group memberships, configuring shared directories, and testing permissions in a real AWS EC2 environment.
