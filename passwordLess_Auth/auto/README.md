# Ansible Playbook – Server Bootstrap Setup

This Ansible playbook sets up a secure Ubuntu/Debian server with a new user, SSH key-based authentication, sudo privileges, essential packages, and a firewall.

---

## Features

- Creates a new user with sudo privileges  
- Configures **passwordless sudo** for the `wheel` group  
- Adds an **SSH public key** for secure login  
- Disables **root password login**  
- Installs required system packages (`curl`, `vim`, `git`, `ufw`, etc.)  
- Sets up **UFW firewall**:  
  - Allows SSH  
  - Denies all other incoming traffic by default  

---

## Prerequisites

1. Ansible installed on your control machine  
   ```bash
   sudo apt update && sudo apt install ansible -y
   ```

2. Target server(s) accessible via SSH  

3. Your SSH key available at:
   ```bash
   ~/.ssh/id_rsa.pub
   ```

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



