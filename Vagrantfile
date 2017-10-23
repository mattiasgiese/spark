# -*- mode: ruby -*-
# vi: set ft=ruby :
Vagrant.configure("2") do |config|
  config.vbguest.auto_update = false
  config.vm.box = "archlinux/archlinux"
  config.vm.box_check_update = false
  config.vm.provider "virtualbox" do |vb|
    # Display the VirtualBox GUI when booting the machine
    vb.gui = false
  
    # Customize the amount of memory on the VM:
    vb.memory = "2048"
  end
  config.vm.provision "shell", inline: <<SCRIPT
echo Installing python
pacman -S --noconfirm --needed python
#pacman-key --init
#pacman-key -u --refresh-keys
SCRIPT
  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "testing.yml"
    ansible.config_file = "ansible.cfg"
    ansible.verbose = "vvv"
    ansible.become_user = 'root'
    ansible.ask_become_pass = true
    ansible.extra_vars = {
      vagrant_testing: true,
      dotfiles_ssh_key: '/home/mattias/.ssh/github_test'
    }
  end
end
