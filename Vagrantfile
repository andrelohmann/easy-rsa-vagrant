# -*- mode: ruby -*-
# vi: set ft=ruby :

#require necessary plugins
required_plugins = %w( vagrant-vbguest )
required_plugins.each do |plugin|
  system "vagrant plugin install #{plugin}" unless Vagrant.has_plugin? plugin
end

Vagrant.configure("2") do |config|

  config.vm.box = "ubuntu/xenial64" # 16.04
  config.vm.provider "virtualbox" do |vb|
    vb.memory = "512"
    vb.cpus = "1"
  end
  config.vm.synced_folder ".", "/vagrant", disabled: true
  config.vm.synced_folder "ansible", "/vagrant/ansible", create: true, owner: "vagrant", group: "vagrant", mount_options: ["dmode=777,fmode=777"]
  config.vm.synced_folder "ca", "/home/vagrant/ca", create: true, owner: "vagrant", group: "vagrant", mount_options: ["dmode=777,fmode=777"]
  config.vbguest.auto_update = true
  config.vm.provision "ansible_local" do |ansible|
    ansible.install = true
    ansible.install_mode = :pip
    ansible.version = "latest"
    ansible.playbook = "ansible/playbook.yml"
    ansible.galaxy_role_file = "ansible/requirements.yml"
  end
end
