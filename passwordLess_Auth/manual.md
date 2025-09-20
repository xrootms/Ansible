#Ansible_passwordless_Authentication_Manual:

✅ Summary: 

1.Generate SSH key (ssh-keygen).
2.Copy public key to slaves (ssh-copy-id).
3.Verify login without password.

4.(Optional) Disable password login for extra security.

👉 Steps for Passwordless SSH Authentication:

✅1. Generate an SSH key on the master (control node)

👉 Run this on your Ansible master machine:

ssh-keygen Press Enter to accept defaults 
Leave the passphrase empty 
This creates:

Private key → ~/.ssh/id_rsa

Public key → ~/.ssh/id_rsa.pub

✅2. Copy the public key to the slave (managed node)

Use the ssh-copy-id command:

ssh-copy-id user@slave_ip


👉 Replace user with the remote username (root, ubuntu, ec2-user, etc.).

Enter the password one last time.

This appends your public key into:

~/.ssh/authorized_keys


on the remote machine.

✅3. Verify passwordless login

Now try:

ssh user@slave_ip_address


👉 It should log in without asking for a password.

✅4. (Optional) Update SSH server settings

On the slave machine, check /etc/ssh/sshd_config:

PasswordAuthentication no
PermitRootLogin no


Then restart SSH:

sudo systemctl restart sshd


👉 This enforces key-only login, more secure than passwords.

✅5. Use with Ansible

Now Ansible can connect without prompting for passwords:

ansible-playbook -i inventory.ini -u user playbook.yml
