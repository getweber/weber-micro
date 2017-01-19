# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant::Config.run do |config|
  config.vm.define :debian do |config|
    config.vm.box = "debian/jessie64"
    config.vm.host_name = "debian"
    config.vm.forward_port 80, 8000
  end
  config.vm.define :ubuntu do |config|
    config.vm.box = "ubuntu/xenial64"
    config.vm.host_name = "ubuntu"
    config.vm.forward_port 80, 8002
  end

  config.vm.provision "ansible" do |ansible|
    ansible.groups = {
      "webapp" => ["debian", "ubuntu"],
    }
    ansible.playbook = "ansible/site.yml"
    ansible.extra_vars = {
      "install_with_debug" => true,
    }
    ansible.sudo = true
  end
end
