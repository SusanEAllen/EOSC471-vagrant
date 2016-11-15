# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrant VM configuration for 2016 EOSC-471 Ariane mini-project.


# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.define "miniproj3" do |miniproj3|
    # Ubuntu 14.04 LTS
    miniproj3.vm.box = "ubuntu/trusty64"
    nowcast.vm.provider "virtualbox" do |v|
      v.memory = 1024
    end
  end

  # Provisioning
  config.vm.provision "shell", inline: <<-SHELL
    apt-get update

    TIMEZONE=Canada/Pacific
    echo "Set timezone to ${TIMEZONE}"
    timedatectl set-timezone ${TIMEZONE}

    apt-get install -y mg
    apt-get install -y gfortran libnetcdf-dev

    if [ -f /home/vagrant/bin/ariane ]; then
      echo "Ariane executable already exists"
    else
      echo "Downloading and unpacking Ariane source code"
      su vagrant -c ' \
        curl --silent -o /home/vagrant/ariane-2.2.6_08.tar.gz https://www.eoas.ubc.ca/~sallen/ariane-2.2.6_08.tar.gz \
        && cd /home/vagrant/ \
        && tar -xvzf ariane-2.2.6_08.tar.gz \
      '

      echo "Building Ariane executable"
      su vagrant -c ' \
        cd /home/vagrant/ariane-2.2.6_08 \
        && export NETCDF_INC=/usr/include \
        && export NETCDF_LIB=/usr/lib \
        && ./configure --prefix=/home/vagrant \
        && make \
        && make check \
        && make install \
      '
    fi
  SHELL
end
