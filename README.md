
Create 4 machine base on vagrant

    sudo apt-get update
    sudo apt-get install apache2
    rm -rm /var/www # thu muc khi cai dat apache
    ln -fs /vagrant/ /var/www

#Bai giai

 create a new file _index.html_ in _/vagrant/html/_

    $ echo "<h1> Hello word! </h1>" > index.html
    $ mkdir -p /prosioner/{bash,ansible,chef,puppet}

# Machine 1: using bash
In Vagrantfile: add

    config.vm.define 'bash' do |bash|
        bash.vm.net :private_network, ip: '192.168.33.111'
    end

    $ touch /prosioner/bash/install-apache.sh
# Read 'install-apache.sh.

Machine 2: using ansible
# in Vagrantfile: add

    ansible.vm.network :forwarded_port, guest: 80, host: 8081
    config.vm.provision :ansible do |ans|
      # where the playbook is location
      ans.playbook = "provisioners/ansible/playbook.yml"
    end

=> playbook must in provision

# Create folder
ansible
│   │   ├── group_vars
│   │   ├── playbook.retry
│   │   ├── playbook.yml
│   │   └── roles
│   │       └── apache
│   │           └── tasks
│   │               └── main.yml

# Watch _playbook.yml_ and _main.yml_



Machine 3: using chef
# in Vagrantfile: add

  config.vm.define :chef do |chef|
    # chef.vm.net :private_network, ip: '192.168.33.113'
    chef.vm.network :forwarded_port, guest: 80, host: 8082
    chef.vm.provision :chef_solo do |chef_app|
      # where the chef is location
      chef_app.cookbooks_path = 'provisioners/chef/cookbooks'
      chef_app.add_recipe 'apache'
    end
  end

# Create folder
chef
│   │   └── cookbooks
│   │       └── apache
│   │           └── recipes
│   │               └── default.rb


Machine 4: using puppet
# in Vagrantfile: add

  config.vm.define :puppet do |puppet|
    # puppet.vm.net :private_network, ip: '192.168.33.114'
    puppet.vm.network :forwarded_port, guest: 80, host: 8082

    puppet.vm.provision :shell, :inline => <<-SHELL
      apt-get update
      apt-get install -y puppet
    SHELL

    puppet.vm.provision :puppet do |pup_app|
      # where the playbook is location
      pup_app.manifests_path = 'provisioners/puppet/manifests'
      pup_app.manifest_file = 'apache.pp'
    end
  end
# install puppet on vagrant machine

# Create folder
puppet
│       └── manifests
│           └── apache.pp

