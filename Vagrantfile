# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.define "develop" do |node|
    node.vm.box = "bento/centos-7.5"
    node.vm.hostname = "develop"
    node.vm.box_check_update = false
    node.vm.network "forwarded_port", guest: 80, host: 8040
    node.vm.network "private_network", ip: "192.168.50.10"
    node.vm.synced_folder "./data", "/data/vagrant"
    node.vm.provider "virtualbox" do |vb|
      vb.name = "develop"
      vb.cpus = 2
      vb.memory = "4096"
    end
  end
  config.vm.provision "shell", inline: <<-SHELL
    # ansible install
    sudo yum install epel-release -y
    sudo yum install ansible --enablerepo=epel-testing -y

    # package install
    sudo yum install git vim -y

    # init config
    cp /data/vagrant/init/.netrc ~/
    cp /data/vagrant/init/.gitconfig ~/
    cp /data/vagrant/init/sshkey/* ~/
  SHELL
end
