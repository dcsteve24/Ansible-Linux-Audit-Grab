# Ansible-Linux-Audit-Grab
Grabs all linux logs, sticks them in a windows shared drive, and deletes or erases them (based on if rotated or not)

Download is expected to be in the root ansible folder; default of /etc/ansible/

Upon download, user must edit the files based on their enviornment. I have marked most of these with a "# --->" to easily identify them. Files that need edited are the following:

1. ./roles/auditing/handlers/main.yml, under the "unmount share module" enter your share path. Remove the #--->
2. ./roles/auditing/tasks/mount_share.yml, enter your src (share path), and your options. This section is prepared for a Windows SMB3 enabled share, so change settings as needed for you enviornment. Remove the #--->
3. ./roles/auditing/vars/secrets.yml, enter your password to mount the share with. Encrypt the file with ansible-vault encrypt path_to_file.
    Remove the #--->
4. ./hosts, add the targets and list the host you are running from under the local group.
5. ./playbooks/Move_Audit.yml, enter your ansible user you SSH/sudo with.

I typically run this play with ansible-playbooks -kK --ask-vault-pass path_to_playbook.yml
