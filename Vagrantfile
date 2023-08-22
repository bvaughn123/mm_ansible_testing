# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.ssh.username = "vagrant"
  config.ssh.password = "vagrant"
  config.vm.synced_folder '.', '/vagrant', disabled: true

  
  # VirtualBox
  config.vm.define "virtualbox" do |virtualbox|
    virtualbox.vm.hostname = "vbox.rocky8.local"
    config.vm.box = "bento/rockylinux-8"
    virtualbox.vm.network :private_network, ip: "192.168.58.42"

    config.vm.provider :virtualbox do |vbx_roxcky|
      vbx_roxcky.gui = true
      vbx_roxcky.memory = 8096
      vbx_roxcky.cpus = 4
      vbx_roxcky.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
      vbx_roxcky.customize ["modifyvm", :id, "--ioapic", "on"]
    end
    
 
    config.vm.provision "ansible" do |ansible|
      ansible.playbook = "ansible/certificates/main.yml"
      ansible.verbose  = "v"
      #ansible.skip_tags = ["pip","cert","dirs"]
    end

    config.vm.provision "ansible" do |ansible|
      ansible.playbook = "ansible/main.yml"
      ansible.verbose  = "v"
    end
  
  end

end
