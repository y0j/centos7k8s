# -*- mode: ruby -*-
# vi: set ft=ruby :
# vagrant plugin install vagrant-disksize (for disksize.size)

Vagrant.configure("2") do |config|

  config.vm.define :master do |master|
    master.vm.provider :virtualbox do |vb|
      vb.name = "master"
      vb.memory = 2048
      vb.cpus = 2
    end
    master.vm.box = "centos/7"
    #master.disksize.size = "10GB"
    master.vm.hostname = "master"
    master.vm.network :private_network, ip: "10.0.0.10"
  end

  %w{worker1 worker2}.each_with_index do |name, i|
    config.vm.define name do |node|
      node.vm.provider "virtualbox" do |vb|
        vb.name = "node#{i + 1}"
        vb.memory = 1024
        vb.cpus = 1
      end
      node.vm.box = "centos/7"
      #node.disksize.size = "10GB"
      node.vm.hostname = name
      node.vm.network :private_network, ip: "10.0.0.#{i + 11}"
    end
  end

  config.vm.provision "shell", inline: 'yum update -y'
  config.vm.provision "shell", inline: 'yum install -y vim git bash-completion'
  config.vm.provision "shell", path: "setup-docker.sh"
  config.vm.provision "shell", path: "setup-kubetools.sh"
end
