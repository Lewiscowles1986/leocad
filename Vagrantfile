# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/xenial64"
  config.vm.network "public_network"

  config.vm.provider "virtualbox" do |vb|
    # Display the VirtualBox GUI when booting the machine
    vb.gui = true
    # Customize the amount of memory on the VM:
    vb.memory = "2048"
    vb.cpus = 2
  end

  config.vm.provision "shell", inline: <<-SHELL
    apt-get update
    apt-get install -y git build-essential zlib1g-dev

    add-apt-repository -y ppa:beineri/opt-qt59-xenial
    apt-get update -yqq

    apt-get install -yqq qt59base qt59tools qt59gamepad libqt5opengl5-dev
    export QT_BASE=59
    source /opt/qt59/bin/qt59-env.sh

    mkdir /tmp/build
    cp -ar /vagrant/* /tmp/build/
    cd /tmp/build
    sed -i '10 s/^/#/' PKGBUILD
    sed -i '12 s/#//' PKGBUILD

    qmake PREFIX=/usr -v
    qmake PREFIX=/usr -r
    make -j4
  SHELL
end
