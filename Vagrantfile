# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "debian/bookworm64"

  config.vm.define "master" do |master|
    master.vm.hostname = "tierra.sistema.test"
    master.vm.network "private_network", ip: "192.168.57.103"
    master.vm.provision "shell", name: "master-dns" ,inline: <<-SHELL
      cp -v /vagrant/file/named /etc/default/
      cp -v /vagrant/file/named.conf.options /etc/bind
      cp -v /vagrant/file/master/named.conf.local /etc/bind
      cp -v /vagrant/file/sistema.test.dns /var/lib/bind
      cp -v /vagrant/file/sistema.test.rev /var/lib/bind
      systemctl restart named
    SHELL
  end
  config.vm.define "slave" do |slave|
    slave.vm.hostname = "venus.sistema.test"
    slave.vm.network "private_network", ip: "192.168.57.102"
    slave.vm.provision "shell", name: "slave-dns" ,inline: <<-SHELL
      cp -v /vagrant/file/named /etc/default/
      cp -v /vagrant/file/named.conf.options /etc/bind
      cp -v /vagrant/file/slave/named.conf.local.slave /etc/bind/named.cond.local
      systemctl restart named
    SHELL
  end
end