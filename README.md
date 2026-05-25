# Lab 1 — Linux & Git Foundations

## What this project does

This project automates the setup of a fresh Ubuntu 22.04 server for the University IT Club website.

After running the provisioning script, the server will have:

- NGINX installed and running
- UFW firewall configured
- Git installed
- Curl installed
- Ports 22 (SSH), 80 (HTTP), and 443 (HTTPS) opened

The server is secured by disabling SSH password authentication and preventing root login through SSH.

---

## Files

- provision.sh — Installs and configures NGINX, UFW, Git, and Curl.
- deploy.sh — Copies and executes provision.sh on a remote server using SSH.
- README.md — Project documentation.
- screenshots/checkpoint1.png — SSH hardening verification screenshot.
- screenshots/checkpoint2.png — NGINX welcome page screenshot.

---



```bash
curl http://$(hostname -I | awk '{print $1}')
```

---

## Repository

https://gitlab.com/YOUR_USERNAME/devops-lab1

---

## Screenshots

- <img width="746" height="331" alt="1" src="https://github.com/user-attachments/assets/10a600cd-5605-409f-a289-ed8ef4104e2f" />
— Output showing:

```text
PasswordAuthentication no
PermitRootLogin no
```

<img width="747" height="201" alt="image" src="https://github.com/user-attachments/assets/7829bd90-b2c6-4981-842b-898bc51edb86" />
— Browser showing the NGINX Welcome Page.

---

## Pre-Lab Answers

### Q1. What is the difference between sudo su and su -?

`sudo su` uses the current user's password and grants root privileges. It switches to the root user but may preserve parts of the current environment.

`su -` requires the root user's password and starts a full root login session with the root user's environment, home directory, and PATH settings.

---

### Q2. Why do we use SSH keys instead of passwords for remote login?

SSH keys provide stronger security than passwords because they are much longer and harder to guess. They help protect against brute-force attacks and provide encrypted authentication.

---

### Q3. What does chmod 600 ~/.ssh/authorized_keys do, and why does SSH require it?

The command restricts access so only the file owner can read and write the file.

SSH requires these permissions because if other users can access or modify the file, unauthorized users could gain access to the server.

---

## Answers

### PQ1. Your script ran apt upgrade -y automatically. On a live production server, why could an unattended upgrade be risky? What could go wrong? How do real organizations handle upgrades more safely?

Automatic upgrades can introduce software incompatibilities, configuration changes, or service failures that may cause downtime.

Organizations typically test updates in development or staging environments before applying them to production servers. They also schedule maintenance windows and keep backups for recovery.

---

### PQ2. What happens if you skip the UFW firewall step? Why is it dangerous to leave port 22 open to the entire internet? Name at least two ways to reduce that risk.

Without UFW, unnecessary ports may remain exposed to attackers.

Leaving SSH (port 22) open to the internet can lead to brute-force attacks and unauthorized access attempts.

Two ways to reduce the risk are:

1. Disable password authentication and use SSH keys.
2. Restrict SSH access to specific IP addresses using firewall rules.

---

### PQ3. You committed provision.sh to Git instead of running commands manually. Why is storing infrastructure setup in version control better than typing commands by hand each time?

Version control provides consistency, reproducibility, collaboration, and auditing.

Benefits include:

- The same server configuration can be recreated anytime.
- Team members can review and improve scripts.
- Every change is tracked with commit history.
- Previous versions can be restored if needed.

---

## Author

Name: Nuyu Ikirezi

Course: DevOps 

Lab: Linux 
