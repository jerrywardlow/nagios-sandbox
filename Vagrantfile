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
  nodes.each do |node|
    config.vm.define node[:hostname] do |nodeconfig|
      nodeconfig.vm.provision :shell, path: node[:config]
      nodeconfig.vm.box = "ubuntu/trusty64"
      nodeconfig.vm.hostname = node[:hostname]
      nodeconfig.vm.network :private_network, type: "dhcp"
      if node[:hostname].include? "server"
        nodeconfig.vm.network "forwarded_port", guest: 80, host: 8080
      end
      nodeconfig.vm.provider :virtualbox do |vb|
        vb.name = node[:hostname]
        vb.memory = 1024
      end
    end
  end
end
