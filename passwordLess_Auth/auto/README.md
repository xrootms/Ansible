# Ansible Playbook – Initial Server Setup

“We’re preparing a new server with the minimum secure configuration before deploying applications on it.”
This playbook sets up a secure Ubuntu server with a new User, SSH key-based authentication, sudo Privileges, Essential packages, and a Firewall.

---

## Features
Creating a non-root user
Adding SSH keys for login
Giving the user sudo privileges
Installing basic tools (git, curl, vim, ufw, etc.)
Securing SSH (disable root password login)
Enabling a firewall

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

## Variables (`vars/default.yml`)

```yaml
create_user: sammy
copy_local_key: "{{ lookup('file', lookup('env','HOME') + '/.ssh/id_rsa.pub') }}"
sys_packages: [ 'curl', 'vim', 'git', 'ufw' ]
```

- **create_user** → Name of the new user to be created  
- **copy_local_key** → Path to your local SSH public key  
- **sys_packages** → List of essential packages to install  

---

## Usage

1. Update your `inventory` file with server details:
   ```ini
   [all]
   your_server_ip ansible_user=root ansible_ssh_private_key_file=~/.ssh/id_rsa
   ```

2. Run the playbook:
   ```bash
   ansible-playbook -i inventory playbook.yml
   ```

---

## Verification

After the playbook runs:

- Login as the new user:
  ```bash
  ssh sammy@your_server_ip
  ```
- Confirm sudo works without a password:
  ```bash
  sudo ls /root
  ```
- Check UFW firewall rules:
  ```bash
  sudo ufw status
  ```

---

## Notes

- This setup **disables root password login** but allows root login with SSH keys if configured.  
- Make sure you have your **SSH key added** before running the playbook.  
- Modify `vars/default.yml` to customize the username or system packages.  

---
✅ Now your server is ready, secure, and manageable with Ansible.



