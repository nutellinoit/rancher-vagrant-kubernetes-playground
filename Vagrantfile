# -*- mode: ruby -*-
# # vi: set ft=ruby :

Vagrant.configure(2) do |config|

  (1..6).each do |i|

    config.vm.define "vm#{i}" do |s|
      #s.ssh.forward_agent = true
      config.vm.provider "virtualbox" do |vb|
        second_disk = "vm#{i}disk2.vdi"
        unless File.exist?(second_disk)
          vb.customize ['createhd', '--filename', second_disk, '--format', 'VDI', '--size', 10 * 1024]
        end
        vb.customize ['storageattach', :id, '--storagectl', 'SATA Controller', '--port', 5, '--device', 0, '--type', 'hdd', '--medium', second_disk]
      end



      s.vm.box = "bento/ubuntu-16.04"
      s.vm.hostname = "vm#{i}"
      s.vm.provision :shell, path: "scripts/bootstrap.sh"
      #s.vm.provision :shell, inline: "PYTHONUNBUFFERED=1 ansible-playbook /vagrant/ansible/worker.yml -c local"
      s.vm.network "public_network", ip: "192.168.1.18#{i}", auto_config: true
      s.vm.provider "virtualbox" do |v|
        v.name = "vm#{i}"
        v.memory = 2048
        v.gui = false
      end
    end

  end
end


