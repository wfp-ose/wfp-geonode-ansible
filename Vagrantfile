# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|

  config.vm.box = "centos/6.4"

  config.vm.network "forwarded_port", guest: 80, host: 8000
  config.vm.network "forwarded_port", guest: 8080, host: 8080
  config.vm.network "forwarded_port", guest: 8180, host: 8180
  config.vm.network "forwarded_port", guest: 8280, host: 8280
  config.vm.network "forwarded_port", guest: 5432, host: 5432

  config.vm.provider "virtualbox" do |vb|\
      vb.gui = true
      vb.cpus = 4
      vb.memory = 8192
  end

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "test.yml"
    ansible.host_key_checking = false
    ansible.verbose = "v"
    ansible.raw_arguments = [
      "--extra-vars=@extra_vars/env/vagrant.yml",  # Deploying production to vagrant
      "--extra-vars=@extra_vars/sys/production.yml",
      "--extra-vars=@secret.yml"
    ]
  end

end
