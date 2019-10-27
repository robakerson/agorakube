# -*- mode: ruby -*-
# vi: set ft=ruby :

$script = <<-SCRIPT
#!/bin/bash
export DEBIAN_FRONTEND=noninteractive
if which ansible-playbook >/dev/null; then
  echo "Ansible is already installed"
else
  apt-get update
  apt-get install -yqq git software-properties-common
  apt-add-repository --yes --update ppa:ansible/ansible
  apt-get install -yqq ansible
fi
cd /vagrant
ansible-playbook -i hosts.vagrant agorakube.yaml
if [ -f /root/agorakube-info.txt ]; then
  cat /root/agorakube-info.txt
fi
SCRIPT

Vagrant.configure("2") do |config|
  # Node1 Block START
  #config.vm.define "node1" do |node1|
  #    node1.vm.box = "bento/ubuntu-18.04"
  #    node1.vm.network "private_network", ip: "10.0.0.11"
  #    node1.vm.hostname = "node1"
  #    node1.vm.provider "virtualbox" do |vb|
  #        vb.customize ["modifyvm", :id, "--memory", 2048]
  #        vb.customize ["modifyvm", :id, "--name", "node1"] 
  #    end
  #end
  # Node1 Block END

  # Node2 Block START
  #config.vm.define "node2" do |node2|
  #    node2.vm.box = "bento/ubuntu-18.04"
  #    node2.vm.network "private_network", ip: "10.0.0.12"
  #    node2.vm.hostname = "node2"
  #    node2.vm.provider "virtualbox" do |vb|
  #        vb.customize ["modifyvm", :id, "--memory", 2048]
  #        vb.customize ["modifyvm", :id, "--name", "node2"] 
  #    end
  #end
  # Node2 Block END

  config.vm.define "deploy" do |deploy|
      deploy.vm.box = "bento/ubuntu-18.04"
      deploy.vm.network :private_network, ip: "10.0.0.10"
      deploy.vm.hostname = "deploy"
      deploy.vm.provider "virtualbox" do |vb|
          vb.customize ["modifyvm", :id, "--memory", 2048]
          vb.customize ["modifyvm", :id, "--name", "deploy"] 
      end
      deploy.vm.provision :shell, inline: $script
  end
end
