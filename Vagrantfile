# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrant VM configuration for 2016 EOSC-471 Ariane mini-project.


# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.define "miniproj3" do |miniproj3|
    # Ubuntu 14.04 LTS
    miniproj3.vm.box = "ubuntu/trusty64"
  end

  # Provisioning
  config.vm.provision "shell", inline: <<-SHELL
    apt-get update

    TIMEZONE=Canada/Pacific
    echo "Set timezone to ${TIMEZONE}"
    timedatectl set-timezone ${TIMEZONE}

    apt-get install -y mg
    apt-get install -y gfortran netcdf-bin
  SHELL
end
