## Intro
 - Ansible playbook to pull service from repository using ssh and install it's dependencies & update it on windows & linux (Multi-Stage Environments strategy).
 
 ![Example](https://user-images.githubusercontent.com/38042656/127904481-8a40e4d1-7f8e-40f7-a343-21441aaab5c9.png)
## How to use it

0.  make sure the file ansible.cfg points to your private key and create an invontory file with the list of nodes to run ansible onto, like this:

        [nodes]
        server_host_or_IP ansible_user=sshuser

1.  to run the playbook in `Development` ❯ `ansible-playbook playbooks/service_playbook.yml`
2.  to run the playbook in `Production` ❯ `ansible-playbook playbooks/service_playbook.yml -i environments/prod`
2.  use `--list-tasks` to list all tasks that would be executed by a play without making any changes to the remote servers or use `--list-hosts` to list all hosts that would be affected by a playbook and `--list-tags` for tags.

- you need to **decrypt secrets.yml** before testing the playbook by using  `ansible-vault decrypt default_env/secrets.yml`
- after testing the playbook **encrypt** it again by using `ansible-vault encrypt default_env/secrets.yml`
 
### note for windows users

- if you have installed ansible using CygWin, make sure that your ssh keys are located under: `/home/$USER/.ssh/`. This might imply copying them like ` cp /cygdrive/c/Users/$USER/.ssh/id_rsa* /home/$USER/.ssh/`
