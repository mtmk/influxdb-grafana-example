# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|
  config.vm.box = "ubuntu/trusty64"
  config.vm.hostname = "influ-graf-1"

  config.vm.network "private_network", ip: "192.168.46.11"

  # config.vm.synced_folder "../data", "/vagrant_data"
  config.vm.synced_folder "~/go", "/home/vagrant/go"

  config.vm.provider "virtualbox" do |vb|
    vb.name = "influ-graf-1"
  end
  
  config.vm.provision "shell", inline: <<-SHELL
    apt-get update
    apt-get install -y git
    apt-get install -y supervisor

    echo "Installing Go 1.4.2"
    mkdir /tmp-install
    cd /tmp-install
    wget -q https://storage.googleapis.com/golang/go1.4.2.linux-amd64.tar.gz
    tar -C /usr/local -zxf go1.4.2.linux-amd64.tar.gz

    echo 'export PATH=$PATH:/usr/local/go/bin' >> /home/vagrant/.profile
    echo 'export GOPATH=$HOME/go' >> /home/vagrant/.profile

    wget https://s3.amazonaws.com/influxdb/influxdb_0.9.2_amd64.deb
    dpkg -i influxdb_0.9.2_amd64.deb 

    #wget http://get.influxdb.org/telegraf/telegraf_0.1.4_amd64.deb
    #dpkg -i telegraf_0.1.4_amd64.deb

    wget https://grafanarel.s3.amazonaws.com/builds/grafana_2.1.0_amd64.deb
    apt-get install -y adduser libfontconfig
    dpkg -i grafana_2.1.0_amd64.deb

  SHELL

end

