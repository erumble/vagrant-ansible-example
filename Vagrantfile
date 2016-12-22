# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
vagrantfile_api_version = "2"

# directory name is used for the VM hostname, and ansible role name
base_dir = File.basename(File.expand_path(File.dirname __FILE__))

# definitions for the machines provisioned by this vagrant file
box_params = {
  box: 'erumble/centos7-x64',
  hostname: "#{base_dir}.dev",
  ip: '192.168.8.100',
  playbook: 'ansible/playbook.yml'
}

# make the vagrant machine(s)
Vagrant.configure(vagrantfile_api_version) do |config|
  config.vm.define box_params.fetch(:hostname) do |box|

    # specify the box, hostname, and ip address
    box.vm.box = box_params.fetch :box
    box.vm.hostname = box_params.fetch :hostname
    box.vm.network :private_network, ip: box_params.fetch(:ip)

    # forward the ssh agent for things like git
    box.ssh.forward_agent = true

    # provision the thing
    box.vm.provision :ansible do |ansible|
      ansible.playbook = box_params.fetch :playbook
      ansible.verbose = 'vv'
    end

  end # config.vm.define
end # Vagrant.configure
