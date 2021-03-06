# -*- mode: ruby -*-
# vi: set ft=ruby :

# set the default provider
ENV["VAGRANT_DEFAULT_PROVIDER"] = "virtualbox"

Vagrant.configure(2) do |config|
  config.vm.box = "geerlingguy/ubuntu1604"

  config.vm.provider :virtualbox do |virtualbox|
    virtualbox.cpus = 1
    virtualbox.memory = 1024
  end

  config.vm.provider :digital_ocean do |ocean, override|
    override.ssh.private_key_path = '~/.ssh/id_rsa'
    override.vm.box = "digital_ocean"
    override.vm.box_url = "https://github.com/smdahlen/vagrant-digitalocean/raw/master/box/digital_ocean.box"

    ocean.token = ENV["DIGITAL_OCEAN_TOKEN"]
    ocean.image = "ubuntu-16-04-x64"
    ocean.region = "fra1"
    ocean.size = "1gb"
  end

  config.vm.define :"qemu-arm-box" do |box|
    box.vm.provision "shell", path: "scripts/provision.sh", privileged: false
    box.vm.provision "shell", path: "scripts/install-qemu-aarch64.sh", privileged: false
    box.vm.provision "shell", path: "scripts/install-uefi-bootdisk.sh", privileged: false
    box.vm.provision "shell", path: "scripts/install-image-ubuntu16.04-arm64.sh", privileged: false
    box.vm.provision "shell", path: "scripts/install-network-bridge.sh", privileged: false
  end
end
