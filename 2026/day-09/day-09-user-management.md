# Day 09 – Linux User & Group Management Challenge

## Objective

Today I practiced Linux user and group management on my Ubuntu AWS EC2 instance.

I learned how to:

- Create users with home directories
- Set passwords for users
- Create groups
- Assign users to multiple groups
- Manage shared directories with group permissions
- Verify permissions and access using different users

---

# Users Created

I created four users with home directories.

| User | Purpose |
|------|---------|
| `tokyo` | Developer user |
| `berlin` | Developer + Admin user |
| `professor` | Admin user |
| `nairobi` | Team workspace user |

### Commands Used

```bash
sudo useradd -m tokyo
sudo passwd tokyo

sudo useradd -m berlin
sudo passwd berlin

sudo useradd -m professor
sudo passwd professor

sudo useradd -m nairobi
sudo passwd nairobi
