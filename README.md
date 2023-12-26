<div id="header" align="center">
  <img src="assets/readme.jpg" width="150"/>

  # :lock: SSH key based authentication + 2FA setup
</div>

> !!! The 2FA secret is only sent ONCE in the initial setup phase, SAVE IT !!!


### Use cases
This project was designed to cover the following use case:
- Password authentication is currently used for authentication on SSH, but want to switch to only key based authentication
- Key based authentication needs to be setup for SSH
- Two-factor authentication needs to be setup for SSH login
- SSH user serves as a 'stepping stone' to a more privileged user
- SUDO(privileged) user requires password to authenticate AFTER SSH authentication has succeeded

### Technical information
- Root login to SSH is disabled
- SSH user only exists for authenticating remotely to the system, and has NO privileges
- SSH user can 'su' to SUDO user to gain privileges
- Google Authenticator is required for 2FA
- SSH listens on port 22
- MaxAuthTries is 6
- MaxSessions is 10
- The provided inventory retrieves hostname, username and password from ENV, it is mainly for ILLUSTRATIONAL purposes

### Limitations
- 2FA secret is only sent ONCE in the initial setup, and might be hard to read.
- Only create one SSH and one SUDO user.
- Does not create SSH keys for authentication, the user is REQUIRED to provide the public SSH key and other variables in the vars/ directory.

### Usage
1. Edit roles/ssh/vars/main.yml so it matches with what you want
2. Run the playbook by using the following command:
```
ansible-playbook playbooks/ssh.yml -i inventories/ssh.yml
```
3. Safe the Google Authenticator code provided in the output, it will NOT be shown again 
4. Enjoy key based authentication + 2FA on your server!