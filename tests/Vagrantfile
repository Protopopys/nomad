# -*- mode: ruby -*-
# vi: set ft=ruby :

BOX_IMAGE = "geerlingguy/ubuntu1804"
NODE_COUNT = 6
SUDO_COMMAND = "sudo -H %c"

Vagrant.configure("2") do |config|
  (1..NODE_COUNT).each do |i|
    config.vm.define "node#{i}" do |node|
      node.vm.box = BOX_IMAGE
      node.ssh.sudo_command = SUDO_COMMAND
      node.vm.hostname = "node#{i}"
      node.vm.network :private_network, ip: "10.1.131.#{i + 10}"
      # ssh settings
      node.ssh.insert_key = false
      node.ssh.private_key_path = ["~/.ssh/id_rsa", "~/.vagrant.d/insecure_private_key"]
      node.vm.provision "file", source: "~/.ssh/id_rsa.pub", destination: "~/.ssh/authorized_keys"
      config.vm.provider "virtualbox" do |v|
        v.memory = 2048
        v.cpus = 2
      end
    end
  end
end