# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "centos-gui/7"
  config.vm.define "rhcsa"
  config.vm.hostname = "rhelserver.example.com"

  # A specific IP address is required to support NFS - DHCP won't work.
  # http://stackoverflow.com/questions/39354221/how-to-set-up-a-shared-vagrant-directory-on-an-osx-vagrant-box
  # To prevent another Adapter being created Address in range of DHCP
  # server of VirtualBox Host-only Adapter
  config.vm.network "private_network", ip: "172.28.128.3"

  config.vm.synced_folder ".", "/vagrant", type: "nfs"

  config.vm.provider "virtualbox" do |vb|
    vb.name = "rhcsa"

    # Display the VirtualBox GUI when booting the machine
    vb.gui = true
 
    # Customize the amount of memory on the VM:
    vb.memory = "1024"
  end

  config.vm.provision "shell", inline: <<-SHELL
    localectl set-keymap dvorak

    # Graphical interface required for course
    yum -y groupinstall "GNOME Desktop"
    systemctl set-default graphical.target
    systemctl isolate graphical.target
  SHELL
end
