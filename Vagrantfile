# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
vagrantfile_api_version = "2"

# directory name is used for the VM hostname, and ansible role name
base_dir = File.basename(File.expand_path(File.dirname __FILE__))

# definitions for the machines provisioned by this vagrant file
box_params = {
    box: 'erumble/centos7-x64',
    hostname: "#{base_dir.gsub('_', '-')}.dev",
    hostname_aliases: ["api.#{base_dir.gsub('_', '-')}.dev"],
    playbook: 'ansible/playbook.yml',
    galaxy_role_file: 'ansible/dependencies.yml'
}

# make the vagrant machine(s)
Vagrant.configure(vagrantfile_api_version) do |config|
  config.vm.define box_params.fetch(:hostname) do |box|

    # specify the box, hostname, and ip address
    box.vm.box = box_params.fetch :box
    box.vm.hostname = box_params.fetch :hostname

    # create a random IP address using the hostname as a seed
    prng = Random.new(box_params.fetch(:hostname).bytes.join.to_i)
    box.vm.network :private_network, ip: "192.168.#{prng.rand(5...255)}.#{prng.rand(2...255)}"

    # configure /etc/hosts on the host OS
    box.hostsupdater.aliases = box_params[:hostname_aliases] if Vagrant.has_plugin? 'vagrant-hostsupdater'

    # give the box some resources
    # box.vm.provider 'virtualbox' do |v|
    #   v.memory = 2048
    #   v.cpus = 2
    # end

    # forward the ssh agent for things like git
    box.ssh.forward_agent = true

    # mount the base dir in /home/vagrant/src instead of /vagrant
    config.vm.synced_folder ".", "/vagrant", disabled: true
    config.vm.synced_folder ".", "/home/vagrant/src/#{base_dir}", owner: 'vagrant', group: 'vagrant'

    # provision the thing
    box.vm.provision :ansible do |ansible|
      ansible.playbook = box_params.fetch :playbook
      ansible.verbose = 'vv'
      ansible.galaxy_role_file = box_params[:galaxy_role_file] # the default is nil
      ansible.extra_vars = {
          etc_hosts: box_params[:hostname_aliases] ? box_params[:hostname_aliases].map{ |hostname| { hostname: hostname, ip: '127.0.0.1' } } : []
      }
    end

  end # config.vm.define
end # Vagrant.configure
