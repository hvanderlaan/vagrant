# -*- mode: ruby -*-
# vi: ft=ruby :

# file   : Vagrantfile
# purpose: deploy vagrant vm's
#
# author : harald van der laan
# date   : 2018/02/28
# version: v1.0.0

# vagrant specific 
Vagrant.require_version ">= 2.0.0"
VAGRANT_API_FILE_VERSION = "2"

# loading cluster configuration
require 'yaml'
server = YAML.load_file('server.yaml')

# main vagrant configuration
Vagrant.configure(VAGRANT_API_FILE_VERSION) do |config|
    server.each do |node|
        config.vm.define node['name'] do |nodecfg|
            nodecfg.vm.box = node['box']
            nodecfg.vm.hostname = node['hostname']
            nodecfg.vm.network :private_network, ip: node['ip']

            nodecfg.vm.provider:virtualbox do |vbox|
                vbox.customize [
                    "modifyvm", :id,
                    "--groups", node['group'],
                    "--memory", node['ram'],
                    "--cpus", node['cpus'],
                    "--name", node['name'],
                    "--vrde", node['vrde'],
                    "--vrdeport", node['vrdeport'],
                ]
            end

            nodecfg.vm.provision :ansible do |ansible|
                ansible.playbook = node['playbook']
            end
        end
    end
end
