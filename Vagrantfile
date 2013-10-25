# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "precise64"
  config.vm.box_url = "http://files.vagrantup.com/precise64.box"

  # Uncomment the next line if you like to watch.
  # config.vm.boot_mode = :gui

  # Port 8000 on the host will go to port 80 on the Vagrant box
  config.vm.network :forwarded_port, guest: 80, host: 8000, auto_correct: true

  # Here's a folder for passing stuff back and forth
  # config.vm.synced_folder "./shared", "/home/vagrant/host_shared"
  config.vm.synced_folder "./shared", "/var/www"

  config.vm.provision :chef_solo do |chef|
    chef.json = {
      :mysql => {
        :server_root_password   => "root",
        :server_repl_password   => "root",
        :server_debian_password => "root"
      }
    }
    chef.cookbooks_path = "cookbooks"
    # You can add any cookbook here you like by specifying the name
    # You can find cookbooks on : https://github.com/opscode-cookbooks
    chef.add_recipe "apt"
    chef.add_recipe "ohai"
    chef.add_recipe "configure"
    chef.add_recipe "phpmyadmin"
  end
end
