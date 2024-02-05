# -*- mode: ruby -*-
# vi: set ft=ruby :

UBUNTU_IMAGE = "bento/ubuntu-22.04"
CENTOS_IMAGE = "centos/8"
DEBIAN_IMAGE = "debian/jessie64"

Vagrant.configure("2") do |config|
    (1..3).each do |i|     
        config.vm.define "ubuntu-node#{i}" do |subconfig|
            subconfig.vm.box = "bento/ubuntu-22.04" 
            subconfig.vm.hostname = "ubuntu-node#{i}"       
            subconfig.vm.network :private_network, ip: "192.168.56.#{i + 10}"     
	        subconfig.vm.provision :hosts, :sync_hosts => true
            subconfig.vm.provision "shell", inline: <<-EOC
                sudo sed -i -e "\\,PasswordAuthentication no, s,PasswordAuthentication no,PasswordAuthentication yes,g" /etc/ssh/sshd_config
                sudo service ssh restart
            EOC
 
        end
    end

    (0..1).each do |i|
        config.vm.define "centos-node#{i}" do |subconfig|
            subconfig.vm.box = CENTOS_IMAGE
            subconfig.vm.hostname = "centos-node#{i}"
            subconfig.vm.network :private_network, ip: "192.168.56.#{i + 14}"               
            subconfig.vm.provision :hosts, :sync_hosts => true
            subconfig.vm.provision "shell", inline: <<-EOC
                sudo sed -i -e "\\,PasswordAuthentication no, s,PasswordAuthentication no,PasswordAuthentication yes,g" /etc/ssh/sshd_config
                sudo service sshd restart
            EOC
        end
    end
end	
