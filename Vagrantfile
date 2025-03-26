# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.define "vm1" do |vm1|
    vm1.vm.box = "bento/ubuntu-22.04"
    vm1.vm.network "private_network", ip: "192.168.56.10"
    vm1.vm.hostname = "k3s-master-node"
  end
   config.vm.define "vm2" do |vm2|
    vm2.vm.box = "bento/ubuntu-22.04"
    vm2.vm.network "private_network", ip: "192.168.56.11"
    vm2.vm.hostname = "k3s-worker-node-1"
  end
   config.vm.define "vm3" do |vm3|
    vm3.vm.box = "bento/ubuntu-22.04"
    vm3.vm.network "private_network", ip: "192.168.56.12"
    vm3.vm.hostname = "k3s-worker-node-2"
  end
  config.vm.provider "virtualbox" do |vb|
    vb.memory = "2048"
    vb.cpus = "2"
  end
end
