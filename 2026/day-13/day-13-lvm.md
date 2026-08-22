# Day 13 – Linux Volume Management (LVM)

## Objective

Today I learned how to use Linux Logical Volume Manager (LVM) to create, mount, and extend storage on an AWS EC2 instance.

I practiced:

- Creating a virtual disk
- Setting up a Physical Volume (PV)
- Creating a Volume Group (VG)
- Creating a Logical Volume (LV)
- Formatting and mounting the volume
- Extending the logical volume

---

## Environment Setup

I switched to the root user.

### Command

```bash
sudo -i
```

Since my EC2 instance did not have an extra disk, I created a virtual disk.

### Command

```bash
dd if=/dev/zero of=/tmp/disk1.img bs=1M count=300
```

This created a **300 MB virtual disk**.

---

## Create a Loop Device

I attached the virtual disk to a loop device.

### Commands

```bash
losetup -fP /tmp/disk1.img
losetup -a
```

The virtual disk was attached as:

```text
/dev/loop3
```

---

## Task 1 – Check Current Storage

### Commands

```bash
lsblk
pvs
vgs
lvs
df -h
```

### What I learned

- `lsblk` shows block devices.
- `pvs`, `vgs`, and `lvs` display LVM information.

---

## Task 2 – Create a Physical Volume

### Command

```bash
pvcreate /dev/loop3
```

### Verify

```bash
pvs
```

### Result

The physical volume was created successfully.

---

## Task 3 – Create a Volume Group

### Command

```bash
vgcreate devops-vg /dev/loop3
```

### Verify

```bash
vgs
```

### Result

Volume group:

```text
devops-vg
```

was created successfully.

---

## Task 4 – Create a Logical Volume

### Command

```bash
lvcreate -L 200M -n app-data devops-vg
```

### Verify

```bash
lvs
```

### Result

Logical volume:

```text
app-data
```

was created successfully.

---

## Task 5 – Format and Mount the Volume

### Commands

```bash
mkfs.ext4 /dev/devops-vg/app-data

mkdir -p /mnt/app-data

mount /dev/devops-vg/app-data /mnt/app-data

df -h /mnt/app-data
```

### Test

```bash
echo "Day 13 LVM Practice" > /mnt/app-data/test.txt

cat /mnt/app-data/test.txt
```

Output:

```text
Day 13 LVM Practice
```

### What I learned

- `mkfs.ext4` formats the logical volume.
- `mount` makes the storage accessible.
- `df -h` confirms the mounted filesystem.

---

## Task 6 – Extend the Logical Volume

I first tried adding **50 MB**, but LVM reported insufficient free space.

Instead, I used all remaining free space.

### Commands

```bash
lvextend -l +100%FREE /dev/devops-vg/app-data

resize2fs /dev/devops-vg/app-data

df -h /mnt/app-data
```

### Result

The logical volume expanded successfully using the remaining available space.

### What I learned

- `lvextend` increases the size of a logical volume.
- `resize2fs` expands the filesystem after the volume grows.
- `-l +100%FREE` uses all remaining free space.

---

## Challenge Faced

While creating the Physical Volume, I encountered duplicate loop device warnings because the same disk image was attached twice.

I fixed it by removing the duplicate loop device and continuing with the setup.

I also received an "Insufficient free space" error while extending the volume, which I solved using:

```bash
lvextend -l +100%FREE
```

---

## Commands Used

```bash
sudo -i

dd if=/dev/zero of=/tmp/disk1.img bs=1M count=300

losetup -fP /tmp/disk1.img

losetup -a

lsblk

pvs

vgs

lvs

df -h

pvcreate /dev/loop3

vgcreate devops-vg /dev/loop3

lvcreate -L 200M -n app-data devops-vg

mkfs.ext4 /dev/devops-vg/app-data

mkdir -p /mnt/app-data

mount /dev/devops-vg/app-data /mnt/app-data

echo "Day 13 LVM Practice" > /mnt/app-data/test.txt

cat /mnt/app-data/test.txt

lvextend -l +100%FREE /dev/devops-vg/app-data

resize2fs /dev/devops-vg/app-data

df -h /mnt/app-data
```

---

## What I Learned

- LVM provides flexible storage management.
- A Physical Volume forms the foundation of LVM storage.
- Volume Groups combine storage into a pool.
- Logical Volumes can be created from that pool.
- Filesystems must be resized after extending a logical volume.
- `-l +100%FREE` is useful when extending a volume with all remaining space.

---

## DevOps Takeaway

In real DevOps environments, storage requirements change frequently. LVM allows administrators to expand application storage without recreating disks, making it an essential skill for managing production servers.

---

## Evidence

Screenshots collected during this exercise:

- `lsblk-output.png`
- `pv-vg-lv-created.png`
- `mounted-volume.png`
- `volume-extended.png`

---

## Day 13 Summary

Today I completed my first Linux LVM lab by creating a virtual disk, building an LVM storage stack (PV → VG → LV), mounting it, testing it with a file, and extending the storage successfully.
