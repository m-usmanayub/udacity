# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "centos/7"
  config.ssh.insert_key = false
  config.vm.synced_folder ".", "/vagrant", disabled: true
  config.vm.provider :virtualbox do |vb|
    vb.memory = 512
  end
  
  config.vm.define "node1" do |node|
    node.vm.hostname = "node1.cw.net"
    node.vm.network :private_network, ip: "192.168.60.11"
  end

  config.vm.define "node2" do |node|
    node.vm.hostname = "node2.cw.net"
    node.vm.network :private_network, ip: "192.168.60.12"
  end

  config.vm.define "node3" do |node|
    node.vm.hostname = "node3.cw.net"
    node.vm.network :private_network, ip: "192.168.60.13"
  end
end

