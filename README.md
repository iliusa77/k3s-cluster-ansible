# Build a Kubernetes cluster using K3s via Ansible

Author: <https://github.com/iliusa77>  

## Installation

### From source

The `k3s-ansible` repository can simply be cloned from github:

```console
$ git clone https://github.com/iliusa77/k3s-ansible.git
$ cd k3s-ansible
```

## Usage

Run Vagrant VMs
```bash
vagrant up
```

Generate SSH key ans send to VMs
```bash
mkdir ssh_key
ssh-keygen -t ed25519 -f ssh_key/id_ed25519
chmod 400 ssh_key/id_ed25519 ssh_key/id_ed25519.pub

ssh-copy-id -o StrictHostKeyChecking=no -i ssh_key/id_ed25519.pub vagrant@192.168.56.10
vagrant@192.168.56.10's password: vagrant

ssh-copy-id -o StrictHostKeyChecking=no -i ssh_key/id_ed25519.pub vagrant@192.168.56.11
ssh-copy-id -o StrictHostKeyChecking=no -i ssh_key/id_ed25519.pub vagrant@192.168.56.12
```

Edit the inventory file to match your cluster setup. For example:
```bash
---
k3s_cluster:
  children:
    server:
      hosts:
        192.168.56.10:
    agent:
      hosts:
        192.168.56.11:
        192.168.56.12:
```

## Install

*Running the playbook from inside the repository*

```bash
ansible-playbook -i inventory.yml install.yml -e k3s_version=v1.24.6+k3s1
```

*Checking k3s cluster status after install*

```bash
kubectl get nodes
NAME                STATUS   ROLES                  AGE     VERSION
k3s-master-node     Ready    control-plane,master   33m     v1.24.6+k3s1
k3s-worker-node-1   Ready    <none>                 33m     v1.24.6+k3s1
k3s-worker-node-2   Ready    <none>                 33m     v1.24.6+k3s1
```

## Upgrade

```bash
ansible-playbook -i inventory.yml install.yml -e k3s_version=v1.31.6+k3s1
```

*Checking k3s cluster status after upgrade*

```bash
kubectl get nodes
NAME                STATUS   ROLES                  AGE   VERSION
k3s-master-node     Ready    control-plane,master   25m   v1.31.6+k3s1
k3s-worker-node-1   Ready    <none>                 24m   v1.31.6+k3s1
k3s-worker-node-2   Ready    <none>                 24m   v1.31.6+k3s1
```

## Cleanup

```bash
ansible-playbook -i inventory.yml cleanup.yml
vagrant destroy -f
```
