# Day 11 – File Ownership Challenge (chown & chgrp)

## Objective

Today I practiced Linux file ownership by learning how to change file owners, groups, and apply ownership recursively.

I worked with:

- `chown`
- `chgrp`
- Linux users and groups
- Recursive ownership
- Shared directories

---

## Task 1 – Understanding Ownership

### Commands

```bash
ls -l
```

### Verification

I identified the **owner** and **group** columns in the output.

Example format:

```text
-rw-r--r-- 1 owner group size date filename
```

### What I learned

- Every Linux file has both an owner and a group.
- Linux uses ownership to control access.

---

## Task 2 – Change File Owner

### Commands

```bash
touch devops-file.txt

ls -l devops-file.txt

sudo chown tokyo devops-file.txt

ls -l devops-file.txt

sudo chown berlin devops-file.txt

ls -l devops-file.txt
```

### Result

The owner changed from `ubuntu` to `tokyo`, and then to `berlin`.

### What I learned

- `chown` changes file ownership.
- Ownership changes usually require `sudo`.

---

## Task 3 – Change File Group

### Commands

```bash
touch team-notes.txt

ls -l team-notes.txt

sudo groupadd heist-team

sudo chgrp heist-team team-notes.txt

ls -l team-notes.txt
```

### Result

The file group changed successfully.

### What I learned

- `chgrp` changes group ownership.
- Groups allow multiple users to share access securely.

---

## Task 4 – Change Owner and Group Together

### Commands

```bash
touch project-config.yaml

sudo groupadd heist-team

sudo chown professor:heist-team project-config.yaml

ls -l project-config.yaml

mkdir app-logs

sudo chown berlin:heist-team app-logs

ls -ld app-logs
```

### Result

Both owner and group changed successfully using a single command.

### What I learned

- `owner:group` syntax updates both together.
- Directories also have ownership like files.

---

## Task 5 – Recursive Ownership

### Commands

```bash
mkdir -p heist-project/vault
mkdir -p heist-project/plans

touch heist-project/vault/gold.txt
touch heist-project/plans/strategy.conf

sudo groupadd planners

sudo chown -R professor:planners heist-project

ls -lR heist-project
```

### Result

The entire directory structure now belongs to `professor` and the `planners` group.

### What I learned

- `-R` applies ownership recursively.
- This is useful for application folders and deployments.

---

## Task 6 – Ownership Practice Challenge

### Commands

```bash
sudo groupadd vault-team

sudo groupadd tech-team

mkdir bank-heist

touch bank-heist/access-codes.txt
touch bank-heist/blueprints.pdf
touch bank-heist/escape-plan.txt

sudo chown tokyo:vault-team bank-heist/access-codes.txt

sudo chown berlin:tech-team bank-heist/blueprints.pdf

sudo chown nairobi:vault-team bank-heist/escape-plan.txt

ls -l bank-heist
```

### Final Ownership

| File | Owner | Group |
|------|-------|--------|
| access-codes.txt | tokyo | vault-team |
| blueprints.pdf | berlin | tech-team |
| escape-plan.txt | nairobi | vault-team |

### What I learned

- Different files can have different owners.
- Groups make secure collaboration easier.

---

## Commands Used

```bash
ls -l
touch devops-file.txt
sudo chown tokyo devops-file.txt
sudo chown berlin devops-file.txt
touch team-notes.txt
sudo groupadd heist-team
sudo chgrp heist-team team-notes.txt
touch project-config.yaml
sudo chown professor:heist-team project-config.yaml
mkdir app-logs
sudo chown berlin:heist-team app-logs
mkdir -p heist-project/vault
mkdir -p heist-project/plans
touch heist-project/vault/gold.txt
touch heist-project/plans/strategy.conf
sudo groupadd planners
sudo chown -R professor:planners heist-project
sudo groupadd vault-team
sudo groupadd tech-team
mkdir bank-heist
touch bank-heist/access-codes.txt
touch bank-heist/blueprints.pdf
touch bank-heist/escape-plan.txt
sudo chown tokyo:vault-team bank-heist/access-codes.txt
sudo chown berlin:tech-team bank-heist/blueprints.pdf
sudo chown nairobi:vault-team bank-heist/escape-plan.txt
ls -l bank-heist
```

---

## What I Learned

- Every Linux file has an owner and a group.
- `chown` changes file ownership.
- `chgrp` changes group ownership.
- `chown owner:group` updates both together.
- Recursive ownership with `-R` is useful for project directories.
- Proper ownership improves security and collaboration.

---

## DevOps Takeaway

File ownership is critical in DevOps because applications, containers, CI/CD pipelines, and shared environments depend on the correct users and groups having the right access.

---

## Evidence

Screenshots collected during this exercise:

- `ownership-before.png`
- `owner-changes.png`
- `group-change.png`
- `recursive-ownership.png`
- `bank-heist-ownership.png`

---

## Day 11 Summary

Today I practiced Linux file ownership by changing file owners, assigning groups, applying recursive ownership, and managing shared project files. This strengthened my understanding of how Linux controls access in real DevOps environments.
