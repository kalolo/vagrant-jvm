# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

require 'yaml'

vconfig = YAML.load_file "conf/vagrant_config.yml"

box_hostname = vconfig['boxconfig']['name']
box_ip       = vconfig['boxconfig']['ip']
box_ram      = vconfig['boxconfig']['ram']
box_os       = vconfig['boxconfig']['box']

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  config.vm.box = box_os
  config.vm.hostname = box_hostname
  config.vm.network "private_network", ip: box_ip
  config.hostsupdater.aliases = ["featur.dev"]
  #config.vm.network "forwarded_port", guest: 80, host: 8080

  config.vm.provider "virtualbox" do |v|
      v.name = box_hostname
      v.memory = box_ram
  end

  config.vm.provision :ansible do |ansible|
    ansible.playbook = "app/playbook.yml"
  end

end
