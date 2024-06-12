# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
# Adjust this variable to modify the count of worker nodes
node_count = 2
Vagrant.configure("2") do |config|
  config.ssh.insert_key = false
  config.vbguest.auto_update = false
  # Define VM
  config.vm.box = "base"
  # Define Virtualization engine 
  config.vm.provider "virtualbox" do |vb|
    vb.customize ["modifyvm", :id, "--groups", "/k8s-playground"]
    vb.memory = 2048
    vb.cpus = 2
    vb.linked_clone = true
  end

  config.vm.define "master" do |node|
    node.vm.hostname = "master"
    node.vm.network "private_network", ip: "192.168.56.10"
    node.vm.provider "virtualbox" do |vb|
      vb.name = "master"
    end
    node.vm.provision "ansible" do |ansible|
      ansible.playbook = "playbooks/master-playbook.yml"
    end
  end

  (1..node_count).each do |i|
    hostname = "node-#{'%02d' % i}"
    config.vm.define "#{hostname}" do |node|
      node.vm.hostname = "#{hostname}"
      node.vm.network "private_network", ip: "192.168.56.#{10 + i}"
      node.vm.provider "virtualbox" do |vb|
        vb.name = "#{hostname}"
      end
      node.vm.provision "ansible" do |ansible|
        ansible.playbook = "playbooks/node-playbook.yml"
      end
    end
  end
  # config.vm.provision "shell", 
  #   path: "update-kubelet-config.sh",
  #   args: ["eth1"], 
  #   privileged: false
end
