# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  config.vm.define "auth-proxy" do |d|
    d.vm.box = "ubuntu/trusty64"
    d.vm.hostname = "auth-proxy"
    # config.vm.network "forwarded_port", guest: 3025, host: 3025
    # config.vm.network "forwarded_port", guest: 3024, host: 3024
    # config.vm.network "forwarded_port", guest: 3080, host: 3080
    # config.vm.network "forwarded_port", guest: 3023, host: 3023
    # config.vm.network "forwarded_port", guest: 3022, host: 3022
    d.vm.network "private_network", ip: "10.100.198.200"
    d.vm.provider "virtualbox" do |v|
      v.memory = 1024
    end
    config.vm.provision "shell", inline: <<-SHELL
    apt-get update
    #apt-get upgrade -y
    apt-get install -y aptitude make
    mkdir -p /var/lib/teleport /etc/teleport
    cp /vagrant/teleport-v2.2.4-linux-amd64-bin.tar.gz /tmp/
    cp /vagrant/teleport.yml /etc/teleport/teleport.yml
    cd /tmp && tar -xvf teleport-v2.2.4-linux-amd64-bin.tar.gz
    cd /tmp/teleport && sudo make install
    sudo su root -c "nohup teleport start --config=/etc/teleport/teleport.yml >> /var/log/teleport.log 2>&1 &"
    SHELL
  end
  config.vm.define "tele-client1" do |d|
    d.vm.box = "ubuntu/trusty64"
    d.vm.hostname = "tele-client1"
    d.vm.network "private_network", ip: "10.100.198.201"
    d.vm.provider "virtualbox" do |v|
      v.memory = 1024
    end
    config.vm.provision "shell", inline: <<-SHELL
    apt-get update
    #apt-get upgrade -y
    apt-get install -y aptitude make
    cp /vagrant/teleport-v2.2.4-linux-amd64-bin.tar.gz /tmp/
    cd /tmp && tar -xvf teleport-v2.2.4-linux-amd64-bin.tar.gz
    cd /tmp/teleport && sudo make install
    sudo su root -c "nohup teleport start --roles=node --token=xxxxxx --auth-server=10.100.198.200:3025 >> /var/log/teleport.log 2>&1 &"
    SHELL
  end
end
