# centos7-ovirt4-engine
Playbooks to help build a ovirt 4 node on CentOS 7 

# Prerequisites
You should begin with a fresh CentOS 7 server which meets ovirt requirements

For this playbook, you also need to have a lvm vg. If you don't have one, please create one.

```
fdisk /dev/sda #don't forget type t/8e before w 

partx -v -a /dev/sda
pvcreate /dev/sda4
vgcreate vg_data /dev/sda4
```

You also need Ansible 2.3 to automate ovirt configuration (adding VMs and networks and such), so this playbook will compile it in role centos7-ansible23

# Installing prerequisites and packages

```
yum install -y epel-release
yum install -y git ansible
```

## Getting the ansible roles

```
cd /tmp
git clone https://github.com/zwindler/centos7-ovirt4-engine
#Copy files to the right location
cp -rp centos7-ovirt4-engine/roles /etc/ansible/roles
cp centos7-ovirt4-engine/*.yml /etc/ansible/
```

Side note: answer file for has been generated with command "engine-setup --generate-answer=/tmp/engine-setup-answers.j2"

## Executing playbooks

If you want to install oVirt prerequisites and launch engine setup
```
ansible-playbook centos7-ovirt4-engine.yml
```

If you want to launch ovirt engine setup with the default configuration. You can review/change the variables given by opening the generated answer file located at /tmp/engine-setup-answers. 

From there, you should be able to connect to the ovirt web console to https://[FQDN_OF_YOUR_HOST]
