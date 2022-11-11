# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  config.vm.box = "hashicorp/bionic64"
  config.vm.hostname = "enve-labs-linux1-sa-vm"
  config.vm.network :public_network, bridge: 'Prueba'
  config.vm.network "forwarded_port", guest: 80, host: 1234
  config.vm.network "forwarded_port", guest: 8080, host: 8081
  config.vm.network "forwarded_port", guest: 3306, host: 3306 

  config.vm.synced_folder "./shared", "/home/vagrant/shared"

  config.vm.provider :virtualbox do |vb|
    vb.name = "enve-labs-linux1-sa-vm"
  end

  config.vm.provision "shell", inline: <<-SHELL
      sudo apt-get remove docker docker-engine docker.io
      sudo apt-get update && sudo apt-get install -y apt-transport-https ca-certificates software-properties-common curl jq
      curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
      sudo apt-key fingerprint 0EBFCD88
      sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
      sudo apt-get update
      sudo apt-get install -y docker-ce
  SHELL

end
