# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
    amountNodes = 3

    config.landrush.enabled = true
    config.landrush.tld = "lab"

    config.vm.box = "debian/stretch64"

    config.vm.provider "virtualbox" do |vm|
      vm.memory = 1024
    end

	(1..amountNodes).each do |id|
        config.vm.define "node-#{id}" do |node|
            if id == 1
                node.vm.hostname = "swarmManager-1.lab"
            else
                node.vm.hostname = "worker-#{id}.lab"
            end
            if id == amountNodes
                node.vm.provision "ansible" do |ansible|
                    ansible.limit = "all"
                    ansible.playbook = "provision.yml"
                end
            end
        end
    end
end
