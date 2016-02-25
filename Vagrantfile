# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|
  if Vagrant.has_plugin?("vagrant-hostmanager")
    config.hostmanager.enabled = true
    config.hostmanager.ip_resolver = proc do |vm, resolving_vm|
      if vm.id
        `VBoxManage guestproperty get #{vm.id} "/VirtualBox/GuestInfo/Net/1/V4/IP"`.split()[1]
      end
    end
  end

  config.vm.box = "ubuntu/trusty64"

  config.vm.provider "virtualbox" do |v|
    v.cpus = 2
    v.memory = 1024
  end

  config.vm.network :private_network, type: "dhcp"

  config.vm.define :server do |srv|
    srv.vm.hostname = "nagios-server"
    srv.vm.synced_folder "server/", "/usr/local/nagios/etc", create: true
    srv.vm.network "forwarded_port", guest: 80, host: 8080
    srv.vm.provision "shell", path: "server-provision"
  end

  config.vm.define :client do |cl|
    cl.vm.hostname = "nagios-client"
    cl.vm.synced_folder "client/", "/usr/local/nagios/etc", create: true
    cl.vm.provision "shell", path: "client-provision"
  end
end
