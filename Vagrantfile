# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.synced_folder "./cyan_memorabilia", "/home/vagrant/cyan_memorabilia"
  config.vm.provider :virtualbox do |vb|
    vb.customize ['modifyvm', :id, '--usb', 'on']
    vb.customize ['usbfilter', 'add', '0', '--target', :id, '--name', 'Ardunio', '--vendorid', '0x2341', 
                  '--productid', '0x0043']
    end
end
