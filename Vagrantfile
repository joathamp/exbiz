require 'yaml'
secmachines = YAML.load_file("machines.yml")

Vagrant.configure("2") do |config|
  secmachines.each do |machines|
    config.vm.define machines["name"] do |server|
      server.vm.hostname = machines["name"]
      server.vm.box = machines["box"]
      server.vm.box_check_update = false
      server.vm.network "private_network", ip: machines["ip"], dns: "8.8.8.8" 

      server.vm.provider "virtualbox" do |vb|
        vb.customize ["modifyvm", :id, "--groups", "/EXBIZ"]
        vb.memory = machines["memory"]
        vb.cpus = machines["cpus"]
        vb.name = machines["name"]
      end
    end
  end
end
