Auditing
=========

Mounts the shared drive and then goes to targets and fetches their audits, erasing or deleting the audits afterwards (depending on if rotated log or not).
My configs are for a windows shared drive on the domain, edit as needed to fit your enviornment (i.e. removing the share_domain variable and entry in tasks)

Logs are saved to the mounted share in the following format: //share_name/YYYY-MM-DD/inventory_hostname/var/log/

Requirements
------------

cifs-utils

Role Variables
--------------

| Variable  | Location | Required | Default | Description
| ------------- | ------------- | ------------- | ------------- | ------------- |
| user_password | ./roles/auditing/vars/secrets.yml | Yes  | N/A | password for user that can mount the share |
| delete_me | ./roles/auditing/vars/main.yml | No | [ ] | empty array later used to hold files to be deleted |
| erase_me | ./roles/auditing/vars/main.yml | No | [ ] | empty array later used to hold files to be erased |
| audits_list | ./roles/auditing/vars/main.yml | No | [ ] | empty array later used to hold audits that will be copied |
| share_drive | ./roles/auditing/vars/main.yml | Yes | N/A | contains the path to the shared drive |
| share_domain | ./roles/auditing/vars/main.yml | Yes | N/A | the domain name of where the share resides |
| share_username | ./roles/auditing/vars/main.yml | Yes | N/A | username of the user capable of mounting the share

various self contained variables inside the play through register command


Example Playbook
----------------

    - hosts: all
      roles:
         - auditing

I run with ansible-playbook -kK --ask-vault-pass path_to_playbook

Author Information
------------------

Steven Craig, 27Jan19
