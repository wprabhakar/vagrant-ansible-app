# Defines our Vagrant environment
#
# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  # create mgmt node
  config.vm.define :mgmt do |mgmt_config|
      mgmt_config.vm.box = "ubuntu/trusty64"
      mgmt_config.vm.hostname = "mgmt"
      mgmt_config.vm.network :private_network, ip: "10.10.10.1"
#      mgmt_config.vm.provision :shell, path: "bootstrap-mgmt.sh"
  end

  config.vm.define "web1" do |node|
      node.vm.box = "ubuntu/trusty64"
      node.vm.hostname = "web1"
      node.vm.network :private_network, ip: "10.10.10.20"
      node.vm.network "forwarded_port", guest: 80, host: "5000"
      node.vm.provider "virtualbox" do |vb|
#        vb.memory = "256"
        vb.customize ["modifyvm", :id, "--cpuexecutioncap", "100"]
#        vb.cpu = `sysctl -n hw.logicalcpu`.to_i
      end
      node.vm.provision :shell, path: "bootstrap-web.sh"
      node.vm.provision "ansible" do |ansible|
        ansible.playbook = "setup.yml"
      end
  end

end
