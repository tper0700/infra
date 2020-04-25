# infra

Infrastructure Automation

## Overview
This project deploys Kubernetes on VirtualBox VMs using Ansible.

## Deploying
Add the following files to make this project work:

### group_vars/all/vault  

```yaml
vault_cluster_ip_range: x.x.x.x-x.x.x.y
```
IP address range used by MetalLB to configure apps on external IP addresses.

### group_vars/nodes/vault  

```yaml
vault_guest_ansible_ssh_user: admin #admin account name to use inside VMs in the cluster
vault_guest_ansible_ssh_password: passwd #password for admin account
vault_ansible_ssh_private_key_file: ~/.ssh/id_xxxx # Local ssh key file for ansible to use to auth to key below
vault_ansible_private_key: ssh... #ssh key value to append to cloud-init file
```

### group_vars/vmhosts/vault  

```yaml
vault_host_ansible_ssh_user: account # name of admin account for ansible to use to log in to VirtualBox server
vault_ansible_ssh_private_key_file: ~/.ssh/id_xxxx # SSH Key file ansible should use to log in to virtualbox server
```

### roles/docker/files/registry.crt  
PEM file to add to docker VMs to authenticate against a private docker registry (when using self signed certs)

### roles/vmhost/tasks/arch_base.ova  
OVA image of base VM to create for each virtual box guest.