# -*- mode: ruby -*-
# vi: set ft=ruby :

ceph_node1 = 'ceph-node1'
ceph_node1_disk1 = './ceph-node1/ceph-node1_disk1.vdi'
ceph_node1_disk2 = './ceph-node1/ceph-node1_disk2.vdi'
ceph_node1_disk3 = './ceph-node1/ceph-node1_disk3.vdi'

BOX='oraclelinux/9'
BOX_URL='https://oracle.github.io/vagrant-projects/boxes/oraclelinux/9.json'

Vagrant.configure("2") do |config|

  config.vm.provider "virtualbox" do |v|
    v.memory = 4096
	v.cpus = 1
    v.gui = true
  end

  config.vm.define ceph_node1 do |node1|

    node1.vm.box = BOX
    node1.vm.box_url = BOX_URL
    node1.vm.network "public_network", bridge: "eno1", ip: "192.168.1.54"
    node1.vm.hostname = "ceph-node1"
    node1.vm.synced_folder ".", "/vagrant", disabled: true

    node1.vm.provider "virtualbox" do |v|
      # Create and attach disk1 if it doesn't exist
      unless File.exist?(ceph_node1_disk1)
        v.customize ['createhd', '--filename', ceph_node1_disk1, '--size', 10240]
        v.customize ['storageattach', :id, '--storagectl', 'SATA Controller', '--port', 1, '--device', 0, '--type', 'hdd', '--medium', ceph_node1_disk1]
      end

      # Create and attach disk2 if it doesn't exist
      unless File.exist?(ceph_node1_disk2)
        v.customize ['createhd', '--filename', ceph_node1_disk2, '--size', 10240]
        v.customize ['storageattach', :id, '--storagectl', 'SATA Controller', '--port', 2, '--device', 0, '--type', 'hdd', '--medium', ceph_node1_disk2]
      end

      # Create and attach disk3 if it doesn't exist
      unless File.exist?(ceph_node1_disk3)
        v.customize ['createhd', '--filename', ceph_node1_disk3, '--size', 10240]
        v.customize ['storageattach', :id, '--storagectl', 'SATA Controller', '--port', 3, '--device', 0, '--type', 'hdd', '--medium', ceph_node1_disk3]
      end
    end
  end
end
