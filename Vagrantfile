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
    #ansible.vm.net :private_network, ip: '192.168.33.112'
    ansible.vm.network :forwarded_port, guest: 80, host: 8081

    ansible.vm.provision :ansible do |ans|
      # where the playbook is location
      ans.playbook = 'provisioners/ansible/playbook.yml'
    end
  end

  config.vm.define :chef do |chef|
    # chef.vm.net :private_network, ip: '192.168.33.113'
    chef.vm.network :forwarded_port, guest: 80, host: 8082
    chef.vm.provision :chef_solo do |chef_app|
      # where the playbook is location
      chef_app.cookbooks_path = 'provisioners/chef/cookbooks'
      chef_app.add_recipe 'apache'
    end
  end

  config.vm.define :puppet do |puppet|
    puppet.vm.net :private_network, ip: '192.168.33.114'
  end
end
