# Ansible Playbook – Initial Server Setup

“We’re preparing a new server with the minimum secure configuration before deploying applications on it.”
This playbook sets up a secure Ubuntu server with a new `User`, `SSH key-based authentication`, `sudo Privileges`, `Essential packages`, and a `Firewall`.

---

## Features
- Creating a non-root user
- Adding SSH keys for login
- Giving the user sudo privileges
- Installing basic tools (git, curl, vim, ufw, etc.)
- Securing SSH (disable root password login)
- Enabling a firewall

---

## Prerequisites

1. Ansible installed on your control machine  
2. Target server(s) accessible via SSH  
3. Your SSH key available at: ~/.ssh/id_rsa.pub

---

## File Structure

```
project/
│── playbook.yml        # Main Ansible playbook
│── vars/
│   └── default.yml     # Variables file
│── inventory           # (Optional) Ansible inventory
│── README.md           # Documentation
```

---

## Variables

- Modify `vars/default.yml` to customize the username or system packages.  

---

## Running this Playbook

1. Obtain the playbook
  ```bash
git clone https://github.com/do-community/ansible-playbooks.git
cd ansible-playbooks/setup_ubuntu1804
   ```
2. Customize Options
- Modify `vars/default.yml` to customize the username or system packages.

3. Update your `inventory` file with server details:

4. Run the playbook:
   ```bash
  ansible-playbook -l [target] -i [inventory file] -u [remote user] playbook.yaml
   ```
---

## Verification

After the playbook runs:

- Login as the new user: `ssh user@your_server_ip`
 
- Confirm sudo works without a password: `sudo ls /root`

- Check UFW firewall rules: `sudo ufw status`

---
✅ Now your server is ready, secure, and manageable with Ansible.



