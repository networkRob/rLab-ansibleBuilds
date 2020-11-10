## rLab Ansible Builds
This repo will contain different playbooks that will leverage a combination of roles to create different purpose built nodes.

Make sure to update the `hosts` file to include your target devices for your enviroment.

### Requirements

Requires Ansible version >= 2.8

### Playbooks
Here is a list of playbooks and what is required.

#### cEOS_host_build.yaml
This playbook (at the moment) requires an install of Centos 64-bit.  It has been tested on Centos-7-1810 Minimal.  When installing CentOS and initial configuration, create a user with admin priveledges.  Then add that user to the `host_user` parameter in `group_vars/all/vars.yaml`.  

When the `add_docker` role is ran, there is an option to add any users into the `docker` group, so `sudo` is not required to run docker.  Modify the `docker_users` list parameter located in `roles/add_docker/defaults/main.yml` to include any users.

For the `cEOS` role, update the `cnt_imgs` parameter section to include any cEOS archive to be uploaded into the host node's docker images.  Place any cEOS source images in `roles/cEOS/files`.  This role will also clone a starter cEOS-Lab topology repo.  This repo is located at: 

https://github.com/networkRob/rLab-eos

To run this playbook, it is best to have already copied your public ssh-keys to the target node, for each of playbook execution.  Since the playbook will required elevated permissions, run the playbook with the following:
```
ansible-playbook cEOS_host_build.yaml -K
```

or 

```
ansible-playbook docker_host_build.yaml -K
```
The `-K` flag will ask at execution for your `become` password to run.
