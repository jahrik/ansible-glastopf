# -*- mode: ruby -*-
# vi: set ft=ruby :

require_relative './files/key_authorization.rb'
VAGRANTFILE_API_VERSION = '2'.freeze
Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.define 'debian' do |debian|
    debian.vm.box = 'bento/debian-8.2'
    debian.vm.provider 'virtualbox' do |vb|
      vb.gui = false
      vb.memory = '1024'
    end
    debian.vm.hostname = "debian.dev"
    debian.vm.network "public_network", bridge: [
      "wlp3s0",
      "wlan0",
    ]
    debian.vm.provision 'shell', inline: 'apt-get update'
    debian.vm.provision 'shell', inline: 'id -u pi &>/dev/null || useradd -m -s /bin/bash -p raspberry -U -G users,sudo pi'
    debian.vm.provision 'shell', inline: 'apt-get install xfce4 lightdm -y'
    authorize_key_for_root config, '~/.ssh/id_rsa.pub'
  end
end
