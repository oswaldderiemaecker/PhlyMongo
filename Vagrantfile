# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = '2'

@script = <<SCRIPT
DOCUMENT_ROOT_ZEND="/var/www/zf/public"
apt-get update
apt-get install -y git curl php5-cli php5 php5-intl php5-dev make php-pear mongodb
printf "\n" | pecl install mongo
echo "extension=mongo.so" | tee /etc/php5/mods-available/mongo.ini
php5enmod mongo
cd /vagrant
curl -Ss https://getcomposer.org/installer | php
php composer.phar install --no-progress
SCRIPT

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = 'chef/ubuntu-14.04'
  config.vm.hostname = "phly-mongo.local"
  config.vm.provision 'shell', inline: @script

  config.vm.provider "virtualbox" do |vb|
    vb.customize ["modifyvm", :id, "--memory", "1024"]
  end

end
