# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|
  config.vm.box = "ubuntu/trusty64"

  config.vm.provider "virtualbox" do |v|
    v.cpus = 2
    v.memory = 1024

  config.vm.network :private_network, type: "dhcp"
