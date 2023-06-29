Vagrant.require_version ">= 2.3.7"
ENV["LC_ALL"] = "en_US.UTF-8"
BOX_MEM = ENV['BOX_MEM'] || "2048"
NODE_NUM = 8
IP_RANGE = "192.168.58."

Vagrant.configure("2") do |config|
  (1..NODE_NUM).each do |i|
    config.vm.define "dn#{i}" do |datanode|
      datanode.vm.box = 'gusztavvargadr/ubuntu-server'
      datanode.vm.hostname = "dn#{i}"
      datanode.ssh.forward_agent = true
      datanode.vm.provider "virtualbox" do |v|
        v.name = "dn#{i}" 
        v.customize ["modifyvm", :id, "--memory", BOX_MEM]
        v.customize ["modifyvm", :id, "--ioapic", "on"]
        v.customize ["modifyvm", :id, "--cpus", "2"]
      end
      datanode.vm.network "private_network", ip: IP_RANGE + "#{i + 2}"
    end
  end
  
  config.vm.define "nn1" do |datanode|
    datanode.vm.box = 'gusztavvargadr/ubuntu-server'
    datanode.vm.hostname = "nn1"
    datanode.ssh.forward_agent = true
    datanode.vm.network "private_network", ip: IP_RANGE + "2"
    datanode.vm.provider "virtualbox" do |v|
      v.name = "nn1" 
      v.customize ["modifyvm", :id, "--memory", BOX_MEM]
      v.customize ["modifyvm", :id, "--ioapic", "on"]
      v.customize ["modifyvm", :id, "--cpus", "2"]
      v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
      v.customize ["modifyvm", :id, "--natdnsproxy1", "on"]
    end
  end
end