# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  # All Vagrant configuration is done here. The most common configuration
  # options are documented and commented below. For a complete reference,
  # please see the online documentation at vagrantup.com.

  # Every Vagrant virtual environment requires a box to build off of.
  config.vm.box = "precise64"

  # Enable provisioning with chef solo, specifying a cookbooks path, roles
  # path, and data_bags path (all relative to this Vagrantfile), and adding
  # some recipes and/or roles.
  #
  config.vm.provision :shell, :inline => 'apt-get update'
  config.vm.provision :shell, :inline => 'apt-get install build-essential 1.9.1-dev --no-upgrade --yes'
  config.vm.provision :shell, :inline => "gem install chef --version 11.10.4 --no-rdoc --no-ri --conservative"
  config.vm.provision "chef_solo" do |chef|
    chef.cookbooks_path = ["cookbooks"]
    chef.data_bags_path = "databags"
    chef.add_recipe "vim"
    chef.json = {
      :users => ['jrice']
    }
    chef.log_level = :debug # TODO - comment this out when you're done tweaking.
  end
end
