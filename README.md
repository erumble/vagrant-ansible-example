Vagrant Ansible Example
=

### Purpose
This Vagrantfile provisions a CentOS 7 VM using Ansible.

The base image was created by this [Packer template](https://github.com/erumble/packer-templates),
and is hosted on [Atlas](https://atlas.hashicorp.com/erumble/boxes/centos7-x64).

The playbook will set custom facts for use in a subsequent play, and then install Ruby and Nginx through the use of Ansible Roles.

It serves as an example for how to automatically pull down roles from Ansible Galaxy, use them, and how to set custom facts.

### Dependencies
* [Vagrant](https://www.vagrantup.com/)
* [VirtualBox](https://www.virtualbox.org/)
* [Ansible](https://www.ansible.com/)

### Vagrant Commands
* `vagrant status` - Check status of VM in current directory 
* `vagrant global-status` - Check status of all Vagrant VMs
* `vagrant up` - Create and provision VM from "not created" state
* `vagrant up` - Start VM from "poweroff" or "aborted" state
* `vagrant provision` - Rerun the provisioner(s)
* `vagrant halt` - Stop VM from any state, same as turning off a computer
* `vagrant reload` - Turn it off and on again
* `vagrant destroy` - Destroy VM, same as dropping computer down a flight of stairs and shredding the HDD/SSD
* `vagrant ssh` - Log in to the VM
* `vagrant help` - Run it and see
