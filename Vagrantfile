# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "debian/bookworm64"

  config.vm.provision "shell", inline: <<-SHELL
  apt-get  update
  apt-get install -y bind9 dnsutils
  SHELL

  config.vm.define "master" do |master|
    master.vm.hostname = "tierra.sistema.test"
    master.vm.network "private_network", ip: "192.168.57.103"
    master.vm.provision "shell", name: "master-dns" ,inline: <<-SHELL
      cp -v /vagrant/named /etc/default/
      cp -v /vagrant/named.conf.options /etc/bind/
      cp -v /vagrant/file/master/named.conf.local /etc/bind/
      cp -v /vagrant/dns.sistema.test /var/lib/bind/
      cp -v /vagrant/rev.sistema.test /var/lib/bind/
      systemctl restart named
    SHELL
  end
  config.vm.define "slave" do |slave|
    slave.vm.hostname = "venus.sistema.test"
    slave.vm.network "private_network", ip: "192.168.57.102"
    slave.vm.provision "shell", name: "slave-dns" ,inline: <<-SHELL
      cp -v /vagrant/named /etc/default/
      cp -v /vagrant/named.conf.options /etc/bind/
      cp -v /vagrant/file/slave/named.conf.local.slave /etc/bind/named.conf.local
      systemctl restart named
    SHELL
  end
end