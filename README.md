# Ansible-Linux-Audit-Grab

Move-Audits
=========

Mounts the shared drive and then goes to targets and fetches their audits, erasing or deleting the audits afterwards (depending on if rotated log or not).
My configs are for a windows shared drive on the domain, edit as needed to fit your enviornment (i.e. removing the share_domain variable and entry in tasks)

Logs are saved to the mounted share in the following format: //share_name/YYYY-MM-DD/inventory_hostname/var/log/

This includes exemptions for fail2ban, to prevent the accidental deletion of its main log.

Requirements
------------

cifs-utils is required on the server mounting the share

1. ./roles/auditing/handlers/main.yml, under the "unmount share module" enter your share path.
2. ./roles/auditing/vars/secrets.yml, enter your password to mount the share with. Encrypt the file with ansible-vault encrypt path_to_file.
3. ./roles/auditing/vars/main.yml, enter your enviornment information for share_drive, share_domain, and share_username
4. ./hosts, add the targets and list the host you are running from under the local group.
5. ./playbooks/Move_Audit.yml, enter your ansible user you SSH/sudo with.

I typically run this play with ansible-playbooks -kK --ask-vault-pass path_to_playbook.yml

Role Variables
--------------

| Variable  | Location | Required | Default | Description
| ------------- | ------------- | ------------- | ------------- | ------------- |
| user_password | ./roles/auditing/vars/secrets.yml | Yes  | N/A | password for user that can mount the share |
| delete_me | ./roles/auditing/defaults/main.yml | No | [ ] | empty array later used to hold files to be deleted |
| erase_me | ./roles/auditing/defaults/main.yml | No | [ ] | empty array later used to hold files to be erased |
| audits_list | ./roles/auditing/defaults/main.yml | No | [ ] | empty array later used to hold audits that will be copied |
| share_drive | ./roles/auditing/vars/main.yml | Yes | N/A | contains the path to the shared drive |
| share_domain | ./roles/auditing/vars/main.yml | Yes | N/A | the domain name of where the share resides |
| share_username | ./roles/auditing/vars/main.yml | Yes | N/A | username of the user capable of mounting the share

various self contained variables inside the play through register command


Example Playbook
----------------

    - hosts: all
      become: true
      roles:
         - auditing

I run with ansible-playbook -kK --ask-vault-pass path_to_playbook

Author Information
------------------

Steven Craig, 27Jan19
