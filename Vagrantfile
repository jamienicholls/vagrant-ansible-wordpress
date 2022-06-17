# -*- mode: ruby -*-
# vi: set ft=ruby :
Vagrant.configure("2") do |config|
  config.vm.box = "generic/rocky8"
  config.vm.box_check_update = true

  config.vm.define "webapp1" do |server|
      server.vm.hostname = "webapp1"
      server.vm.network "private_network", ip: "192.168.50.30"
      server.vm.network "forwarded_port", guest: 8080, host: 8080
      server.vm.provider "virtualbox" do |v|
          v.name = "webapp1"
          v.memory = 1024
          v.cpus = 1
          v.linked_clone = true
          v.gui = false
      end
      config.vm.synced_folder "./provisioning", "/home/vagrant/provisioning", create: false, type: "rsync", rsync__auto: true, rsync__args: ["--verbose", "--archive", "-z", "--copy-links"]
      server.vm.provision "ansible_local" do |ansible|
          ansible.provisioning_path = "/home/vagrant/provisioning/"
          ansible.extra_vars = { ansible_python_interpreter:"/usr/bin/python3" }
          ansible.playbook = "web.yml"
      end
  end

  config.vm.define "db1" do |server|
      server.vm.hostname = "db1"
      server.vm.network "private_network", ip: "192.168.50.32"
      server.vm.provider "virtualbox" do |v|
          v.name = "db1"
          v.memory = 1024
          v.cpus = 1
          v.linked_clone = true
          v.gui = false
      end
      config.vm.synced_folder "./provisioning", "/home/vagrant/provisioning", create: false, type: "rsync", rsync__auto: true, rsync__args: ["--verbose", "--archive", "-z", "--copy-links"]
      server.vm.provision "ansible_local" do |ansible|
          ansible.provisioning_path = "/home/vagrant/provisioning/"
          ansible.extra_vars = { ansible_python_interpreter:"/usr/bin/python3" }
          ansible.playbook = "database.yml"
      end
  end
end
