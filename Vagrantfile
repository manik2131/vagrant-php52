# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  # All Vagrant configuration is done here. The most common configuration
  # options are documented and commented below. For a complete reference,
  # please see the online documentation at vagrantup.com.

  # Every Vagrant virtual environment requires a box to build off of.
  config.vm.box = "box-cutter/ubuntu1004"

  config.vm.provider "virtualbox" do |vb|
    vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    vb.customize ["modifyvm", :id, "--natdnsproxy1", "on"]
    vb.customize ["modifyvm", :id, "--memory", 2048, "--cpus", "4"]
    vb.customize ["setextradata", :id, "VBoxInternal2/SharedFoldersEnableSymlinksCreate/v-root", "1"]
  end

  config.vm.network "private_network", ip: "192.168.100.50"

  # If true, then any SSH connections made will enable agent forwarding.
  # Default value: false
  # config.ssh.forward_agent = true

  config.vm.synced_folder ".", "/vagrant", type: "nfs"

  # Set the Timezone to something useful
  config.vm.provision "shell", inline: "echo \"Europe/Paris\" | sudo tee /etc/timezone && dpkg-reconfigure --frontend noninteractive tzdata"

  # Update version and install PHP 5.2 repository
  config.vm.provision "shell", inline: "apt-get update"
  config.vm.provision "shell", inline: "sudo apt-get -y upgrade"
  config.vm.provision "shell", inline: "sudo aptitude -y install python-software-properties"
  config.vm.provision "shell", inline: "sudo add-apt-repository ppa:andphe/php"
  config.vm.provision "shell", inline: "sudo aptitude update"

  # install apache
  config.vm.provision "shell", inline: "sudo apt-get install -y apache2"

  config.vm.provision "shell", inline: "sudo aptitude -y install php5-common=5.2.17.dfsg.1-0ubuntu0ppa3~lucid libapache2-mod-php5=5.2.17.dfsg.1-0ubuntu0ppa3~lucid php5=5.2.17.dfsg.1-0ubuntu0ppa3~lucid php5-cli=5.2.17.dfsg.1-0ubuntu0ppa3~lucid php5-curl=5.2.17.dfsg.1-0ubuntu0ppa3~lucid php5-mcrypt=5.2.17.dfsg.1-0ubuntu0ppa3~lucid php5-gd=5.2.17.dfsg.1-0ubuntu0ppa3~lucid php5-dev=5.2.17.dfsg.1-0ubuntu0ppa3~lucid php-pear=5.2.17.dfsg.1-0ubuntu0ppa3~lucid"

  # install mysql
  config.vm.provision "shell", path: "mysql.sh"

  # install apc
  config.vm.provision "shell", inline: "sudo apt-get install -y php-apc"

  # set locales
  config.vm.provision "shell", inline: "sudo locale-gen fr_FR.UTF-8"
  config.vm.provision "shell", inline: "sudo dpkg-reconfigure locales"

end
