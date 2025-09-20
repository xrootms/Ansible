# Ansible Passwordless Authentication Manual

This guide explains how to set up passwordless SSH authentication for Ansible.  
Once configured, Ansible can connect to managed nodes without prompting for passwords.

---

## ✅ Summary

1. Generate SSH key (`ssh-keygen`)  
2. Copy public key to slaves (`ssh-copy-id`)  
3. Verify login without password  
4. (Optional) Disable password login for extra security  

---

## 👉 Steps for Passwordless SSH Authentication

### ✅ 1. Generate an SSH key on the master (control node)

Run this on your **Ansible master machine**:

```bash
ssh-keygen
```

- Press **Enter** to accept defaults  
- Leave the **passphrase empty**  

This creates:

- Private key → `~/.ssh/id_rsa`  
- Public key → `~/.ssh/id_rsa.pub`  

---

### ✅ 2. Copy the public key to the slave (managed node)

Use the `ssh-copy-id` command:

```bash
ssh-copy-id user@slave_ip
```

- Replace **`user`** with the remote username (`root`, `ubuntu`, `ec2-user`, etc.)  
- Enter the password **one last time**  

This appends your public key into:

```
~/.ssh/authorized_keys
```

on the remote machine.

---

### ✅ 3. Verify passwordless login

Now try:

```bash
ssh user@slave_ip_address
```

👉 It should log in **without asking for a password**.  

---

### ✅ 4. (Optional) Update SSH server settings

On the **slave machine**, edit:

```bash
sudo nano /etc/ssh/sshd_config
```

Update the following values:

```
PasswordAuthentication no
PermitRootLogin no
```

Restart SSH:

```bash
sudo systemctl restart sshd
```

👉 This enforces **key-only login**, more secure than passwords.  

---

### ✅ 5. Use with Ansible

Now Ansible can connect without prompting for passwords:

```bash
ansible-playbook -i inventory.ini -u user playbook.yml
```

Example `inventory.ini`:

```ini
[webservers]
192.168.1.101
192.168.1.102
```

---

## Done!

successfully set up **Passwordless SSH Authentication for Ansible** 🚀

