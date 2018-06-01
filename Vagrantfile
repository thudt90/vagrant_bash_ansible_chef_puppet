# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|
  config.vm.box = 'bento/ubuntu-16.04'
  config.ssh.insert_key = false

  config.vm.provider :virtualbox do |vb|
    vb.memory = 256
  end

  config.vm.define :bash do |bash|
    bash.vm.network :forwarded_port, guest: 80, host: 8080
    bash.vm.provision :shell, path: 'provisioners/bash/install_apache2.sh'
  end

  config.vm.define :ansible do |ansible|
    ansible.vm.net :private_network, ip: '192.168.33.112'
  end

  config.vm.define :chef do |chef|
    chef.vm.net :private_network, ip: '192.168.33.113'
  end

  config.vm.define :puppet do |puppet|
    puppet.vm.net :private_network, ip: '192.168.33.114'
  end
end
