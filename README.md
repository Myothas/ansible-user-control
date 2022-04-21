# ansible-user-control  
Manages users and their ssh keys on linux hosts.  

<span style="color:red">Important Notes:</span>
* Any users not specified in the user-vars.yml will be deleted *(Excluding centos and ubuntu)*.
* If you don't want the users to be able to escalate to root without password change `escalate_root_no_pass` to false.
    
# Usage
***user-control/vars/user-vars.yml*** contains the list of users you want to create.
  
## Example:  
```
- username: username
  fullname: "Full Name"
  email: "george.bob@bigcorp.org"
  shell: /bin/bash
  ssh_key: "{{ lookup('file', 'username.pub') }}"
  exclusive_ssh_key: yes
  user_state: present
  groups: admin
  servers:
    - masters
    - bastion
```
  
**For each new user you create you must:**
* Create a public key file under ***user-control/files/*** which matches the username.
* Provide a list of groups matching the inventory groups which the user should have access.
