# -*- mode: ruby -*-
# vi: set ft=ruby :

# load configs
require 'yaml'
current_dir    = File.dirname(File.expand_path(__FILE__))
configs        = YAML.load_file("#{current_dir}/config.yml")
vagrant_config = configs['configs']

# require necessary plugins
required_plugins = %w( vagrant-vbguest )
required_plugins.each do |plugin|
  system "vagrant plugin install #{plugin}" unless Vagrant.has_plugin? plugin
end

Vagrant.configure(2) do |config|

  config.vm.box = "ubuntu/bionic64" # 18.04

  config.vm.provider "virtualbox" do |vb|
    vb.memory = vagrant_config['memory']
    vb.cpus = vagrant_config['cpus']
  end

  # auto update guest additions
  config.vbguest.auto_update = true

  config.vm.synced_folder ".", "/vagrant", disabled: true
  config.vm.synced_folder "ansible", "/vagrant/ansible", create: true, owner: "vagrant", group: "vagrant", mount_options: ["dmode=775,fmode=775"]
  config.vm.synced_folder "ca", "/home/vagrant/ca", create: true, owner: "vagrant", group: "vagrant", mount_options: ["dmode=775,fmode=775"]

  config.vm.provision "ansible_local" do |ansible|
    ansible.install = true
    ansible.install_mode = :default # install latest ansible from ppa package
    ansible.playbook = "ansible/playbook.yml"
    ansible.galaxy_role_file = "ansible/requirements.yml"
  end
end
