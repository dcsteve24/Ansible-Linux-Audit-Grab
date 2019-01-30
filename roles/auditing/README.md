Role Name
=========

Mounts the shared drive and then goes to targets and fetches their audits, erasing or deleting the audits afterwards (depending on if rotated log or not).
My configs are for a windows shared drive on the domain, edit as needed to fit your enviornment

Logs are saved to the mounted share in the following format: //<share>//<YYYY-MM-DD>/<inventory_hostname>/var/log/

Requirements
------------

cifs-utils

Role Variables
--------------

/var/secrets: auditor_password 		#Holds the auditor account password
/var/main.yml: delete_me 		#Empty array later used to hold files to be deleted
/var/main.yml: erase_me			#Empty array later used to hold files to be erased
/var/main.yml: audits_list		#Empty array later used to hold audits that will be copied
 
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
