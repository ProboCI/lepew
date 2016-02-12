# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "lepew"
  #config.vm.box_url = "http://domain.com/path/to/above.box"
  config.vm.network "private_network", type: "dhcp"
  config.vm.network :private_network, ip: "192.168.33.254"

  config.vm.provider :virtualbox do |vb|
    # Use VBoxManage to customize the VM. For example to change memory:
    vb.customize ["modifyvm", :id, "--memory", "2048"]
  end

  # Install puppet.
  config.vm.provision "shell", path: "scripts/puppet_setup.sh"

  # Run puppet
  config.librarian_puppet.puppetfile_dir = "puppet"
  config.vm.provision "puppet" do |puppet|
    puppet.module_path = "puppet/modules"
    puppet.manifests_path = "puppet/manifests"
    puppet.manifest_file = "main.pp"
    puppet.options = ["--debug", "--trace"]
  end

  config.ssh.forward_agent = true
end
