# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  config.vm.define "server-01" do |client|
    client.vm.box = "bento/ubuntu-18.04"
    client.vm.hostname = "server-01"
    client.vm.network "private_network", type: "dhcp"
  end

  config.vm.define "server-02" do |server|
    server.vm.box = "bento/ubuntu-18.04"
    server.vm.hostname = "server-02"
    server.vm.network "private_network", type: "dhcp"
    server.vm.provision "shell", inline: <<-SHELL
      sudo apt update
      sudo apt install wireguard
    SHELL
  end

  config.vm.provider "virtualbox" do |vb|
    vb.memory = "1024"
  end

end
