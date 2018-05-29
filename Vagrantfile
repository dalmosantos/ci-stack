# -*- mode: ruby -*-
# vi: set ft=ruby :


Vagrant.configure("2") do |config|


  config.vm.box = "ubuntu/xenial64"
  config.vm.box_check_update = true
  config.vm.provider "virtualbox" do |vb|
     vb.customize ["modifyvm", :id, "--memory", "3072" ]
     vb.customize ["modifyvm", :id, "--cpus", "2" ]
     vb.customize ["setextradata", "global", "GUI/SuppressMessages", "all" ]
    end

  (1..2).each do |i|
    config.vm.define "docker#{i}" do |node|
      node.vm.hostname = "docker#{i}"
      node.vm.network :private_network, :ip => "192.168.33.10#{i}"
	  #node.vm.network "forwarded_port", guest: 80, host: 9999
      #node.vm.network "forwarded_port", guest: 443, host: 443
      #node.vm.network "forwarded_port", guest: 4444, host: 4444
	  #node.vm.network "forwarded_port", guest: 5432, host: 5432
      #node.vm.network "forwarded_port", guest: 8010, host: 8010
      #node.vm.network "forwarded_port", guest: 8080, host: 8080
      #node.vm.network "forwarded_port", guest: 8081, host: 8081
      #node.vm.network "forwarded_port", guest: 8082, host: 8082
      #node.vm.network "forwarded_port", guest: 8090, host: 8090
      #node.vm.network "forwarded_port", guest: 9000, host: 9000
      #node.vm.network "forwarded_port", guest: 9443, host: 9443
      #node.vm.network "forwarded_port", guest: 29148, host: 29418
    end
  end

  config.vm.provision "shell", inline: <<-SHELL
    apt-get clean
    apt-get update
    apt-get remove docker docker-engine docker.io -y
    curl -fsSL get.docker.com -o get-docker.sh
    chmod +x get-docker.sh
    bash get-docker.sh
    docker --version
    curl -L https://github.com/docker/compose/releases/download/1.21.2/docker-compose-$(uname -s)-$(uname -m) -o /usr/local/bin/docker-compose
    chmod +x /usr/local/bin/docker-compose
    docker-compose --version
   SHELL
end