# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "bento/centos-7.4"
  # config.vm.box_check_update = false
  config.vm.network "private_network", type: "dhcp"
  # config.vm.synced_folder "../data", "/vagrant_data"
  # config.vm.provider "virtualbox" do |vb|
  #   vb.gui = true
  #   vb.memory = "1024"
  # end
  config.vm.provision "ansible_local" do |ansible|
    ansible.compatibility_mode = "2.0"
    ansible.playbook = "provisioning/playbook.yml"
    ansible.extra_vars = "override_vars.yml"
  end
end
