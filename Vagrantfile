# -*- mode: ruby -*-
# vi: set ft=ruby :

$script = <<SCRIPT
sudo growpart /dev/vda 1
sudo resize2fs /dev/vda1
SCRIPT

Vagrant.configure(2) do |config|
  config.vm.box = "Fedora-22"
  config.vm.hostname = "devstack"
  config.vm.post_up_message = "Devstack Up!"
  config.ssh.forward_agent = true
  config.vm.network "forwarded_port", guest: 80, host: 8080, auto_correct: true
  config.vm.network "forwarded_port", guest: 5000, host: 5000, auto_correct: true
  config.vm.network "forwarded_port", guest: 9696, host: 9696, auto_correct: true
  config.vm.network "forwarded_port", guest: 8774, host: 8774, auto_correct: true
  config.vm.network "forwarded_port", guest: 35357, host: 35357, auto_correct: true
  config.vm.synced_folder ".", "/vagrant", disabled:true
  config.vm.network :private_network, ip: '10.200.16.10'
  config.vm.network :private_network, ip: '10.200.16.11'
  config.vm.provider "libvirt" do |lv|
      lv.memory = 6144
      lv.cpus = 2
  end
  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "site.yml"
    ansible.host_key_checking = false
    ansible.raw_ssh_args = ['-o ForwardAgent=yes']
  end
end
