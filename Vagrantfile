# -*- mode: ruby -*-
# # vi: set ft=ruby :

Vagrant.configure(2) do |config|

  (1..7).each do |i|

    config.vm.define "vm#{i}" do |s|
      #s.ssh.forward_agent = true
      s.vm.box = "bento/ubuntu-16.04"
      s.vm.hostname = "vm#{i}"
      s.vm.provision :shell, path: "scripts/bootstrap.sh"
      #s.vm.provision :shell, inline: "PYTHONUNBUFFERED=1 ansible-playbook /vagrant/ansible/worker.yml -c local"
      s.vm.network "public_network", ip: "192.168.1.18#{i}", auto_config: true
      s.vm.provider "virtualbox" do |v|
        v.name = "vm#{i}"
        v.memory = 2048
        v.gui = false
        unless File.exist?("vm#{i}disk2.vdi")
          v.customize ['createhd', '--filename', "vm#{i}disk2.vdi", '--format', 'VDI', '--size', 30 * 1024]
        end
        v.customize ['storageattach', :id, '--storagectl', 'SATA Controller', '--port', 5, '--device', 0, '--type', 'hdd', '--medium', "vm#{i}disk2.vdi"]

      end
    end
  end
end


