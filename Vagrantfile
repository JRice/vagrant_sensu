# -*- mode: ruby -*-
# vi: set ft=ruby :

$install_chef = <<SCRIPT
if ! [ -d "/opt/chef" ];
then
  apt-get update
  apt-get install -y curl
  curl -L https://www.opscode.com/chef/install.sh | bash
fi
SCRIPT

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  # All Vagrant configuration is done here. The most common configuration
  # options are documented and commented below. For a complete reference,
  # please see the online documentation at vagrantup.com.

  # Every Vagrant virtual environment requires a box to build off of.
  config.vm.box = "precise64"

  config.vm.network "forwarded_port", guest: 8080, host: 8181

  # Enable provisioning with chef solo, specifying a cookbooks path, roles
  # path, and data_bags path (all relative to this Vagrantfile), and adding
  # some recipes and/or roles.
  #
  config.vm.provision :shell, :inline => $install_chef

  config.vm.provision "chef_solo" do |chef|
    chef.data_bags_path = "data_bags"
    chef.add_recipe "ntp"
    chef.add_recipe "vim"
    # Note that this includes sensu::dashboard:
    chef.add_recipe "monitor::master"
    chef.add_recipe "monitor::redis"
    chef.add_recipe "monitor::rabbitmq"
    chef.json = {
      :users => ['jrice']
    }
    # chef.log_level = :debug
  end
end
