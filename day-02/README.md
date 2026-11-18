# Day 2 – Linux User and Group Administration

## Objective
Practise Linux user and group management, directory permissions and shared access.

## Practical Tasks Completed

1. Created a Linux group named `devops`.
2. Created a Linux user named `devuser`.
3. Added `devuser` to the `devops` supplementary group.
4. Created `/opt/devops-project`.
5. Changed group ownership using `chown`.
6. Configured directory permissions using `chmod 770`.
7. Tested file creation using `sudo -u devuser`.
8. Enabled SGID using `chmod 2770`.
9. Verified group inheritance for newly created files.

## Commands Practised

```bash
sudo groupadd devops
sudo useradd -m -s /bin/bash devuser
sudo usermod -aG devops devuser
sudo mkdir /opt/devops-project
sudo chown :devops /opt/devops-project
sudo chmod 770 /opt/devops-project
sudo -u devuser touch /opt/devops-project/test.txt
sudo chmod 2770 /opt/devops-project
sudo -u devuser touch /opt/devops-project/team-file.txt
```

## Key Learnings

- UID identifies a Linux user.
- GID identifies a Linux group.
- `chmod` changes permissions.
- `chown` changes ownership.
- `usermod -aG` adds supplementary group membership.
- SGID makes new files inherit the directory's group ownership.

## Result

Successfully created Linux users and groups, configured shared directory permissions, and verified SGID group inheritance.
