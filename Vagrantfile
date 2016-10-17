# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"
Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  # Create central
  config.vm.define :central do |central_config|
    central_config.vm.box = "centos/7"
    central_config.vm.box_url = "http://cloud.centos.org/centos/7/vagrant/x86_64/images/CentOS-7-x86_64-Vagrant-1605_01.VirtualBox.box"
    central_config.vm.hostname = "central"
    central_config.ssh.forward_agent = true
    central_config.vm.network :private_network, ip: "10.0.15.11"
    central_config.vm.network "forwarded_port", guest: 7767, host: 1234, protocol: "tcp"
    central_config.vm.provider "virtualbox" do |vb|
      vb.memory = "256"
    end
    central_config.vm.synced_folder ".", "/vagrant"

    central_config.vm.provision :ansible do |ansible|
      ansible.verbose = "v"
      ansible.playbook = "site.yml"
      ansible.inventory_path = "vagrant/inventory"
      #ansible.groups = {
      #  "central" => ["centrals", "brokers"],
      #}
    end
  end


  # Create a distributed realm scheduler/poller-reactionner
  (1..1).each do |i|
      config.vm.define "poller#{i}" do |poller_config|
        poller_config.vm.box = "centos/7"
        poller_config.vm.hostname = "poller#{i}"
        poller_config.vm.box_url = "http://cloud.centos.org/centos/7/vagrant/x86_64/images/CentOS-7-x86_64-Vagrant-1605_01.VirtualBox.box"
        poller_config.vm.network :private_network, ip: "10.0.15.#{20+i}"
        poller_config.vm.provider "virtualbox" do |vb|
          vb.memory = "256"
        end
        #poller_config.vm.synced_folder ".", "/vagrant"

        poller_config.vm.provision :ansible do |ansible|
          ansible.verbose = "v"
          ansible.playbook = "site.yml"
          #ansible.groups = {
          #"poller#{i}" => ["pollers"],
          #}
          ansible.inventory_path = "vagrant/inventory"
        end
      end
  end

  # MongoDB
  (1..1).each do |i|
      config.vm.define "mongo#{i}" do |mongo_config|
        mongo_config.vm.box = "centos/7"
        mongo_config.vm.hostname = "poller#{i}"
        mongo_config.vm.box_url = "http://cloud.centos.org/centos/7/vagrant/x86_64/images/CentOS-7-x86_64-Vagrant-1605_01.VirtualBox.box"
        mongo_config.vm.network :private_network, ip: "10.0.15.#{70+i}"
        mongo_config.vm.provider "virtualbox" do |vb|
          vb.memory = "256"
        end
        #mongo_config.vm.synced_folder ".", "/vagrant"

        mongo_config.vm.provision :ansible do |ansible|
          ansible.verbose = "v"
          ansible.playbook = "site.yml"
          #ansible.groups = {
          #"mongo#{i}" => ["mongos"],
          #}
          ansible.inventory_path = "vagrant/inventory"
        end
      end
  end

#  # Create monitored nodes
#  (1..2).each do |i|
#      config.vm.define "node#{i}" do |node_config|
#        node_config.vm.box = "centos/7"
#        node_config.vm.hostname = "node#{i}"
#        node_config.vm.box_url = "http://cloud.centos.org/centos/7/vagrant/x86_64/images/CentOS-7-x86_64-Vagrant-1605_01.VirtualBox.box"
#        node_config.vm.network :private_network, ip: "10.0.15.#{50+i}"
#        node_config.vm.provider "virtualbox" do |vb|
#          vb.memory = "256"
#        end
#        #node_config.vm.synced_folder ".", "/vagrant"
#
#        node_config.vm.provision :ansible do |ansible|
#          ansible.verbose = "v"
#          ansible.playbook = "site.yml"
#          #ansible.groups = {
#          #"node#{i}" => ["nodes"],
#          #}
#	  ansible.inventory_path = "inventory"
#        end
#      end
#  end

  # Create influxDB
  config.vm.define :influx do |influx_config|
    influx_config.vm.box = "centos/7"
    influx_config.vm.box_url = "http://cloud.centos.org/centos/7/vagrant/x86_64/images/CentOS-7-x86_64-Vagrant-1605_01.VirtualBox.box"
    influx_config.vm.hostname = "influxdb"
    influx_config.ssh.forward_agent = true
    influx_config.vm.network :private_network, ip: "10.0.15.13"
    influx_config.vm.provider "virtualbox" do |vb|
      vb.memory = "256"
    end
    influx_config.vm.synced_folder ".", "/vagrant"

    influx_config.vm.provision :ansible do |ansible|
      ansible.verbose = "v"
      ansible.playbook = "site.yml"
      ansible.inventory_path = "vagrant/inventory"
    end
  end


end
