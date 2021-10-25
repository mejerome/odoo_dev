# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "bento/ubuntu-20.04"
  config.ssh.insert_key = false
  config.vm.synced_folder ".", "/vagrant"
  config.vm.provider "virtualbox" do |vb|
    vb.memory = 1024
    vb.cpus = 1
    vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    vb.customize ["modifyvm", :id, "--ioapic", "on"]
  end

  config.vm.define "odoo" do |odoo|
    odoo.vm.hostname = "odoo"
    odoo.vm.network "public_network"
    odoo.vm.provision "ansible_local" do |ansible|
      ansible.playbook = "playbook/main.yml"
      ansible.galaxy_role_file = "playbook/requirements.yml"
      ansible.galaxy_roles_path = "/home/vagrant/ansible/roles"
    end
  end
end