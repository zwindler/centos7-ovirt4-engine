# centos7-ovirt-enginesetup
Playbooks to help build a ovirt allinone node on CentOS 7

# Prerequisites
You should begin with a fresh CentOS 7 server which meets ovirt requirements

For this playbook, you also need to have a lvm vg. If you don't have one, please create one

```
fdisk /dev/sda #don't forget type t/8e before w 

partx -v -a /dev/sda
pvcreate /dev/sda4
vgcreate vg_data /dev/sda4
```

# Installing prerequisites and packages

```
yum install -y epel-release
yum install -y ansible git
```

## Getting the ansible roles

```
cd /etc/ansible/roles
git clone https://github.com/zwindler/centos7-ovirt-allinone
git clone https://github.com/zwindler/centos7-ovirt-enginesetup
```

Side note: answer file for has been generated with command "engine-setup --generate-answer=/tmp/engine-setup-answers.j2"

## Creating top level playbook
```
cd /etc/ansible
cat > ovirt-allinone.yml << EOF
---
- hosts: localhost
  remote_user: root
  roles:
  - centos7-ovirt-allinone
EOF
```

## Executing playbooks

If you want to install oVirt as All In One
```
ansible-playbook ovirt-allinone.yml
```

If you want to launch ovirt engine setup with the default configuration. You can review/change the variables given by opening the generated answer file located at /tmp/engine-setup-answers. 
```
ansible-playbook ovirt-enginesetup.yml
```
