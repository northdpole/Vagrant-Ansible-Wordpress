# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
	config.vm.provider "virtualbox" do |v|
		v.gui = true
	end
	config.vm.box = "ubuntu/trusty64"
	config.vm.network :private_network, type: "dhcp"
	config.vm.provision "ansible" do |ansible|
		ansible.verbose = "v"
		ansible.playbook = "setup.yml"
		ansible.host_key_checking = "false"
		ansible.limit = "all"
	end
	config.vm.provision "shell" do |shell| shell.inline = "wget -c -P /vagrant/ https://wordpress.org/latest.zip && wget -c -P /vagrant/ https://github.com/zaproxy/zaproxy/releases/download/2.5.0/ZAP_2.5.0_Linux.tar.gz&& sleep 4 && reboot"
	end
	config.vm.provider :virtualbox do |vb|
		vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
		vb.customize ["modifyvm", :id, "--natdnsproxy1", "on"]
	end
	config.vm.synced_folder ".", "/vagrant", owner:"www-data", group:"www-data", mount_options:["dmode=775", "fmode=775"]
end
