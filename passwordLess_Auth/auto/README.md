# Ansible Playbook – Initial Server Setup

“We’re preparing a new server with the minimum secure configuration before deploying applications on it.”
This playbook sets up a secure Ubuntu server with a new `User`, `SSH key-based authentication`, `sudo Privileges`, `Essential packages`, and a `Firewall`.

---

## Features
`
`- Creating a non-root user`
`- Adding SSH keys for login`
- Giving the user sudo privileges
- Installing basic tools (git, curl, vim, ufw, etc.)
- Securing SSH (disable root password login)
- Enabling a firewall`
`

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

## Running this Playbook

1. **Obtain the playbook**
   ```bash
   git clone https://github.com/do-community/ansible-playbooks.git
   cd ansible-playbooks/setup_ubuntu1804
   ```

2. **Customize options**
   - Edit `vars/default.yml` to update the username or system packages as needed.

3. **Update your inventory**
   - Add your server details to the `inventory` file.

4. **Run the playbook**
   ```bash
   ansible-playbook -l [target] -i [inventory_file] -u [remote_user] playbook.yml


## Verification

- Login as the new user: `ssh user@your_server_ip`
- Confirm sudo works without a password: `sudo ls /root`
- Check UFW firewall rules: `sudo ufw status`

---
✅ Now your server is ready, secure, and manageable with Ansible.



