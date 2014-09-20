# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "base"

  config.hostmanager.enabled = true
  config.hostmanager.manage_host = true

  config.vm.define "web" do |web|
    web.vm.box = "chef/debian-7.4"
    web.vm.network "private_network", ip: "192.168.50.3"
    web.hostmanager.aliases = %w(www.dev.taka3sh.org dev.taka3sh.org secure.dev.taka3sh.org nv.dev.taka3sh.org)
  end

  config.vm.define "db" do |db|
    db.vm.box = "chef/centos-6.5"
    db.vm.network "private_network", ip: "192.168.50.4"
    db.hostmanager.aliases = %w(db.dev.taka3sh.org)
  end

  config.vm.provision "ansible" do |ansible|
    ansible.groups = {
      "webservers" => ["web"],
      "dbservers"  => ["db"]
    }
    ansible.playbook = "site.yml"
  end
end
