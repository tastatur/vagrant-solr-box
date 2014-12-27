# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "precise64"
  config.vm.box_url = "http://files.vagrantup.com/precise64.box"
  config.vm.network :forwarded_port, guest: 8983, host: 8983
  config.vm.provision :shell do |shell|
    shell.inline = "puppet module install puppetlabs/apt --force --modulepath '/vagrant/modules';
                   puppet module install puppetlabs/stdlib --force --modulepath '/vagrant/modules'"
  end
  config.vm.provision :puppet, :module_path => "modules" do |puppet|
    puppet.manifests_path = "manifests"
    puppet.manifest_file  = "default.pp"
  end
  config.vm.provider "virtualbox" do |v|
    v.customize ["modifyvm", :id, "--cpus", "2"]
    v.customize ["modifyvm", :id, "--memory", "3096"]
  end
end
