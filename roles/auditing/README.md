Auditing
=========

Mounts the shared drive and then goes to targets and fetches their audits, erasing or deleting the audits afterwards (depending on if rotated log or not).
My configs are for a windows shared drive on the domain, edit as needed to fit your enviornment

Logs are saved to the mounted share in the following format: //<share>//<YYYY-MM-DD>/<inventory_hostname>/var/log/

Requirements
------------

cifs-utils

Role Variables
--------------

| Variable  | Location | Required | Default | Description
| ------------- | ------------- | ------------- | ------------- | ------------- |
| auditor_password  | ./roles/auditing/vars/secrets.yml | Yes  | N/A | Account that can |
| krb5_default_realm  | ./roles/sssd_auth/vars/main.yml | Yes  | N/A | where the kerberos authentication occurs (typically same as realm_domain). Must be in all CAPS. |
| realm_ad_ou | ./roles/sssd_auth/vars/main.yml |Yes | N/A | the OU or CN (in LDAP form) to place the PC when joined to the domain |
| sudo_group | ./roles/sssd_auth/vars/main.yml |Yes | N/A | Adds the specified group to allow the ability to sudo|
| kerberos_user | ./roles/sssd_auth/vars/secrets.yml | Yes | N/A | The user that can add computers to the domain |
| kerberos_user_password | ./roles/sssd_auth/vars/secrets.yml | Yes | N/A | The password of the user that can add computers to the domain |

- /var/secrets: auditor_password 		#Holds the auditor account password
- /var/main.yml: delete_me 		#Empty array later used to hold files to be deleted
- /var/main.yml: erase_me			#Empty array later used to hold files to be erased
- /var/main.yml: audits_list		#Empty array later used to hold audits that will be copied
- /var/main.yml: share_drive #contains path to shared drive
- /var/main.yml: share_domain #contains domain name
- /var/main.yml: share_username #contains a username of the user capable of mounting the share

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
