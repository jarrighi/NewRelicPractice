# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|

  config.vm.box = "fitmentgroup/rvmruby222"

  config.vm.network "forwarded_port", guest: 3000, host: 3030

  config.vm.provision "shell", inline: <<-SHELL
    sudo apt-get update
    sudo apt-get install -y postgresql postgresql-contrib
    sudo apt-get install -y libpq-dev
    sudo apt-get install -y nodejs
  SHELL
end