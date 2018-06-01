
Create 4 machine base on vagrant

sudo apt-get update
sudo apt-get install apache2
rm -rm /var/www # thu muc khi cai dat apache
ln -fs /vagrant/ /var/www

Bai giai

# create a new file index.html
$ echo "<h1> Hello word! </h1>" > index.html
$ mkdir -p /prosioner{bash,ansible,chef,puppet}

Machine 1: using bash
# in Vagrantfile: add

  config.vm.define 'bash' do |bash|
    bash.vm.net :private_network, ip: '192.168.33.111'
  end

$ touch /prosioner/bash/install-apache.sh
# Read 'install-apache.sh.

Machine 2: using ansible
Machine 3: using chef
Machine 4: using puppet
