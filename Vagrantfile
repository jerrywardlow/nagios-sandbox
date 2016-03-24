# -*- mode: ruby -*-
# vi: set ft=ruby :

nodes = [
  { hostname: "nagios-server",
    box:      "ubuntu/trusty64",
    config:   "sr_provision.sh"
  },
  { hostname: "nagios-client",
    box:      "ubuntu/trusty64",
    config:   "cl_provision.sh"
  }
]

Vagrant.configure(2) do |config|
  if Vagrant.has_plugin?("vagrant-hostmanager")
    config.hostmanager.enabled = true
  end

# Everything below this comment needs to be reworked and condensed

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
    srv.vm.provision "shell", path: "sr_provision.sh"
  end

  config.vm.define :client do |cl|
    cl.vm.hostname = "nagios-client"
    cl.vm.synced_folder "client/", "/usr/local/nagios/etc", create: true
    cl.vm.provision "shell", path: "cl_provision.sh"
  end
end
