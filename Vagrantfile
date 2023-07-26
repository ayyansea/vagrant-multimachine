# -*- mode: ruby -*-
# vi: set ft=ruby :

# General settings

BOX = "generic/debian10"
BASENAME = "node"
COUNT = 3
CPU = 2
MEM = 2048
PROVIDER = "libvirt"
SUBNET = "10.20.0"

# Here goes your PUBLIC ssh key

SSH_KEY = ""

# -----------------------------

LIBVIRT_HOST = ""
LIBVIRT_USER = ""
LIBVIRT_PASSWORD = ""

Vagrant.configure("2") do |config|
  (1..COUNT).each do |i|
    hostname = "#{BASENAME}-#{i}"
    ip_address = "#{SUBNET}.#{i+2}"

    config.vm.define hostname do |node|
      node.vm.box = BOX
      node.vm.hostname = hostname

      if PROVIDER == "libvirt"
        node.vm.provider PROVIDER do |provider|
          provider.cpus = CPU
          provider.memory = MEM

          if not LIBVIRT_HOST.empty?
            provider.host = LIBVIRT_HOST
          end

          if not LIBVIRT_USER.empty?
            provider.username = LIBVIRT_USER
          end

          if not LIBVIRT_PASSWORD.empty?
            provider.password = LIBVIRT_PASSWORD
          end
        end
      end

      node.vm.network "private_network", ip: ip_address
    end
  end
end
