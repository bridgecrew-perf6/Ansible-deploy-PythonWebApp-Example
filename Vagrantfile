# -*- mode: ruby -*-
# vim: set ft=ruby :

$ssh_auth = <<SCRIPT
sed -i 's/PasswordAuthentication no/PasswordAuthentication yes/g' /etc/ssh/sshd_config
systemctl restart sshd
SCRIPT

Vagrant.configure(2) do |config|

  config.vm.define "pythonwebapp" do |subconfig|
    subconfig.vm.box = "centos/7"
    subconfig.vm.hostname="pythonwebapp"
    subconfig.vm.network "forwarded_port", guest: 80, host: 8080
    subconfig.vm.network :private_network, ip: "192.168.13.13"
    subconfig.vm.provision "shell", inline: $ssh_auth
	  config.ssh.forward_agent = true
    subconfig.vm.provider "virtualbox" do |vb|
      vb.memory = "2048"
      vb.cpus = "2"
    end
  end

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "playbook.yaml"
  end

end
