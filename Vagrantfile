# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  # Base VM OS configuration.
  config.vm.box = "ubuntu/trusty64"
  config.ssh.insert_key = false
  config.vm.synced_folder '.', '/vagrant', disabled: true

  # General VirtualBox VM configuration.
  config.vm.provider :virtualbox do |v|
    v.memory = 1024
    v.cpus = 2
    v.linked_clone = true
  end

  # Wordpress.
  config.vm.define "wordpress" do |wordpress|
    wordpress.vm.hostname = "wordpress.dev"
    wordpress.vm.network :private_network, ip: "192.168.20.21"
  end

  # Provisioning.
  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "dev.yml"
    ansible.inventory_path = "inventories/vagrant/inventory"
    ansible.limit = "all"
    ansible.extra_vars = {
      ansible_ssh_user: 'vagrant',
      ansible_ssh_private_key_file: "~/.vagrant.d/insecure_private_key"
    }
  end
end
