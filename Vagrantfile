# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://vagrantcloud.com/search.
  config.vm.box = "chenhan/lubuntu-desktop-18.04"

  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  # config.vm.box_check_update = false

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  # NOTE: This will enable public access to the opened port
  config.vm.network "forwarded_port", guest: 80, host: 8080
  config.vm.network "forwarded_port", guest: 443, host: 8443

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine and only allow access
  # via 127.0.0.1 to disable public access
  # config.vm.network "forwarded_port", guest: 80, host: 8080, host_ip: "127.0.0.1"

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  # config.vm.network "private_network", ip: "192.168.33.10"

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network "public_network"

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  # config.vm.synced_folder "../data", "/vagrant_data"

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
  config.vm.provider "virtualbox" do |vb|
  #   # Display the VirtualBox GUI when booting the machine
      vb.gui = true
  #
  #   # Customize the amount of memory on the VM:
      vb.cpus = 2
      vb.memory = "1024"
      vb.customize ["modifyvm", :id, "--vram", "64"]
      vb.customize ["modifyvm", :id, "--clipboard", "bidirectional"]
      vb.customize ["modifyvm", :id, "--audio", "none"]
  end
  #
  # View the documentation for the provider you are using for more
  # information on available options.

  # Enable provisioning with a shell script. Additional provisioners such as
  # Puppet, Chef, Ansible, Salt, and Docker are also available. Please see the
  # documentation for more information about their specific syntax and use.
  config.vm.provision "shell", inline: <<-SHELL
      export DEBIAN_FRONTEND=noninteractive
      # export LANGUAGE=en_US.UTF-8
      # export LANG=en_US.UTF-8
      # export LC_ALL=en_US.UTF-8
      # locale-gen en_US.UTF-8
      # dpkg-reconfigure locales
	  apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 9DA31620334BD75D9DCB49F368818C72E52529D4
	  echo "deb [ arch=amd64 ] https://repo.mongodb.org/apt/ubuntu bionic/mongodb-org/4.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-4.0.list
      apt-get update
	  apt-get install -y mongodb-org ttf-anonymous-pro
	  systemctl enable mongod
	  systemctl start mongod
      cd /tmp
      wget -q https://download-test.robomongo.org/linux/robo3t-1.3.1-linux-x86_64-7419c406.tar.gz
      tar xf robo3t-1.3.1-linux-x86_64-7419c406.tar.gz -C /opt/
      mv /opt/robo3t-1.3.1-linux-x86_64-7419c406 /opt/robo3t
      ln -s /opt/robo3t/bin/robo3t /usr/local/bin/robo3t
      cat > /usr/share/applications/robo3t.desktop << EOL
[Desktop Entry]
Name=Robo 3T
Comment=Database shell for MongoDB
Encoding=UTF-8
Exec=robo3t
Icon=gksu-root-terminal
StartupNotify=true
Terminal=false
Type=Application
Categories=Utility;GTK;GNOME;
EOL
       mkdir -p /vagrant/samples/dump/Samples
       cd /vagrant/samples/dump/Samples
       wget -q -nc https://github.com/SouthbankSoftware/dbkoda-data/raw/master/SampleCollections/dump/SampleCollections/samples_pokemon.bson
       wget -q -nc https://github.com/SouthbankSoftware/dbkoda-data/raw/master/SampleCollections/dump/SampleCollections/samples_pokemon.metadata.json 
       cd /vagrant/samples
       mongorestore
       cat > /usr/share/lxterminal/lxterminal.conf << EOL
[general]
fontname=Anonymous Pro 14
selchars=-A-Za-z0-9,./?%&#:_
scrollback=1000
EOL
mkdir /home/vagrant/.config/lxterminal -p
cat > /home/vagrant/.config/lxterminal/lxterminal.conf << EOL
[general]
fontname=Anonymous Pro 14
selchars=-A-Za-z0-9,./?%&#:_
scrollback=1000
EOL
chown -R vagrant:vagrant /home/vagrant/.config
cat > /etc/lightdm/lightdm.conf.d/10-autologin.conf << EOL
[Seat:*]
autologin-guest = false
autologin-user = vagrant
autologin-user-timeout = 0

[SeatDefaults]
allow-guest = false
EOL
       reboot
# wget https://downloads.mongodb.com/compass/mongodb-compass-community_1.17.0_amd64.deb
# dpkg -i mongodb-compass-community_1.17.0_amd64.deb
# git clone https://github.com/SouthbankSoftware/dbkoda-data.git
# cd dbkoda-data/SampleCollections
# mongorestore
# cd ../..
  SHELL
end
