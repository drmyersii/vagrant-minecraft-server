# Vim
# vim: set filetype=ruby:
# vim: set ft=ruby:
#
# Emacs
# -*- mode: ruby; -*-
require "yaml"


conf = YAML.load_file "config.yml"

Vagrant.configure("2") do |config|

    # disable vagrant shared root directory
    config.vm.synced_folder ".", "/vagrant", disabled: true

    # settings for DigitalOcean provider
    config.vm.provider :digital_ocean do |provider, override|
        override.vm.box     = "digital_ocean"
        override.vm.box_url = "https://github.com/smdahlen/vagrant-digitalocean/raw/master/box/digital_ocean.box"

        override.ssh.private_key_path = conf["digitalocean"]["ssh_key"]

        provider.token  = conf["digitalocean"]["token"]
        provider.image  = conf["digitalocean"]["image"]
        provider.region = conf["digitalocean"]["region"]
        provider.size   = conf["digitalocean"]["size"]
    end

    # settings for Linode provider
    config.vm.provider :linode do |provider, override|
        override.vm.box     = "linode"
        override.vm.box_url = "https://github.com/displague/vagrant-linode/raw/master/box/linode.box"

        override.ssh.private_key_path = conf["linode"]["ssh_key"]

        provider.token        = conf["linode"]["token"]
        provider.distribution = conf["linode"]["distribution"]
        provider.datacenter   = conf["linode"]["datacenter"]
        provider.plan         = conf["linode"]["plan"]
    end

    # call provisioning shell script
    config.vm.provision :shell, path: "./provision.sh"
end
