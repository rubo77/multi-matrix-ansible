# Defines our Vagrant environment
#
# -*- mode: ruby -*-
# vi: set ft=ruby :
Vagrant.configure("2") do |config|

  # disable guest additions
  config.vbguest.auto_update = false

  config.vm.define :matrixdev do |web_config|
    web_config.vm.box = "sharlak/debian_stretch_64"
    web_config.vm.hostname = "matrixdev"
    web_config.vm.network :private_network, ip: "10.0.1.10"
    web_config.vm.provider "virtualbox" do |vb|
      vb.memory = "512"
    end

    web_config.vm.provision "ansible" do |ansible|
      ansible.playbook = "multi-matrix.yml"
      ansible.groups = {
        "multi-matrix" => ['matrixdev']
      }
      ansible.host_vars = {
        "matrixdev" => {"ansible_become" => true, 'matrix_domain' => 'dummy.site'}
      }
      ansible.verbose = 'v'
      ansible.tags = ['matrix']
    end
  end

end
