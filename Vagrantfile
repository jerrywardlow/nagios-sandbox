# -*- mode: ruby -*-
# vi: set ft=ruby :

nodes = [
  { hostname: "nagios-server",
    box:      "ubuntu/trusty64",
    config:   "sr_provision.sh",
    ip:       "11",
  },
  { hostname: "nagios-client",
    box:      "ubuntu/trusty64",
    config:   "cl_provision.sh",
    ip:       "22",
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
      nodeconfig.vm.network :private_network, ip: "172.22.22." + node[:ip]
      nodeconfig.vm.synced_folder ".", "/vagrant", disabled: true
      tempdir = node[:hostname].sub("nagios-", "")
      nodeconfig.vm.synced_folder tempdir+"/", "/"+tempdir

      nodeconfig.vm.provider :virtualbox do |vb|
        vb.name = node[:hostname]
        vb.memory = 1024
      end
    end
  end
end
