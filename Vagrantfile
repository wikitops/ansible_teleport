# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  config.vm.box = "ubuntu/xenial64"

  # Teleport Master
  (1..1).each do |i|
    config.vm.provider "virtualbox" do |vb|
      vb.memory = 2048
      vb.cpus = 2
    end

    config.vm.define "teleport0#{i}" do |server|
      server.vm.hostname = "teleport0#{i}"
      server.vm.network "private_network", ip: "10.0.0.15#{i}"
    end
  end

  # Teleport Worker
  (1..3).each do |i|
    config.vm.provider "virtualbox" do |vb|
      vb.memory = 1024
      vb.cpus = 2
    end

    config.vm.define "worker0#{i}" do |server|
      server.vm.hostname = "worker0#{i}"
      server.vm.network "private_network", ip: "10.0.0.16#{i}"
    end
  end

  # Provision
  config.vm.provision "shell", path: "provision.sh"
  config.vm.provision "file", source: "~/.ssh/id_rsa.pub", destination: "/home/vagrant/.ssh/authorized_keys"

end
